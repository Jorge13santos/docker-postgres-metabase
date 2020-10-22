#  instalado o docker;

### instalando o docker

    curl -fsSL https://get.docker.com | bash
    
### informação da versao do docker

    docker info

### instalado o docker-compose;

    curl -L "https://github.com/docker/compose/releases/download/1.27.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    
    chmod +x /usr/local/bin/docker-compose
    
    docker-compose --version
    
    mkdir -p compose/metadate
    
### editando o arquivo 

    vim compose/metadate/docker-compose.yaml
    
### subindo os serviços

    docker-compose up -d
    docker-compose ps



