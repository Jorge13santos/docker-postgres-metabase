1. instalado o docker;

# curl -fsSL https://get.docker.com | bash
# docker info

2. instalado o docker-compose;

# curl -L "https://github.com/docker/compose/releases/download/1.27.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# chmod +x /usr/local/bin/docker-compose
# docker-compose --version

3. Subindo os container via docker-compose;

# mkdir /opt/Compose
# vim /opt/Compose/docker-compose.yaml
version: "3.8"
services:
   pgsql-metabase-docker:
    image: jorgeluiz/met-postgres-infra
    restart: always
    ports:
      - 5432:5432
    environment:
      POSTGRES_PASSWORD: postgres
      POSTGRES_USER: metabase
      POSTGRES_DB: metabase
    volumes:
      - /HOME/docker/volumes/postgres:/var/lib/postgresql/data
   metabase-docker:
     image: jorgeluiz/met-metabase
     restart: always
     ports:
       - 3002:3000
     volumes:
       - /HOME/docker/volumes/metabase-data:/metabase-data
     environment:
       MB_DB_TYPE: postgres
       MB_DB_DBNAME: metabase
       MB_DB_PORT: 5432
       MB_DB_USER: metabase
       MB_DB_PASS: postgres
       MB_DB_HOST: pgsql-metabase-docker
     depends_on:
       - pgsql-metabase-docker
     links:
       - pgsql-metabase-docke
 # docker-compose up -d
 # docker-compose ps
 # the end
