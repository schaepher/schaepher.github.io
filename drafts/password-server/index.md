# password-server


密码服务器

```docker-compose
version: '3.3'
services:
    bitwarden:
        image: mprasil/bitwarden:latest
        container_name: bitwarden
        restart: always
        volumes:
        - ./data/bitwarden_rs/data:/data
        env_file:
        - config.env


    nginx:
        image: nginx
        ports:
            - '443:443'
            - '80:80'
        volumes:
            - ./nginx-conf.d:/etc/nginx/conf.d/
        links:
            - "bitwarden:bitwarden"
```

```env
SIGNUPS_ALLOWED=false
DOMAIN=xxxxx.com
DATABASE_URL=/data/bitwarden.db
ROCKET_WORKERS=10
WEB_VAULT_ENABLED=false
```
