# Curso de React Avançado

Repositórios usados no curso:

- [Boilerplate](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate)

## Sumário

- [Seção 1: Módulo 1: Introdução Teórica](#seção-1-módulo-1-introdução-teórica)
- [Seção 2: Módulo 1: Criando nosso Boilerplate do NextJS](#seção-2-módulo-1-criando-nosso-boilerplate-do-nextjs)
- [Seção 3: Módulo 2: Iniciando com Strapi](#seção-3-módulo-2-iniciando-com-strapi)
- [Seção 5: Módulo 2 (extra): Introdução ao GraphQL](#seção-5-módulo-2-extra-introdução-ao-graphql)
- [Seção 6: Módulo 2 (extra): Trabalhando com GraphQL no Frontend](#seção-6-módulo-2-extra-trabalhando-com-graphql-no-frontend)

## Seção 1: Módulo 1: Introdução Teórica

### O que o NextJS tem/faz?

- Renderização no servidor (SSR);
- Geração de estáticos (SSG - Static Site Generation);
- CSS-in-JS (Styled-jsx, Styled Components);
- Zero config. (rotas, hot reloading, code splitting);
- Completamente extensível;
- Otimizado para produção.

### Quem usa?

Netflix, GitHub, Twitch, Uber e outros.

### Tipos de aplicação

- Static Site (SSG) - GatsbyJS, Hexo, Jekyll e NextJS
- Client Side Rendering (Single Page Application - SPA) - Create React App
- Server Side Rendering (SSR) - NextJS

### Vantagens / Desvantagens

#### Static Site Generation - SSG

Vantagens:
- Uso quase nulo do servidor;
- Pode ser servido numa CDN (melhor cache);
- Melhor performance de todos;
- Flexibilidade para usar qualquer servidor;

Desvantagens:
- Tempo de build pode ser muito alto;
- Dificuldade para escalar em apps grandes;
- Dificuldade para realizar atualizações constantes;

#### Single Page Application - SPA

Vantagens:
- Permite páginas ricas em interações sem recarregar;
- Site rápido após load inicial;
- Ótimo para apps web;
- Possui diversas bibliotecas;

Desvantagens:
- Load inicial pode ser muito grande;
- Performance imprevisível;
- Dificuldade no SEO;
- A maioria do conteúdo não é indexado;

#### Server Side Rendering - SSR

Vantagens:
- Ótimo em SEO;
- Meta tags com previews mais adequados;
- Melhor performance para o usuário (o conteúdo vai ser visto mais rápido);
- Código compartilhado com backend em Node;
- Menor processamento no lado do usuário;

Desvantagens:
- TTFB (Time to first byte) maior, o servidor vai preparar todo o conteúdo para entregar;
- HTML maior;
- Reload completo nas mudanças de rota*.

> O NextJS suporta os três tipos!

### Introdução ao GraphQL

Os GraphQL Clients são responsáveis por criar comandos de abstração para realizar queries/mutations, sistema de cache, validações e otimizações.

#### Fetch client x Caching client

Quais os clients mais conhecidos/utilizados?
- FetchQL
- GraphQL Request
- uRQL
- Relay Modern
- **Apollo Client** <--

### Introduação ao Strapi

O Strapi é um headless CMS open-source feito 100% em Javascript, totalmente customizável e orientado para devs preocupados em agilidade.

#### Vantagens do headless CMS

- Mesma entrega para diferentes tipos de dispositivos;
- Agnóstico de frameworks;
- Mais fácil na manutenção;
- Mais ágil para criação de protótipos;

#### Vantagens do Strapi

- 100% open-source;
- Altamente customizável (API e painel);
- Funciona com REST API ou GraphQL ao apertar de um botão;
- Self hosted (você controla seus dados e onde colocá-los);
- Roadmap bem definido e grande investimento;

#### Algumas features nativas do Strapi

- Suporte a múltiplos BD (SQLite, MongoDB, Postgres, MariaDB);
- Doc automática c/ plugin de one-click
- Integração a webhooks;
- Autenticações e permissões por padrão;
- Integração c/ diferentes serviços (Cloudinary, Algolia, Redis);
- Sistema de e-mails;
- Sistema de assets que otimiza imagens e cria em diferentes tamanhos

#### O que podemos fazer com Strapi

- Sites estáticos;
- Sites institucionais para empresas;
- Sites de notícias;
- E-commerce;
- O que você quiser!

#### Porque usar o Strapi

- Mais agilidade;
- Codebase toda em JS (+fácil manutenção);
- Sem mensalidade e controle do próprio dado (contentful, DatoCMS);

#### Como funciona o Strapi

- Possui 3 tiposde estruturas de dados:
  - Collection types (conjunto de dados padrão. Ex: Usuários, Produtos);
  - Single types (dado único. Ex: Homepage, footer, menu);
  - Component types (estrutura de dados reutilizadas. Ex: Galerias, Hero);

### CSS-in-JS

Bibliotecas: Aphrodite, Emotion, Glamour, **-> Styled Componentes <-** e Styled JSX.

#### Vantagens do Styled Components

- Critical CSS automático;
- Escopo definido (sem colisão de classes);
- Remoção de CSS não utilizado;
- Estilos dinâmicos (Props, Themes);
- Manutenção simplificada e sem dor;

### Introdução a Testes de Software

#### Tipos de teste

- Testes unitários
  - Testam isoladamente pequenas unidades de código;
  - O código está se comportando como o **dev** espera?
- Testes funcionais
  - Checa se as unidades funcionam também entre si;
  - Testes podem conter multiplas classes, métodos;
  - O programa funciona de acordo com que o **usuário** espera?

> TDD, Jest

## Seção 2: Módulo 1: Criando nosso Boilerplate do NextJS

### Configurando o TypeScript

```
touch tsconfig.json
yarn dev
yarn add --dev typescript @types/react @types/node
yarn dev
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/4672c416a9854f12494b85103e38ba2fb65f8414)

### Configurando o ESLint

```
npx eslint --init
yarn add eslint-plugin-react-hooks --dev
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/aed958c2e1dfcc92b73774cd2a263e8012f5ddad)

### Configurando o Prettier c/ Eslint

```
yarn add --dev --exact prettier
yarn add --dev eslint-plugin-prettier eslint-config-prettier
```

### Configurando um Git Hook c/ Husky e Lint-Staged (Opcional)

```
yarn add husky --dev
yarn husky init
yarn add lint-staged --dev
```


### Instalando e configurando o Jest com TypeScript

Site oficial do [Jest](https://jestjs.io/)

```
yarn add --dev jest @babel/preset-typescript @types/jest
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/221b3afef815a11a12d99ab9d061dacb1062f399)

### Instalando o React Testing Library e escrevendo os primeiros testes

Site oficial do [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

```
yarn add --dev @testing-library/react @testing-library/jest-dom
```

Link para o [Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/)

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/df535fb30018ccd6abfa6fbac062bd750d133728)


### Instalando o Styled Components e configurando o SSR


```
yarn add --dev @types/styled-components babel-plugin-styled-components
yarn add styled-components
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/d5196a56ecce8df00070e45865263051207bd312)
- [Estilos globais](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/b69057460a52f1ab1865dc6ef1d9c4a5f5f0bc6e) 

### Melhorando snapshots com Jest-styled-components

```
yarn add --dev jest-styled-components
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/79fd3655633a34314289ebf9dd75ca911b144dce)

### Configurando o Storybook e escrevendo stories

[Storybook](https://storybook.js.org/) é uma ferramenta para testes de componentes de UI de forma isolada.

```
npx sb init
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/cc232b04ae88b5b089aa6bf34505a1788a9e0cf1)
- [Storybook Essentials](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/3d16b0612dfd56a555aec1064b15b3b2cc4fa508)

### Configurando o PWA

Utilizamos o plugin [next-pwa](https://www.npmjs.com/package/next-pwa), para configurá-lo:

```
yarn add next-pwa
```
Para testar:

```
NODE_ENV=production yarn build
yarn start
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/e0670e5b76174516d255a9e1c73374e4cfc4ef69)

### Iniciando um projeto através do boilerplate

```
yarn create next-app -e https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate
```

### Automatizando criação de arquivos

Criando arquivos a partir de um template com [PLOP](https://plopjs.com/). Para instalá-lo:

```
yarn add -D plop
```

## Seção 3: Módulo 2: Iniciando com Strapi

### Strapi por debaixo dos panos

O [Strapi](https://strapi.io/) é um *headless CMS* que permite criar uma API de forma muito rápida sem estar atrelado a um front-end específico. 

O projeto é totalmente open source e seu [repositório](https://github.com/strapi/strapi) é *monorepo*, então ele utiliza o [Lerna](https://lerna.js.org/) para gerenciar isso. Sendo assim, todos os packages ficam no mesmo repositório (dentro da pasta `packages`), sendo o pacote `strapi` o principal deles. 

O pacote `strapi` utiliza várias dependências, mas as mais importantes são: 

- `koa`: Framework web em Node, desenvolvido pela mesma equipe do Express e é um framework mais robusto (que o Express) para aplicações mais complexas; 
- `node-fetch`
- `rimraf`: Especifíco para Windows, para conseguir apagar pastas;
- `dotenv`: Para trabalhar com variáveis de ambiente;

Outros pacotes importantes do Strapi: `strapi-database` e o `strapi-utils`.

### Requisitos para o Strapi

Segundo a [documentação](https://docs.strapi.io/developer-docs/latest/getting-started/introduction.html), você tem quatro opções para instalar o Strapi: via CLI, Docker, DigitalOcean One-Click e via Platform.sh One-Click.

### Comandos do PostgreSQL

No ambiente WSL, você tem duas opções de instalação do PostgreSQL:

#### 1. Via diretamente no Ubuntu

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

#### 2. Via Docker

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

### Iniciando o Strapi local (opção 1)

```
yarn create strapi-app reactavancado-api
```

### Iniciando o Strapi com Docker (opção 2)

Para iniciar o Strapi com Docker, basta seguir três passos:

- Criar um arquivo `docker-compose.yaml`
- Baixar as últimas imagens através do comando `docker-compose pull`
- Rodar a *stack* através do comando `docker-compose up`, opcionalmente pode-se usar o atributo `-d` (detached) para rodar em background no terminal.

> Extra: Instalando o [Docker no Windows com WSL](https://docs.docker.com/desktop/windows/wsl/)


### Importando e Exportando dados no PostgreSQL

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

## Seção 5: Módulo 2 (extra): Introdução ao GraphQL

Basicamente o GraphQL é dividido em duas partes:

- `queries`: usado para consultas. Semelhante ao método `GET`.
- `mutations`: usado para mudanças no banco. Tipo o método `POST`, `PUT`, `PATCH` e `DELETE`.

### Queries

Você pode iniciar uma `query` simplesmente abrindo chaves `{ ... }` ou pode dar nome à ela desta forma: 

```
query GET_AUTHORS { 
  ...
}
```

É meio que um padrão usar UPCASE com underline nos nomes da queries.

#### Query parametrizada

```
query GET_AUTHOR($id: ID!) {
  author (id: $id) {
    id
    name
  }
}
```

>**Obs.:** A "!" no tipo do parâmetro (ID!) obriga o usuário a preencher.

Aí na **QUERY VARIABLES** você terá que inputar os dados:
```
{
  "id": 4
}
``` 

#### Alias

Você pode dar um apelido para qualquer atributo desta forma:

```
novoNome: nome_do_atributo
```

#### Fragments

```
fragment imageData on UploadFile {
  alternativeText
  url
}

query GET_SOMETHING {
  photo: {
    ...imageData
  }
}
```

### Mutations

```
mutation UPDATE_AUTHOR {
  updateAuthor(
    input: {
      where: { id: 4 }
      data: { name: "Felipe" }
    }
  ) {
    author {
      name
    }
  }
}
```

#### Mutation parametrizada

```
mutation UPDATE_AUTHOR($id: ID!, $data: editAuthorInput) {
  updateAuthor(
    input: {
      where: { id: $id }
      data: $data
    }
  ) {
    author {
      name
    }
  }
}
```

Aí na **QUERY VARIABLES** você terá que inputar os dados:

```
{
  "id": 4,
  "data": {
    "name": "Felipe"
  }
}
```

#### Mutation para criar dados (createAuthor)

```
mutation CREATE_AUTHOR {
  createAuthor (
    input: {
      data: {
        name: "Novo autor"
        role: "Instrutor"
        description: "...."
      }
    }
  ) {
    author {
      name
      role
      description
    }
  }
}
```

#### Deletando dados com mutation

```
mutation DELETE_AUTHOR {
  deleteAuthor(input: { where: { id: 9 } }) {
    author { id }
  }
}
```

## Seção 6: Módulo 2 (extra): Trabalhando com GraphQL no Frontend

[Repositório da landing page para clonar](https://github.com/React-Avancado/landing-page).

Rode o comando `yarn install` para inicializar o projeto e `yarn dev` para executar.

### Criando o GraphQL Client

Foi o utilizado o [graphql-request](https://github.com/prisma-labs/graphql-request) como client, para instalá-lo:

```
yarn add graphql-request graphql
```

Crie a pasta `graphql` com o arquivo `client.ts` dentro da pasta `src`.

No arquivo `client.ts`:

```
import { GraphQLClient } from 'graphql-request'

const client = new GraphQLClient('http://localhost:1337/graphql')
export default client
```

### Criando a primeira query no Frontend

Para uma melhor organização, crie a pasta `queries` dentro da pasta `graphql` e depois crie o arquivo `getLandingPage.ts` da primeira query com seguinte conteúdo:

```
const GET_LANDING_PAGE = /* GraphQL */ `
  query GET_LANDING_PAGE {
    landingPage {
      logo {
        alternativeText
        url
      }
    }
  }
`

export default GET_LANDING_PAGE
```

### Fazendo o fetch dos primeiros dados (Data Fetching - getStaticProps)

Existem [algumas opções de *fetching*](https://nextjs.org/docs/basic-features/data-fetching/overview) no Next.js, mas as principais são duas: 

- `getStaticProps`: Como próprio nome diz, utilizado para sites SSG (Static Site Generation), ou seja, as propriedades serão pré-renderizadas ao subir a aplicação no servidor.
- `getServerSideProps`: Utilizado para aplicações SSR (Server-Side Rendering), ou seja, as propriedades serão processadas a cada requisição do usuário (buscando a informação em tempo real no servidor).

No caso da nossa aplicação, será utilizado o `getStaticProps`, desta forma no arquivo `src/pages/index.tsx`:

```
export const getStaticProps: GetStaticProps = async () => {
  const { landingPage } = await client.request(GET_LANDING_PAGE)

  return {
    props: {
      ...landingPage
    }
  }
}
```

### Criando Types para a API e mostrando primeiros dados em tela

Para passar os dados para o componente é necessário criar a *"tipagem"* dos dados. Crie uma pasta chamada `types` dentro do `src` com o arquivo `api.ts`:

```
export type LogoProps = {
  alternativeText: string
  url: string
}

export type LandingPageProps = {
  logo: LogoProps
}
```

No `pages/index.tsx` importe esses tipos: `import { LandingPageProps } from 'types/api'` e passe por parâmetro no componente `Index`: `const Index = ({ logo }: LandingPageProps) =>( ...` e depois pegue os dados do logo no componente correspondente, confira o [commit dessa etapa](https://github.com/felipebbarbosa/curso_udemy_react-avancado_landing-page/commit/03478f75ae1ecda7b1e20e2fcd290bbdea0a2c7a).

### Criando variáveis de ambiente

O [Next.js](https://nextjs.org/docs/basic-features/environment-variables) tem suporte para carregar variáveis de ambientes tanto do `.env.local` quanto do `process.env`. A diferença entre eles é a seguinte:

- `.env.local`: Geralmente só precisa de um por projeto e é utilizado para armazenar informações referentes à senha ou outro dado sigilo. Ele **deve ser adicionado** ao `.gitignore`. 

- `process.env`: É utilizado para atributos que variam de acordo com o ambiente, por exemplo, desenvolvimento e produção. Sendo assim, é necessário criar um arquivo para cada ambiente: `.env.development` e `.env.production`. Com isso, por padrão, quando executar o comando `next dev`, o arquivo `.env.development` será carregado. Se executar `next start`, o `.env.production` que será carregado.

Além disso, o **Next** tem um "truque" que permite a aplicação chamar uma variável de ambiente no lado do cliente (navegador) e para isso, basta colocar o prefixo `NEXT_PUBLIC_` no nome da variável.

E para utilizar as variáveis no código basta chamar `process.env.NOME_DA_VARIAVEL`.

Veja o [commit](https://github.com/felipebbarbosa/curso_udemy_react-avancado_landing-page/commit/fb17760d40f97fe724a39ea9889f03309e0b688f) das implementações feita em aula.


