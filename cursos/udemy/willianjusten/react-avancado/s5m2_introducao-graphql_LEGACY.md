# Seção 5: Módulo 2 (extra): Introdução ao GraphQL

Basicamente o GraphQL é dividido em duas partes:

- `queries`: usado para consultas. Semelhante ao método `GET`.
- `mutations`: usado para mudanças no banco. Tipo o método `POST`, `PUT`, `PATCH` e `DELETE`.

## Queries

Você pode iniciar uma `query` simplesmente abrindo chaves `{ ... }` ou pode dar nome à ela desta forma: 

```
query GET_AUTHORS { 
  ...
}
```

É meio que um padrão usar UPCASE com underline nos nomes da queries.

### Query parametrizada

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
```json
{
  "id": 4
}
``` 

### Alias

Você pode dar um apelido para qualquer atributo desta forma:

```
novoNome: nome_do_atributo
```

### Fragments

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

## Mutations

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

### Mutation parametrizada

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

```json
{
  "id": 4,
  "data": {
    "name": "Felipe"
  }
}
```

### Mutation para criar dados (createAuthor)

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

### Deletando dados com mutation

```
mutation DELETE_AUTHOR {
  deleteAuthor(input: { where: { id: 9 } }) {
    author { id }
  }
}
```

---

[Voltar](./README.md)