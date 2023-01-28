# Seção 6: Módulo 2 (extra): Trabalhando com GraphQL no Frontend

[Repositório da landing page para clonar](https://github.com/React-Avancado/landing-page).

Rode o comando `yarn install` para inicializar o projeto e `yarn dev` para executar.

## Criando o GraphQL Client

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

## Criando a primeira query no Frontend

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

## Fazendo o fetch dos primeiros dados (Data Fetching - getStaticProps)

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

## Criando Types para a API e mostrando primeiros dados em tela

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

## Criando variáveis de ambiente

O [Next.js](https://nextjs.org/docs/basic-features/environment-variables) tem suporte para carregar variáveis de ambientes tanto do `.env.local` quanto do `process.env`. A diferença entre eles é a seguinte:

- `.env.local`: Geralmente só precisa de um por projeto e é utilizado para armazenar informações referentes à senha ou outro dado sigilo. Ele **deve ser adicionado** ao `.gitignore`. 

- `process.env`: É utilizado para atributos que variam de acordo com o ambiente, por exemplo, desenvolvimento e produção. Sendo assim, é necessário criar um arquivo para cada ambiente: `.env.development` e `.env.production`. Com isso, por padrão, quando executar o comando `next dev`, o arquivo `.env.development` será carregado. Se executar `next start`, o `.env.production` que será carregado.

Além disso, o **Next** tem um "truque" que permite a aplicação chamar uma variável de ambiente no lado do cliente (navegador) e para isso, basta colocar o prefixo `NEXT_PUBLIC_` no nome da variável.

E para utilizar as variáveis no código basta chamar `process.env.NOME_DA_VARIAVEL`.

Veja o [commit](https://github.com/felipebbarbosa/curso_udemy_react-avancado_landing-page/commit/fb17760d40f97fe724a39ea9889f03309e0b688f) das implementações feita em aula.

---

[Voltar](./README.md)
