# Seção 1: Módulo 1: Introdução Teórica

## O que o NextJS tem/faz?

- Renderização no servidor (SSR);
- Geração de estáticos (SSG - Static Site Generation);
- CSS-in-JS (Styled-jsx, Styled Components);
- Zero config. (rotas, hot reloading, code splitting);
- Completamente extensível;
- Otimizado para produção.

## Quem usa?

Netflix, GitHub, Twitch, Uber e outros.

## Tipos de aplicação

- Static Site (SSG) - GatsbyJS, Hexo, Jekyll e NextJS
- Client Side Rendering (Single Page Application - SPA) - Create React App
- Server Side Rendering (SSR) - NextJS

## Vantagens / Desvantagens

### Static Site Generation - SSG

Vantagens:
- Uso quase nulo do servidor;
- Pode ser servido numa CDN (melhor cache);
- Melhor performance de todos;
- Flexibilidade para usar qualquer servidor;

Desvantagens:
- Tempo de build pode ser muito alto;
- Dificuldade para escalar em apps grandes;
- Dificuldade para realizar atualizações constantes;

### Single Page Application - SPA

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

### Server Side Rendering - SSR

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

## Introdução ao GraphQL

Os GraphQL Clients são responsáveis por criar comandos de abstração para realizar queries/mutations, sistema de cache, validações e otimizações.

## Fetch client x Caching client

Quais os clients mais conhecidos/utilizados?
- FetchQL
- GraphQL Request
- uRQL
- Relay Modern
- **Apollo Client** <--

## Introduação ao Strapi

O Strapi é um headless CMS open-source feito 100% em Javascript, totalmente customizável e orientado para devs preocupados em agilidade.

### Vantagens do headless CMS

- Mesma entrega para diferentes tipos de dispositivos;
- Agnóstico de frameworks;
- Mais fácil na manutenção;
- Mais ágil para criação de protótipos;

### Vantagens do Strapi

- 100% open-source;
- Altamente customizável (API e painel);
- Funciona com REST API ou GraphQL ao apertar de um botão;
- Self hosted (você controla seus dados e onde colocá-los);
- Roadmap bem definido e grande investimento;

### Algumas features nativas do Strapi

- Suporte a múltiplos BD (SQLite, MongoDB, Postgres, MariaDB);
- Doc automática c/ plugin de one-click
- Integração a webhooks;
- Autenticações e permissões por padrão;
- Integração c/ diferentes serviços (Cloudinary, Algolia, Redis);
- Sistema de e-mails;
- Sistema de assets que otimiza imagens e cria em diferentes tamanhos

### O que podemos fazer com Strapi

- Sites estáticos;
- Sites institucionais para empresas;
- Sites de notícias;
- E-commerce;
- O que você quiser!

### Porque usar o Strapi

- Mais agilidade;
- Codebase toda em JS (+fácil manutenção);
- Sem mensalidade e controle do próprio dado (contentful, DatoCMS);

### Como funciona o Strapi

- Possui 3 tiposde estruturas de dados:
  - Collection types (conjunto de dados padrão. Ex: Usuários, Produtos);
  - Single types (dado único. Ex: Homepage, footer, menu);
  - Component types (estrutura de dados reutilizadas. Ex: Galerias, Hero);

## CSS-in-JS

Bibliotecas: Aphrodite, Emotion, Glamour, **-> Styled Componentes <-** e Styled JSX.

### Vantagens do Styled Components

- Critical CSS automático;
- Escopo definido (sem colisão de classes);
- Remoção de CSS não utilizado;
- Estilos dinâmicos (Props, Themes);
- Manutenção simplificada e sem dor;

## Introdução a Testes de Software

### Tipos de teste

- Testes unitários
  - Testam isoladamente pequenas unidades de código;
  - O código está se comportando como o **dev** espera?
- Testes funcionais
  - Checa se as unidades funcionam também entre si;
  - Testes podem conter multiplas classes, métodos;
  - O programa funciona de acordo com que o **usuário** espera?

> TDD, Jest

---

[Voltar](./README.md)