# Docker Nginx SSL Proxy

This is a docker container to use nginx as a proxy 
to various other docker containers not visible to the public.

## Installation 

1) Clone the repository
```
git clone https://github.com/ground-creative/docker-wordpress.git {folder-name}
```

2) Create a docek network
```
docker network create nginx-proxy
```

3) Run docker-compose to build the proxy
```
docker-compose up -d --build
```

## Test Container Docker Compose File

This is an example container

```
version: '3'

services:
  nginx:
    image: nginx:alpine
    expose:
      - "80"
    environment:
      - VIRTUAL_HOST=test.carlodomain.com
      - VIRTUAL_PORT=80
      - LETSENCRYPT_HOST=test.carlodomain.com
      - LETSENCRYPT_EMAIL=irony00100@gmail.com
    volumes:
      - ./www/:/usr/share/nginx/html
    networks:
      - proxy
    restart: unless-stopped

networks:
  proxy:
    external:
      name: nginx-proxy
```