# Infrastructure: Shared VPS with Docker Compose

## Overview

We're sharing the Contabo VPS (212.56.33.218) with OFUNDEFINED landing page using **docker-compose** for isolation.

**Architecture**:
```
Contabo VPS (212.56.33.218)
│
├─ nginx (reverse proxy) — Port 80/443
│  ├─ requests to alfabetizacao.ofundefined.com → app_backend:3001
│  ├─ requests to mvp-dev.viamoto.app → viamoto_backend:3002
│  ├─ requests to app.oliveiraenfermagem.com.br → oliveira_backend:3003
│  └─ static files (landing pages, etc)
│
└─ Docker Compose services
   ├─ app_backend (Node.js + PostgreSQL for Caminho das Letras)
   ├─ viamoto_backend (Laravel + Postgres for ViaMoto)
   ├─ oliveira_backend (Monolith for Oliveira Enfermagem)
   └─ monitoring (optional: Prometheus, Grafana, etc)
```

---

## Why Docker Compose (Not API Gateway)

### API Gateway (e.g., Kong, Traefik) — When Needed
- **Pros**: Centralized auth, rate limiting, request transformation, monitoring
- **Cons**: Overkill for MVP, adds complexity, operational overhead

### Docker Compose + Nginx — Perfect for MVP
- **Pros**: Simple, lightweight, easy to manage, proven at scale
- **Cons**: Less sophisticated routing/transformation

**Decision**: Start with **nginx reverse proxy** in docker-compose. If we need advanced routing (auth, rate limiting, request transformation), migrate to Traefik or Kong later.

---

## Setup: docker-compose.yml

```yaml
version: '3.9'

services:
  # ===== Nginx Reverse Proxy =====
  nginx:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl/certs:/etc/nginx/ssl:ro
      - /var/www/static:/usr/share/nginx/html:ro
    depends_on:
      - app_backend
      - viamoto_backend
      - oliveira_backend
    networks:
      - shared_network
    restart: unless-stopped

  # ===== Caminho das Letras Backend =====
  app_backend:
    build:
      context: ./alfabetizacao-app/backend  # Node.js + Express
      dockerfile: Dockerfile
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://app_user:password@postgres:5432/alfabetizacao
      - JWT_SECRET=your-secret-here
      - FIREBASE_CREDENTIALS=${FIREBASE_CREDENTIALS}
    depends_on:
      - postgres
    networks:
      - shared_network
    restart: unless-stopped
    labels:
      - "com.example.description=Caminho das Letras Backend"

  # ===== Postgres (Shared) =====
  postgres:
    image: postgres:15-alpine
    environment:
      - POSTGRES_PASSWORD=secure_password
      - POSTGRES_INITDB_ARGS=-c shared_buffers=256MB
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init-dbs.sql:/docker-entrypoint-initdb.d/init.sql  # Create multiple DBs
    networks:
      - shared_network
    restart: unless-stopped

  # ===== ViaMoto Backend (Laravel) =====
  viamoto_backend:
    build:
      context: ./viamoto/backend
      dockerfile: Dockerfile
    environment:
      - APP_ENV=production
      - APP_DEBUG=false
      - DB_CONNECTION=pgsql
      - DB_HOST=postgres
      - DB_PORT=5432
      - DB_DATABASE=viamoto
      - DB_USERNAME=viamoto_user
      - DB_PASSWORD=secure_password
    depends_on:
      - postgres
    networks:
      - shared_network
    restart: unless-stopped

  # ===== Oliveira Monolith =====
  oliveira_backend:
    build:
      context: ./oliveiraenfermagem/monolith
      dockerfile: Dockerfile
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://oliveira_user:password@postgres:5432/oliveira
      - SUPABASE_URL=https://supabase.oliveiraenfermagem.com.br
      - SUPABASE_ANON_KEY=${SUPABASE_ANON_KEY}
    depends_on:
      - postgres
    networks:
      - shared_network
    restart: unless-stopped

volumes:
  postgres_data:

networks:
  shared_network:
    driver: bridge
```

---

## nginx.conf Setup

```nginx
upstream app_backend {
    server app_backend:3001;
}

upstream viamoto_backend {
    server viamoto_backend:3000;
}

upstream oliveira_backend {
    server oliveira_backend:3000;
}

# Redirect HTTP to HTTPS
server {
    listen 80;
    server_name _;
    return 301 https://$host$request_uri;
}

# HTTPS Server Block
server {
    listen 443 ssl http2;
    server_name alfabetizacao.ofundefined.com mvp-dev.viamoto.app app.oliveiraenfermagem.com.br;

    ssl_certificate /etc/nginx/ssl/certificate.crt;
    ssl_certificate_key /etc/nginx/ssl/private.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    # Caminho das Letras Backend
    location /api/alfabetizacao {
        proxy_pass http://app_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # ViaMoto Backend
    location /api/viamoto {
        proxy_pass http://viamoto_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Oliveira Backend
    location /api/oliveira {
        proxy_pass http://oliveira_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Static files
    location / {
        root /usr/share/nginx/html;
        try_files $uri $uri/ =404;
    }
}
```

---

## Database Initialization (init-dbs.sql)

```sql
-- Create separate databases for each project
CREATE DATABASE alfabetizacao;
CREATE DATABASE viamoto;
CREATE DATABASE oliveira;

-- Create users with limited privileges
CREATE USER app_user WITH PASSWORD 'secure_password';
CREATE USER viamoto_user WITH PASSWORD 'secure_password';
CREATE USER oliveira_user WITH PASSWORD 'secure_password';

-- Grant privileges
GRANT ALL PRIVILEGES ON DATABASE alfabetizacao TO app_user;
GRANT ALL PRIVILEGES ON DATABASE viamoto TO viamoto_user;
GRANT ALL PRIVILEGES ON DATABASE oliveira TO oliveira_user;
```

---

## Deployment (on VPS)

### Step 1: SSH into VPS
```bash
ssh -i ~/.ssh/ofundefined-vps root@212.56.33.218
```

### Step 2: Set up project directories
```bash
cd /var/www
git clone https://github.com/ofundefined/alfabetizacao-app.git
git clone https://github.com/viamoto-is/monolith.git
git clone https://github.com/oliveiraenfermagem/monolith.git

# Or pull if already cloned
cd /var/www/alfabetizacao-app && git pull
```

### Step 3: Create docker-compose override for production
```bash
# Place at /var/www/docker-compose.yml
# Place SSL certs at /var/www/ssl/

# Create .env file with secrets
cat > /var/www/.env << 'EOF'
FIREBASE_CREDENTIALS='{"type":"service_account",...}'
SUPABASE_ANON_KEY='eyJ...'
EOF
```

### Step 4: Start services
```bash
cd /var/www
docker-compose up -d

# Check logs
docker-compose logs -f
```

### Step 5: Verify
```bash
curl -I https://alfabetizacao.ofundefined.com/api/alfabetizacao/health
```

---

## Scaling Later (If Needed)

If we need advanced features:

### Option 1: Traefik (recommended)
- Automatic SSL with Let's Encrypt
- Better load balancing
- Middleware (auth, rate limiting)
- Dashboard

```yaml
traefik:
  image: traefik:latest
  command:
    - "--api.dashboard=true"
    - "--providers.docker=true"
    - "--entrypoints.web.address=:80"
    - "--entrypoints.websecure.address=:443"
    - "--certificatesresolvers.letsencrypt.acme.tlschallenge=true"
    - "--certificatesresolvers.letsencrypt.acme.email=admin@ofundefined.com"
    - "--certificatesresolvers.letsencrypt.acme.storage=/traefik/acme.json"
  ports:
    - "80:80"
    - "443:443"
  volumes:
    - /var/run/docker.sock:/var/run/docker.sock:ro
    - ./traefik:/traefik
  networks:
    - shared_network
```

### Option 2: Kong (overkill for now, but possible)
- Full API gateway features
- Plugins (auth, rate limiting, request transformation)
- Admin API

---

## Monitoring & Logging

### Simple Approach (MVP)
```yaml
services:
  # App logs → stdout → docker-compose logs
  # nginx logs → /var/log/docker/ (mounted)
```

### Enhanced (Later)
```yaml
  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    networks:
      - shared_network

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    networks:
      - shared_network
```

---

## Backup Strategy

### Daily Database Backup
```bash
# /var/www/backup.sh
#!/bin/bash
docker-compose exec postgres pg_dump -U postgres alfabetizacao | gzip > /backups/alfabetizacao-$(date +%Y%m%d).sql.gz
docker-compose exec postgres pg_dump -U postgres viamoto | gzip > /backups/viamoto-$(date +%Y%m%d).sql.gz
```

Add to crontab:
```
0 2 * * * /var/www/backup.sh
```

---

## Disaster Recovery

```bash
# Restore from backup
gunzip < /backups/alfabetizacao-20260419.sql.gz | docker-compose exec -T postgres psql -U postgres -d alfabetizacao
```

---

## Cost Estimate

- Contabo VPS (6vCPU, 12GB RAM): $6.69/mo
- No additional costs for docker-compose + nginx
- If we migrate to Traefik: still $0 (open source)
- If we add monitoring (Prometheus, Grafana): ~$5–10/mo

**Total**: ~$7–16/mo

---

## Next Steps

1. **Prepare Dockerfiles**: Each project needs a Dockerfile
   - alfabetizacao-app: Node.js backend Dockerfile
   - viamoto: Laravel Dockerfile (or use existing)
   - oliveira: Node.js/monolith Dockerfile

2. **Test locally**: Run docker-compose on your machine first
3. **Deploy to VPS**: Follow steps above
4. **Monitor**: Watch logs for errors, crashes
5. **Scale if needed**: Migrate to Traefik if required

---

## FAQ

**Q: What if one service crashes?**
A: `restart: unless-stopped` auto-restarts. nginx continues serving other projects.

**Q: Can we run different versions of Node/Python?**
A: Yes, each container has its own runtime. Node 18 for app, Laravel 10 for viamoto, etc.

**Q: Do we need load balancing?**
A: No, single VPS is sufficient for MVP. If traffic spikes, migrate to Kubernetes later.

**Q: Is this secure?**
A: Yes, with proper SSL, firewall rules, and secret management (.env files, docker secrets for prod).
