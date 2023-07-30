# Seção 13: Módulo 3: Iniciando o projeto da Won e criando primeiros fundações

> [Repositório do projeto](https://github.com/caderno-dev/curso_udemy_react-avancado_client)


## Iniciando o projeto através do Boilerplate

```bash
yarn create next-app -e https://github.com/caderno-dev/curso_udemy_react-avancado_boilerplate client
```

Onde:

- `-e <link>`: Flag que diz que é apartir de um exemplo do link do repositório especificado.
- `client`: É o nome do novo projeto gerado apartir do exemplo.


## Utilizando Web Fonts no Next e detalhes

Existem algumas maneiras de carregar uma fonte no seu projeto, seja utilizando um CDN e importando via HTML ou diretamente no CSS; Ou fazendo download da fonte e adicionando no seu código. Essa segunda opção é melhor para no casos de PWA, por exemplo.

> Um ótimo [artigo](https://www.zachleat.com/web/comprehensive-webfonts/) sobre as melhores estratégias de carregamento de fontes

Para facilitar o trabalho caso siga pela segunda opção, o site [google-webfonts-helper](https://gwfh.mranftl.com/fonts) é uma ótima ferramenta de auxilio.

Neste site, você tem a opção de querer atender todos os browsers ou se pretente atender somente os modernos. Aí basta fazer o download, colocar as fontes em `public\fonts` e colocar o código sugerido no arquivo `src\styles\global.ts`, desta forma:

```typescript
import { createGlobalStyle } from 'styled-components'

const GlobalStyles = createGlobalStyle`
  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 100;
    src: url('/fonts/poppins-v20-latin-100.woff2') format('woff2');
  }

  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 400;
    src: url('/fonts/poppins-v20-latin-regular.woff2') format('woff2');
  }

  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 600;
    src: url('/fonts/poppins-v20-latin-600.woff2') format('woff2');
  }


  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    font-size: 62.5%;
  }

  html, body, #__next {
    height: 100%;
  }

  body {
    font-family: 'Poppins', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif
  }
`

export default GlobalStyles
```

### font-display: swap

Uma outra configuração para cada `@font-face` é adicionar a propriedade `font-display: swap;`, isso informa ao browser que pode carregar uma fonte padrão enquanto está carregando a página e troque para fonte de desajada quando o carregamento estiver completo. Por padrão, sem opção, o browser não carrega texto nenhum enquanto a fonte não tiver sido totalmente carregada.

### Corrigindo problema de Antialising

No seletor global de CSS, adicione as seguintes propriedades: 

```css
* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## Criando o theme.ts (colors, spacings, layers, etc)

Este arquivo ficará em `src/styles/theme.ts` com o seguinte conteúdo:

```typescript
export default {
  grid: {
    container: '130rem',
    gutter: '3.2rem'
  },
  border: {
    radius: '0.4rem'
  },
  font: {
    family:
      "Poppins, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif",
    light: 300,
    normal: 400,
    bold: 600,
    sizes: {
      xsmall: '1.2rem',
      small: '1.4rem',
      medium: '1.6rem',
      large: '1.8rem',
      xlarge: '2.0rem',
      xxlarge: '2.8rem'
    }
  },
  colors: {
    primary: '#F231A5',
    secondary: '#3CD3C1',
    mainBg: '#06092B',
    white: '#FAFAFA',
    black: '#030517',
    lightGray: '#EAEAEA',
    gray: '#8F8F8F',
    darkGray: '#2E2F42'
  },
  spacings: {
    xxsmall: '0.8rem',
    xsmall: '1.6rem',
    small: '2.4rem',
    medium: '3.2rem',
    large: '4.0rem',
    xlarge: '4.8rem',
    xxlarge: '5.6rem'
  },
  layers: {
    base: 10,
    menu: 20,
    overlay: 30,
    modal: 40,
    alwaysOnTop: 50
  }
}
```

## Configurando ThemeProvider e suporte do TypeScript com declaration file

Para o utilizar o tema (`theme.ts`) criado no tópico anterior com o **Styled Components** é preciso usar o **ThemeProvider** ([documentação](https://styled-components.com/docs/api#themeprovider)), que é um *component helper* que injeta os estilos em todos componentes.

Ele precisa ficar na camada mais externa da aplicação, no caso do **Next.js**, essa camada fica no arquivo `.src/pages/_app.tsx` ([documentação](https://nextjs.org/docs/pages/building-your-application/routing/custom-app)), desta forma:

```TypeScript
import { AppProps } from 'next/app'
import Head from 'next/head'
import { ThemeProvider } from 'styled-components'

import GlobalStyles from 'styles/global'
import theme from 'styles/theme'

function App({ Component, pageProps }: AppProps) {
  return (
    <ThemeProvider theme={theme}>
      <Head>
        <title>React Avançado - Boilerplate</title>
        <link rel="shortcut icon" href="/img/icon-512.png" />
        <link rel="apple-touch-icon" href="/img/icon-512.png" />
        <link rel="manifest" href="/manifest.json" />
        <meta
          name="description"
          content="A simple project starter to work with TypeScript, React, NextJS and Styled Components"
        />
      </Head>
      <GlobalStyles />
      <Component {...pageProps} />
    </ThemeProvider>
  )
}

export default App
```

Com isso, as informações do tema são injetadas para todos os componentes, inclusive para o `GlobalStyles`, assim é possível alterar algumas informações do estilo global para pegar direto do tema, desta forma no arquivo `src/styles/global.ts`:

```TypeScript
import { createGlobalStyle, css } from 'styled-components'

const GlobalStyles = createGlobalStyle`
  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 100;
    font-display: swap;
    src: url('/fonts/poppins-v20-latin-100.woff2') format('woff2');
  }

  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 400;
    font-display: swap;
    src: url('/fonts/poppins-v20-latin-regular.woff2') format('woff2');
  }

  @font-face {
    font-display: swap; /* Check https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display for other options. */
    font-family: 'Poppins';
    font-style: normal;
    font-weight: 600;
    font-display: swap;
    src: url('/fonts/poppins-v20-latin-600.woff2') format('woff2');
  }


  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  ${({ theme }) => css`
    html {
      font-size: 62.5%;
    }

    body {
      font-family: ${theme.font.family};
      font-size: ${theme.font.sizes.medium};
    }
  `}
`

export default GlobalStyles
```

É necessário importar o componente `css` do **Styled Component**, porém para fazer isso funcionar é necessário criar o `DefaultTheme` através do [*declaration file*](https://styled-components.com/docs/api#create-a-declarations-file).

E como tema padrão, vamos usar o conteúdo do `theme.ts`. Sendo assim, para o Styled Component entender isso, vamos criar um arquivo chamado `styled-components.d.ts` (`.d` simboliza arquivo de declaração) na raíz do projeto, com o seguinte conteúdo:

```TypeScript
import theme from 'styles/theme'

// inferência de tipos
type Theme = typeof theme

declare module 'styled-components' {
  // eslint-disable-next-line @typescript-eslint/no-empty-interface
  export interface DefaultTheme extends Theme {}
}
```

Desta forma, o **Styled Components** irá fazer um *merge* do conteúdo dele com o tema que criamos. É para isso que serve o arquivo de declaração (*declaration file*).

O comentário `// eslint-disable-next-line @typescript-eslint/no-empty-interface` serve para o Eslint desabilitar o erro, pois não é correto criar uma `interface` vazia. Mas neste caso faz sentido.

### Corrigindo o Storybook

Com as alterações feitas anteriormente, se você rodar o Storybook com o comando `yarn storybook`, irá ocorrer o seguinte erro:

```
Error: Cannot read properties of undefined (reading 'font')
```

Isso que o Storybook não está lendo o arquivo `_app.tsx`, então ele não tem o `ThemeProvider`, para corrigir isso basta alterar o arquivo `.storybook/preview.js` para chamar o `ThemeProvider`, desta forma:

```javascript
import { ThemeProvider } from 'styled-components'
import GlobalStyles from '../src/styles/global'
import theme from '../src/styles/theme'

export const decorators = [
  (Story) => (
    <ThemeProvider theme={theme}>
      <GlobalStyles />
      <Story />
    </ThemeProvider>
  )
]
// ...código omitido
```

## Configurando webpack do Storybook para absolute path

No arquivo `.storybook/main.js`, você consegue customizar algumas [configurações do webpack](https://storybook.js.org/docs/react/builders/webpack#extending-storybooks-webpack-config) através do atributo `webpackFinal`, desta forma:

```javascript
module.exports = {
  stories: ["../src/components/**/stories.@(js|jsx|ts|tsx)"],
  addons: ["@storybook/addon-essentials"],
  //...código omitido
  webpackFinal: (config) => {
    config.resolve.modules.push(`${process.cwd()}/src`)
    return config
  }
};
```

Onde `${process.cwd()}` pega o diretório raíz do projeto.

Com isso, agora no arquivo `.storybook/preview.js` não precisa mais passar o `../src/` para importar os módulos.

```javascript
import { ThemeProvider } from 'styled-components'
import GlobalStyles from 'styles/global'
import theme from 'styles/theme'

// ...código omitido
```

---

[Voltar](./README.md)