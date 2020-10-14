1. instalado o docker;

# curl -fsSL https://get.docker.com | bash
# docker info

2. instalado o docker-compose;

# curl -L "https://github.com/docker/compose/releases/download/1.27.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# chmod +x /usr/local/bin/docker-compose
# docker-compose --version
# mkdir -p compose/metadate
# vim compose/metadate/docker-compose.yaml
insira o código
# docker-compose up -d
# docker-compose ps



