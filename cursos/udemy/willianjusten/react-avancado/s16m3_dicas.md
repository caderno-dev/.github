# Seção 16: Módulo 3: Dicas rápidas de TS e nova variável de button

[Repositório do projeto](https://github.com/caderno-dev/curso_udemy_react-avancado_client)

## Usando const assertion para melhorar autocomplete

[`const` assertion](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions) é uma maneira de definir que uma variável pode ser considerada uma constante. Usando deste recurso, vamos usar para melhorar o autocomplete do editor nas variáveis utilizada no tema do projeto, desta forma:

[Código alterado nesta aula](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/d6b3936339da51878bf1058299f8f856f6e93eee) | [Vídeo da aula](https://www.udemy.com/course/react-avancado/learn/lecture/22774281)

## Criando um typecheck para testar o TS antes do next build

Em tempo de desenvolvimento, o Next não analisa sintaticamente os tipos (apesar do editor fazer isso para gente) e com isso, alguns erros podem acontecer quando rodar o `build`. Porém, o processo de build é lento e existe uma maneira de verificar isso antes do build através do comando:

```
tsc --project tsconfig.json --noEmit
```

Agora, você pode criar um script no `package.json`, desta forma:

[Código alterado nesta aula](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/b759b7228e04c7fc555d134e0d10a6c6ef571f8c)

## Criando uma variável minimal para o button

[Código alterado nesta aula](https://github.com/caderno-dev/curso_udemy_react-avancado_client/commit/cf8d99c4af18bcce592599efca33c20540235122)

---

[Voltar](./README.md)