# Seção 18: Módulo 3: Criando páginas de Sign In e Sign Out

[Repositório do projeto](https://github.com/caderno-dev/curso_udemy_react-avancado_client)

## Criando o template de Auth e rotas

Assim como foi feito para página `Home`, a estrutura de templates deixa o código mais organizado e fácil, parecido com a estrutura de componentes. Além disso, **é ideial** que na pasta `pages` fique somente as páginas sem os arquivos de estilos.

Para criar um template, basta executar o comando `yarn generate Auth` para criar com um componente mesmo. Porém, será necessário mover a pasta `Auth` de dentro de `components` para `templates` e remover o arquivo `stories.tsx`.

E para criar a página, basta criar um arquivo dentro de `pages`, no caso: `sign-in.tsx`. Vale lembrar que ao adicionar um arquivo dentro desta pasta, **automaticamente será criado uma rota** para esta página usando o próprio nome do arquivo.

```typescript
import Auth from 'templates/Auth'

export default function SignIn() {
  return <Auth />
}
```

E para ver rodando, basta executar `yarn dev`.

[Código alterado nesta aula](#) | [Vídeo da aula](https://www.udemy.com/course/react-avancado/learn/lecture/23018974)


---

[Voltar](./README.md)