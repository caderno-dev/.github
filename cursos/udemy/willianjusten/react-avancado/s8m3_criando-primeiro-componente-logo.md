# Seção 8: Módulo 3: Criando primeiro componente Logo (SVG + React)

> [Repositório do projeto](https://github.com/caderno-dev/curso_udemy_react-avancado_client)


## Baixando do Figma, otimizando no SVGOMG e usando como componente

[SVGOMG](https://jakearchibald.github.io/svgomg/) é um site que otimiza seu SVG.

Com código do SVG em mãos, para criar o componente `Logo`, execute no terminal:

```
yarn generate Logo
```

> **Obs:** Isso só funciona devido ao [PLOP](./s2m1_boilerplate-nextjs.md#automatizando-criação-de-arquivos)

Agora basta colocar o SVG no arquivo `src/components/Logo/index.tsx`:

```JavaScript
import * as S from './styles'

const Logo = () => (
  <S.Wrapper>
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 158 48">
      //...código omitido
    </svg>
  </S.Wrapper>
)

export default Logo

```

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/ca00de6b4cf146bd4df79e39991c0656e6eb159a)

## Utilizando o currentColor do SVG e non null assertion do TS

O SVG tem uma propriedade chamada `currentColor` cuja sua função é simplesmente adotar a cor do componente pai, no caso, do `<S.Wrapper>`. Com isso, vamos alterar a cor de preenchimento do texto da logo para `currentColor`, desta forma:

```html
//...código omitido
<path fill="currentColor" d="...código omitido" />
//...código omitido
```

E como o objetivo é que a cor do logo seja de acordo com o tema escolhido, no `src/components/Logo/styles.ts` vamos importar o theme, desta forma:

```typescript
import styled, { css } from 'styled-components'

export const Wrapper = styled.div`
  ${({ theme }) => css`
    color: ${theme.colors.black};
  `}
`
```

Mas ainda não está dinâmico. Para isto, precisamos definir um *props* com as opções de cores possíveis, desta forma no arquivo `src/components/Logo/index.tsx`:

```typescript
import * as S from './styles'

export type LogoProps = {
  color?: 'white' | 'black'
}

const Logo = ({ color = 'white' }: LogoProps) => (
  <S.Wrapper color={color}>
// ...código omitido
```

Alguns detalhes no código acima:

- `color?` - O interrogação indica que essa propriedade é opcional.
- `{ color = 'white' }: LogoProps` - Aqui está passando um valor padrão para propriedade `color` caso ela não exista.

Agora no arquivo `src/components/Logo/style.ts` basta pegar a cor escolhida desta forma:

```typescript
import styled, { css } from 'styled-components'
import { LogoProps } from '.'

export const Wrapper = styled.div<LogoProps>`
  ${({ theme, color }) => css`
    color: ${theme.colors[color!]};
  `}
`
```

Onde:

- `styled.div<LogoProps>` - Está dizendo para o `div` usar as propriedades do `LogoProps`.
- `[color!]` - Como a propriedade `color` é opcional, é necessário fazer *non null assertion* passando `!`. Pois estamos garantindo que a propriedade sempre irá ser passada no `index.tsx`, pois lá já tem o valor default caso a propriedade não seja passada. Então, desta forma não precisamos preencher o valor default nos dois arquivos. Porém, o **eslint** não gosta disso, então é necessário desabilitar nas regras (`rules`) do arquivo `.eslintrc.json`, desta forma: `"@typescript-eslint/no-non-null-assertion": "off"`.

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/3a3c6b79b77cfda15dcbc19955738bffe65e96bd)

## Configurando args e controls no Storybook

Para que a funcionalidade [controls](https://storybook.js.org/docs/react/essentials/controls) passe a funcionar no Storybook, basta modificar o arquivo `src/components/Logo/stories.tsx`:

```typescript
import { StoryFn, Meta } from '@storybook/react'
import Logo, { LogoProps } from '.'

export default {
  title: 'Logo',
  component: Logo
} as Meta

export const Basic: StoryFn<LogoProps> = (args) => <Logo {...args} />
```

> **Obs:** O código está um pouco diferente do que foi passado na [aula](https://github.com/Won-Games/client/commit/841e5489b0530ebe59c8a74829789be347314e26) porque estou com uma versão mais nova do **Storybook**.

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/f06e9af4b050a869d27f50faf5ead40e58124f98)

## Criando um helper de testes renderWithTheme

Uma estrutura básica de testes de componentes segue mais ou menos essa linha:

- Renderiza o componente - `render`
- Seleciona o elemento a ser testado - `screen` (queries) - `getByLabel`, ...
- Faz a comparação - `except`, `assertion` (por exemplo, espero que rendereize a logo branca)

A biblioteca de testes utilizada é a [Testing Library](https://testing-library.com/docs/react-testing-library/intro/). Um [cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/) bem massa para ter e decorar os métodos. Mas também tem um [playground](https://testing-playground.com/) que te ajuda a encontrar o melhor testes para determinado elemento.

Como nos nossos testes alguns componentes dependem do tema escolhido, vamos criar um *helper* para encapsula o elemento dentro do  `<ThemeProvider>`, desta forma:

Crie o arquivo `src/utils/tests/helpers.tsx`

```typescript
import { ThemeProvider } from 'styled-components'
import { RenderResult, render } from '@testing-library/react'

import theme from 'styles/theme'

export const renderWithTheme = (children: React.ReactNode): RenderResult =>
  render(<ThemeProvider theme={theme}>{children}</ThemeProvider>)
```

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/c843714f7c4905e98b3001053844ec81bcd00e23)

## Criando primeiros testes

Pensando também em acessibilidade, vamos alterar nosso `<svg>` para que um leitor de tela para cegos descreva o conteúdo da imagem, desta forma:

```
<svg 
  xmlns="http://www.w3.org/2000/svg"
  fill="none"
  viewBox="0 0 158 48"
  role="img"
  aria-label="Won Games"
>
```

No arquivo `src/components/Logo/test.tst`, vamos fazer o seguintes testes:

```typescript
import { screen } from '@testing-library/react'
import { renderWithTheme } from 'utils/tests/helpers'

import Logo from '.'

describe('<Logo />', () => {
  it('should render a white label by default', () => {
    renderWithTheme(<Logo />)
    expect(screen.getByLabelText(/Won Games/i).parentElement).toHaveStyle({
      color: '#FAFAFA'
    })
  })

  it('should render a black label when color is passed', () => {
    renderWithTheme(<Logo color="black" />)
    expect(screen.getByLabelText(/Won Games/i).parentElement).toHaveStyle({
      color: '#030517'
    })
  })
})
```
> **Obs:** Por algum motivo será necessário adicionar uma configuração no Jest: `modulePaths: ['<rootDir>/src/', '<rootDir>/.jest']` para ele reconhecer o diretório do `helper`.

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/8201a21513cf16c367b3de4047dd11576a855365)

## Criando uma outra prop da logo usando o TDD

A ideia do TDD (Test Driven Development) é primeiro escrever o teste para depois fazer a implementação.

Seguindo essa linha, vamos escrever para os testes para verificar o tamanho do logo:

```typescript
// ...código omitido
  it('should render a normal logo when size is default', () => {
    renderWithTheme(<Logo />)
    expect(screen.getByLabelText(/Won Games/i).parentElement).toHaveStyle({
      width: '11rem'
    })
  })

  it('should render a bigger logo', () => {
    renderWithTheme(<Logo size="large" />)
    expect(screen.getByLabelText(/Won Games/i).parentElement).toHaveStyle({
      width: '20rem'
    })
  })
// ...código omitido
```

Como a propriedade `size` ainda não existe no componente, vamos adicioná-la:

```typescript
import * as S from './styles'

export type LogoProps = {
  color?: 'white' | 'black'
  size?: 'normal' | 'large'
}

const Logo = ({ color = 'white', size = 'normal' }: LogoProps) => (
  <S.Wrapper color={color} size={size}>

// ...código omitido
```

Por fim, precisamos adicionar ao estilo:

```typescript
import styled, { css } from 'styled-components'
import { LogoProps } from '.'

const wrapperModifiers = {
  normal: () => css`
    width: 11rem;
    height: 3.3rem;
  `,

  large: () => css`
    width: 20rem;
    height: 5.9rem;
  `
}

export const Wrapper = styled.div<LogoProps>`
  ${({ theme, color, size }) => css`
    color: ${theme.colors[color!]};

    ${!!size && wrapperModifiers[size]}
  `}
`
```

Alguns detalhes desta parte:

- Daria para fazer um `if` dentro da propriedade `css`, porém uma maneira mais elegante e legível é construindo `modifiers` (no caso, `wrapperModifiers`);
- Aí no `css` é só chamar como se fosse uma variável usando chaves;
- `!!size` está checando se a variável existe, os `!!` (dupla negação) é um hackzinho para checar se a variável existe e está dentro das opções esperadas, ou seja, se passar um valor que não esteja na lista de opções do size (normal ou large), a condição será falsa.

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/fb3cf01495faf6f43c523029ec33534b986766e4)

## Trabalhando com responsividade e testando media-queries

A ideia é esconder o escrito 'Won' do logo quando estiver no mobile. Para isto, primeiro será necessário instalar a biblioteca [styled-media-query](https://github.com/morajabi/styled-media-query) para trabalhar com media-queries.

```
yarn add styled-media-query
```

Vamos adicionar uma nova propriedade no `LogoProps` do arquivo `index.tsx`:

```typescript
import * as S from './styles'

export type LogoProps = {
  color?: 'white' | 'black'
  size?: 'normal' | 'large'
  hideOnMobile?: boolean
}

const Logo = ({
  color = 'white',
  size = 'normal',
  hideOnMobile = false
}: LogoProps) => (
  <S.Wrapper color={color} size={size} hideOnMobile={hideOnMobile}>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 158 48"
      role="img"
      aria-label="Won Games"
    >
      // ...código omitido
      <path
        className="text"
        fill="currentColor"
        d="..."
      />
 // ...código omitido
```

Um detalhe é adicionar a classe no path do svg para facilitar no css, desta forma `<path className="text"...` conforme código acima.

No arquivo `styles.ts`:

```typescript
import styled, { css } from 'styled-components'
import media from 'styled-media-query'

import { LogoProps } from '.'

const wrapperModifiers = {
  normal: () => css`
    width: 11rem;
    height: 3.3rem;
  `,

  large: () => css`
    width: 20rem;
    height: 5.9rem;
  `,

  hideOnMobile: () => css`
    ${media.lessThan('medium')`
      width: 5.8rem;
      height: 4.5rem;

      svg {
        height: 4.5rem;
        pointer-events: none;
      }

      .text {
        display: none;
      }
    `}
  `
}

export const Wrapper = styled.div<LogoProps>`
  ${({ theme, color, size, hideOnMobile }) => css`
    color: ${theme.colors[color!]};

    ${!!size && wrapperModifiers[size]}
    ${!!hideOnMobile && wrapperModifiers.hideOnMobile}
  `}
`
```

Por fim, vamos testar fazendo uso do `jest-styled-components`:

```typescript
  it('should render a bigger logo without text if hideOnMobile', () => {
    renderWithTheme(<Logo hideOnMobile />)
    expect(screen.getByLabelText(/Won Games/i).parentElement).toHaveStyleRule(
      'width',
      '5.8rem',
      {
        media: '(max-width: 768px)'
      }
    )
  })
```

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/e9292a20d12c1ec02f3b0e96fc3059fc15d9414f)

---

[Voltar](./README.md)