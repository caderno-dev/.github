# Java e java.lang: programe com a classe Object e String

## Organizando as classes com Pacotes

- **FQN (Full Qualified Name)** é o nome completo da classe, composto pelo nome do pacote e o nome da classe.
- Pacotes são diretórios com significado especial dentro do código fonte Java.
- A palavra chave `package` deve ser a primeira declaração no código fonte Java.
- *Packages* servem para organização e agrupar as classes e interfaces.
- Por organização e pela convenção adotada, precisamos seguir o domínio da empresa. Ou seja, se a empresa tem como domínio `alura.com.br`, os pacotes devem ser subpacotes de `br.com.alura`.
- Quando um projeto utiliza pacotes, podemos usar o `import` de outras classes para sua utilização.
- O modificador `default` do Java restringe acesso a nível de pacote. Logo, se não for definido algum modificador, seja na classe, método, ou atributo, apenas classes do mesmo pacote podem acessar essas informações.

## Todos os modificadores de acesso

- `public`: visível em todos os espaços.
- `protected`: visível dentro do pacote e público para os filhos.
- `<<package private>>` ou **default**: visível apenas dentro do pacote.
- `private`: visível apenas dentro da classe.

## Distribuição do seu código

### Javadoc

- É preciso ter instalado o JDK para poder gerar a documentação javadoc.
- O javadoc é uma documentação escrita pelo desenvolvedor para desenvolvedores.
- Existem tags especias para marcar o autor ou a versão da classe.

Exemplo:

```
/**
* javadoc aqui
*/
```

Todas as tags:
- `@author` (usado na classe ou interface)
- `@version` (usado na classe ou interface)
- `@param` (usado no método e construtor)
- `@return` (usado apenas no método)
- `@exception` ou `@throws` (no método ou construtor)
- `@see`
- `@since`
- `@serial`
- `@deprecated`

Importante é que as tags do javadoc existem apenas para padronizar alguns dados fundamentais do seu código fonte como o autor e a versão.

### Criando uma biblioteca com JAR

- JAR = Java Archive
- É o formato padrão do mundo Java para distribuir código compilado.
- É um arquivo compactado como ZIP.

## O pacote java.lang

- Possui classes essenciais para qualquer programa. Por exemplo, as classes String e System.
- Não precisa do `import`, é automaticamente importado.
- Um objeto do tipo `String` não pode ser alterado, são **imutáveis**. Isso significa que, uma vez criado, não pode ser alterado, por isso qualquer alteração cria um novo objeto `String`.

## A classe Object

- Qualquer objeto pode ser referenciado pelo tipo `Object`, já que ela é a principal. É a forma mais genérica de referenciar um objeto.
- Não é preciso deixar explícito na declaração de uma classe que ela deve herdar de `Object`, porque isso é automático. O compilador automaticamente insere a declaração.
- O método `toString()` existe para devolver uma informação sobre o estado do objeto.
- O método `toString()` existe para ser sobrescrito.


## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-pacotes-e-java-lang)

---

[Voltar](./README.md)
