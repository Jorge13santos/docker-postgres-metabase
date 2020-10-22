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

### vim compose/metadate/docker-compose.yaml

# ... or docker-compose.yaml
    
    version: "3.7"
    # Declaração dos serviços.
services:
    # Configuração do container do Postgres.
  pgsql-metabase-docker:
    # Nome da imagem a ser buscada.
    image: postgres
    # Permite escolher reiniciar caso o serviço pare.
    restart: always
    # Especificação do expose das portas.
    ports:
      - 5432:5432
    # Criação das váriaveis de ambiente.
    environment:
      # Senha para o banco.
      POSTGRES_PASSWORD: postgres
      # Usuário
      POSTGRES_USER: metabase
      #Nome do Banco
      POSTGRES_DB: metabase
    # Indicação do diretório para volume.  
    volumes:
      # Use um diretório que já esteja criado.
      - /HOME/docker/volumes/postgres:/var/lib/postgresql/data

 ### Configuração do container do Metabase.
  metabase-docker:
    # Nome da imagem a ser buscada.
    image: metabase/metabase
    # Permite escolher reiniciar caso o serviço pare.
    restart: always
    # Especificação do expose das portas.
    ports:
      - 3002:3000
    # Indicação do diretório para volume.  
    volumes:
    # Use um diretório que já esteja criado.
      - /HOME/docker/volumes/metabase-data:/metabase-data
    # Criação das váriaveis de ambiente.
    environment:
      # Nome do tipo de Banco.
      MB_DB_TYPE: postgres   
      # Nome do Banco.
      MB_DB_DBNAME: metabase  
      # Porta de Conexão.
      MB_DB_PORT: 5432  
      #  Nome do Usuário a se conectar no Banco.
      MB_DB_USER: metabase  
      # Nome da senha do Usuário.
      MB_DB_PASS: postgres  
      # Nome do Host de conexão.
      MB_DB_HOST: pgsql-metabase-docker 
    # Especificação de dependência.  
    depends_on:
      - pgsql-metabase-docker
    # Especificação do contianer a ser linkado.  
    links:
      - pgsql-metabase-docker
    
    
### subindo os serviços

    docker-compose up -d
    docker-compose ps



