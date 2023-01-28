# Seção 9: Módulo 2: Criando a API para o E-commerce (Won Games)

## Inicializando o Strapi

Como a própria documentação do Strapi diz, é necessário ter o banco de dados rodando antes de tudo. No caso, **Postgres**!

No meu caso específico, estou o rodando o **Postgres** no **Docker** e acessando via **WSL**, então o comando para acessar é:

```bash
sudo -u postgres psql -h 0.0.0.0
```

E a senha: `strapi123`

Vamos criar o usuário no banco:

```sql
CREATE USER wongames WITH ENCRYPTED PASSWORD 'wongames123';
```

O resultado esperado no terminal é `CREATE ROLE`. Caso não mostre, tem alguma coisa errada.

Agora, vamos criar o banco de dados:

```sql
CREATE DATABASE wongames OWNER wongames;
```

Resultado esperado no terminal: `CREATE DATABASE`.

Saia do terminal do Postgres com `\q` e vamos criar o projeto Strapi!

```
yarn create strapi-app api
```

E as respostas das perguntas:

- Choose your installation type: `Custom (manual settings)`
- Choose your preferred language: `TypeScript`
- Choose your default database client: `postgres`
- Database name: `wongames`
- Host: `127.0.0.1`
- Port: `5432`
- Username: `wongames`
- Password: `wongames123`
- Enable SSL connection: `No`

Feito isso, entre no projeto criado `cd api` e rode o comando `yarn develop` para inicializá-lo.

Agora é necessário cadastrar um usuário. Segue os dados do usuário cadastrado:

- E-mail: `felipebbarbosa@gmail.com`
- Senha: `Wongames123`

## Criando as Collection Types

No Strapi Admin, `Content-Types Builder > Collection Type > Create new collection type`

### Categories

- Display name: `category`
- Fields:
  - `name` - Short text, Required, Unique
  - `slug` - UID, Required, Attached to `name`

### Platforms

- Display name: `platform`
- Fields:
  - `name` - Short text, Required, Unique
  - `slug` - UID, Required, Attached to `name`

### Developers

- Display name: `developer`
- Fields:
  - `name` - Short text, Required, Unique
  - `slug` - UID, Required, Attached to `name`

### Publishers

- Display name: `publisher`
- Fields:
  - `name` - Short text, Required, Unique
  - `slug` - UID, Required, Attached to `name`

### Games

- Display name: `game`
- Fields:
  - `name` - Short text, Required, Unique
  - `slug` - UID, Required, Attached to `name`
  - `short_description` - Long text, Required, Max. length = 160
  - `description` - Rich text, Required
  - `price` - Number, Number format = decimal, Required, Default value = 0
  - `release_date`, Date, Type = date
  - `rating` - Enumeration, Values = FREE, pegi3, pegi7, pegi12, pegi16, pegi18
  - `cover` - Media, Single media
  - `gallery` - Media, Multiple media

