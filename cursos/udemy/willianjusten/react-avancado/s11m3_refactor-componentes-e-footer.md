# Seção 11: Módulo 3: Ajustes/Refactor em componentes já existentes e Footer

> [Repositório do projeto](https://github.com/caderno-dev/curso_udemy_react-avancado_client)

## EXTRA: Definindo types para jest-styled-components

A biblioteca `jest-styled-components` já declarada globalmente no arquivo `.jest/setup.ts`, porém por uma falha ela não é reconhecida pelos tests, sendo necessário importá-la novamente dentro do arquivo de teste. Para resolver essa situação, temos que definir o types da biblioteca.

Como já existe um outro types, vamos organizá-los em uma pasta chamada `types`, desta forma:

> [Código alterado neste capítulo](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/9e1f9c7a33ae94a004fae4bfe569f88e15619f6f)

---

[Voltar](./README.md)