# Java OO: Entendendo a Orientação a Objetos

[Página do curso](https://cursos.alura.com.br/course/java-introducao-orientacao-objetos)

## O problema do paradigma procedural

- Idéia central do paradigma OO: Dado e funcionalidade sobre ele andam juntos.

## Orientação a Objetos

- Classe: especificação de um tipo, definindo atributos e comportamentos.
- Objeto: é instância de uma classe onde pode definir valores para seus atributos. Para criar uma instância precisamos usar a palavra chave `new`.
- Atributos: características que especificam uma classe.
- Métodos: define o comportamento ou a maneira de fazer algo. Por convenção, o nome do método no mundo Java deve começar com letra minúscula (lowerCamelCase).

> `this` é palavra chave usada para referência ao objeto em si.

## Composição de objetos

- Realizar o relacionamento entre classes através de composição;
- Vantagens de se isolar informações repetidas em outra classe;

## Encapsulamento e visibilidade

- Encapsulamento: esconder o funcionamento de um atributo tornando o acesso à eles privados e disponibilizar o acesso através de métodos. Por exemplo: *getters* e *setters*.

> **Para saber mais: Cuidado com o Modelo Anêmico** 
> Uma classe com apenas *getters* e *setters* do atributos são conhecidas como classes fantoches ou `Value Objects`, ou seja, não possui responsabilidade alguma, a não ser carregar um punhado de atributos! **Definitivamente isso não é a Orientação a Objetos!**.

## Construtores e membros estáticos

- Construtor padrão: Não precisamos escrever esse código, o Java automaticamente insere;
- O construtor é executado apenas uma vez no momento em que construímos um objeto;
- O construtor nos oferece a possibilidade de inicializar alguns dados;
- O construtor padrão que o Java estipula caso não tenhamos escritos nenhum outro, deixa de existir;

- A palavra-chave `static` torna um atributo/método da classe, e não mais do objeto. **Os métodos estáticos acessam apenas atributos estáticos**.

- Você pode usar `this( )` para reaproveitamento de construtores.

---

[Voltar](./README.md)
