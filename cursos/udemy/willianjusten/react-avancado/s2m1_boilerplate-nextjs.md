# Seção 2: Módulo 1: Criando nosso Boilerplate do NextJS

## Configurando o TypeScript

```
touch tsconfig.json
yarn dev
yarn add --dev typescript @types/react @types/node
yarn dev
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/4672c416a9854f12494b85103e38ba2fb65f8414)

## Configurando o ESLint

```
npx eslint --init
yarn add eslint-plugin-react-hooks --dev
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/aed958c2e1dfcc92b73774cd2a263e8012f5ddad)

## Configurando o Prettier c/ Eslint

```
yarn add --dev --exact prettier
yarn add --dev eslint-plugin-prettier eslint-config-prettier
```

## Configurando um Git Hook c/ Husky e Lint-Staged (Opcional)

```
yarn add husky --dev
yarn husky init
yarn add lint-staged --dev
```


## Instalando e configurando o Jest com TypeScript

Site oficial do [Jest](https://jestjs.io/)

```
yarn add --dev jest @babel/preset-typescript @types/jest
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/221b3afef815a11a12d99ab9d061dacb1062f399)

## Instalando o React Testing Library e escrevendo os primeiros testes

Site oficial do [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)

```
yarn add --dev @testing-library/react @testing-library/jest-dom
```

Link para o [Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/)

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/df535fb30018ccd6abfa6fbac062bd750d133728)


## Instalando o Styled Components e configurando o SSR


```
yarn add --dev @types/styled-components babel-plugin-styled-components
yarn add styled-components
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/d5196a56ecce8df00070e45865263051207bd312)
- [Estilos globais](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/b69057460a52f1ab1865dc6ef1d9c4a5f5f0bc6e) 

## Melhorando snapshots com Jest-styled-components

```
yarn add --dev jest-styled-components
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/79fd3655633a34314289ebf9dd75ca911b144dce)

## Configurando o Storybook e escrevendo stories

[Storybook](https://storybook.js.org/) é uma ferramenta para testes de componentes de UI de forma isolada.

```
npx sb init
```

[Alterações feitas neste tópico.](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/cc232b04ae88b5b089aa6bf34505a1788a9e0cf1)
- [Storybook Essentials](https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate/commit/3d16b0612dfd56a555aec1064b15b3b2cc4fa508)

## Configurando o PWA

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

## Iniciando um projeto através do boilerplate

```
yarn create next-app -e https://github.com/felipebbarbosa/curso_udemy_react-avancado_boilerplate
```

## Automatizando criação de arquivos

Criando arquivos a partir de um template com [PLOP](https://plopjs.com/). Para instalá-lo:

```
yarn add -D plop
```

---

[Voltar](./README.md)