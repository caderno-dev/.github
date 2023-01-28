# Seção 3: Módulo 2: Iniciando com Strapi

## Strapi por debaixo dos panos

O [Strapi](https://strapi.io/) é um *headless CMS* que permite criar uma API de forma muito rápida sem estar atrelado a um front-end específico. 

O projeto é totalmente open source e seu [repositório](https://github.com/strapi/strapi) é *monorepo*, então ele utiliza o [Lerna](https://lerna.js.org/) para gerenciar isso. Sendo assim, todos os packages ficam no mesmo repositório (dentro da pasta `packages`), sendo o pacote `strapi` o principal deles. 

O pacote `strapi` utiliza várias dependências, mas as mais importantes são: 

- `koa`: Framework web em Node, desenvolvido pela mesma equipe do Express e é um framework mais robusto (que o Express) para aplicações mais complexas; 
- `node-fetch`
- `rimraf`: Especifíco para Windows, para conseguir apagar pastas;
- `dotenv`: Para trabalhar com variáveis de ambiente;

Outros pacotes importantes do Strapi: `strapi-database` e o `strapi-utils`.

## Requisitos para o Strapi

Segundo a [documentação](https://docs.strapi.io/developer-docs/latest/getting-started/introduction.html), você tem quatro opções para instalar o Strapi: via CLI, Docker, DigitalOcean One-Click e via Platform.sh One-Click.

## Comandos do PostgreSQL

No ambiente WSL, você tem duas opções de instalação do PostgreSQL:

### 1. Via diretamente no Ubuntu

Depois de [instalado](https://docs.microsoft.com/pt-br/windows/wsl/tutorials/wsl-database), você pode checar a versão através do comando `psql --version`.

Para iniciar, checar status e encerrar o serviço do Postgres os comandos são os seguintes:

```
sudo service postgresql start
sudo service postgresql status
sudo service postgresql stop
```

Para criar o usuário no banco: `sudo -u postgres createuser strapi`
Para criar o banco de dados: `sudo -u postgres createdb strapi`
Para entrar no terminal do Postgres: `sudo -u postgres psql`

No terminal do Postgress:

- `\du` - Lista usuários
- `\l` - Lista os bancos de dados
- `\q`- Sair

Criar senha e dar permissão ao usuário:

```
alter user strapi with encrypted password 'strapi123';
grant all privileges on database strapi to strapi;
```

### 2. Via Docker

Para criar uma image docker Postgres, execute o comando:

```
docker run --name strapi -e POSTGRES_PASSWORD=strapi123 -p 5432:5432 -d postgres
```

O usuário padrão é o *postgres*, então precisamos criar o usuário *strapi*, os passos são os mesmos que diretamente no sistema operacional, a diferença é que no Docker, provavelmente você precisará passar o host `-h 0.0.0.0`:

Para criar o usuário no banco: `sudo -u postgres createuser strapi -h 0.0.0.0`
Para criar o banco de dados: `sudo -u postgres createdb strapi -h 0.0.0.0`
Para entrar no terminal do Postgres: `sudo -u postgres psql -h 0.0.0.0`

No terminal do Postgress:

- `\du` - Lista usuários
- `\l` - Lista os bancos de dados
- `\q`- Sair

Criar senha e dar permissão ao usuário:

```
alter user strapi with encrypted password 'strapi123';
grant all privileges on database strapi to strapi;
```

## Iniciando o Strapi local (opção 1)

```
yarn create strapi-app reactavancado-api
```

## Iniciando o Strapi com Docker (opção 2)

Para iniciar o Strapi com Docker, basta seguir três passos:

- Criar um arquivo `docker-compose.yaml`
- Baixar as últimas imagens através do comando `docker-compose pull`
- Rodar a *stack* através do comando `docker-compose up`, opcionalmente pode-se usar o atributo `-d` (detached) para rodar em background no terminal.

> Extra: Instalando o [Docker no Windows com WSL](https://docs.docker.com/desktop/windows/wsl/)


## Importando e Exportando dados no PostgreSQL

Para checar status do banco:
```
sudo service postgresql status
```

Para exportar:

```
pg_dump -c --if-exists --exclude-table=strapi_administrator -h 127.0.0.1 -U strapi -d strapi -W > strapi.sql
```

Para importar:
```
pqsl -h 127.0.0.1 -U strapi -d strapi -W < strapi.sql
```

Onde:
- `-U`: usuário
- `-d`: banco de dados
- `-W`: solicita senha

---

[Voltar](./README.md)