# Docker Nginx Proxy With SSL Layer

This is a docker container to use nginx as a proxy 
to various other docker containers not visible to the public.

## Installation 

1) Clone the repository
```
git clone https://github.com/ground-creative/docker-wordpress.git {folder-name}
```

2) Create a docker network
```
docker network create nginx-proxy
```

3) Run docker-compose to build the proxy
```
docker-compose up -d --build
```

## Example Container Docker Compose File

1) Create docker-compose.yml file and paste the following:
```
version: '3'

services:
  nginx:
    image: nginx:alpine
    expose:
      - "80"
    environment:
	  # change the host and email address values
      - VIRTUAL_HOST=somedomain.com
      - VIRTUAL_PORT=80
      - LETSENCRYPT_HOST=address@somedomain.com
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

2) Run docker-compose to build the container
```
docker-compose up -d --build
```

3) Access the container at the specified address in the VIRTUAL_HOST field

	(http|https)://{VIRTUAL_HOST}
