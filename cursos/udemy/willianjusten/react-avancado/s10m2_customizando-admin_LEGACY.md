# Seção 10: Módulo 2: Customizando o Admin do Strapi para a Won Games

- [Documentação de customização do Strapi](https://docs.strapi.io/developer-docs/latest/development/admin-customization.html#customization-options)

## Customizando a Logo da página de Login/Password/Register

No curso foi ensinado de uma maneira, mas quando assisti a aula já tinha sido atualizado a forma devido a atualização do próprio Strapi que simplificou esta parte. Pois agora basta modificar os logos pela própria interface do admin em `Settings > Overview > Customization`.

## Editando o favicon

Isto também está diferente do que foi apresentado no curso. Segundo a documentação, estes são os passos para alterar o favicon:

- Criar a pasta `./src/admin/extensions/` se ainda não existir.
- Subir o favicon nesta pasta.
- Substituir o arquivo de favicon da pasta raíz do Strapi.
- Atualizar o arquivo `./src/admin/app.js` desta forma:

```javascript
import favicon from './extensions/favicon.png';

export default {
  config: {
    // ...
    head: {
      favicon: favicon
    }
  }
}
```

Feito isso, execute o comando `yarn build && yarn develop` no terminal.

## Removendo o ícone de tutoriais

Coloque a chave `config.tutorials` para `false` no arquivo `./src/admin/app.js`.

---

[Voltar](./README.md)