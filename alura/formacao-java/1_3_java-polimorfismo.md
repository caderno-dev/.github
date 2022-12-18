# Java Polimorfismo: Entenda herança e interfaces

## Introdução a herança

- Na sintaxe da linguagem, a herança é expressada pela palavras `extends`. Por exemplo: 

```java
public class Gerente extends Funcionario { 
    ...
}
```

- Ao herdar, a classe filha ganha todas as características (atributos) e todas as funcionalidades (métodos) da classe mãe.

- Reutilização de código

## Super e reescrita de métodos

- Classe mãe ou classe pai, também é chamada de *base class* ou *super class*.

- A classe filha também é chamada de *sub class*.

- Modificadores de visibilidade:
    - `private` - Visível apenas dentro da própria classe.
    - `protected` - Visível dentro da classe e também para filhos, ou herdeiros.
    - `public` - Visível em todo lugar.

- Para acessar algo definido na classe mãe, usamos a palavra `super`. Por exemplo: `super.getNome()`.

## Entendendo Polimorfismo

- Polimorfismo é um objeto que pode ser referenciado por uma referência de mesmo tipo, ou genérica. Ou seja, se temos um objeto `Gerente()`, a referência pode ser tanto do tipo `Gerente` quanto do tipo `Funcionario`.

- Entretanto, **ao executarmos o código, sempre será chamado o método específico**.

- Objetos não mudam de tipo, a referência pode mudar.

- O uso de referências mais genéricas permite desacoplar sistemas.

## Herança e o uso construtores

- **Construtores não são herdados**. Os construtores pertencem somente à sua própria classe.

- Para chamar o construtor da classe pai no construtor da classe filha, usamos `super()`. O `super` significa que subimos na hierarquia.

- Utilizamos a anotação `@Override` em cima do método para avisar o compilador que a intenção é de sobrescrever o método, não é obrigatório para o funcionamento, mas desta forma, dá erro de compilação caso tenha algum erro de sintaxe.

## Classes e métodos abstratos

- A palavra `abstract` está **sempre** relacionada com herança.

- **Classes abstratas** não podem ser instanciadas. Para instanciar, devemos criar primeiro uma classe filha não abstrata. Uma classe abstrata representa um conceito, algo abstrato, e o compilador não permite instanciar um objeto dessa classe.

- Da mesma forma que existem classes abstratas, também existem métodos abstratos.

- Método abstrato, significa que ele não tem um corpo, ou seja, não foi implementado. Ele define apenas a assinatura (visibilidade, retorno, nome do método e parâmetros).

- Uma vez declarado o método abstrato, a classe filha precisa implementá-lo, senão não compila.

- Resumindo classes abstratas: 
    - Podem ter atributos: Uma classe abstrata é uma classe normal, só não pode instanciar e pode ter métodos abstratos. O resto continua valendo!
    - Podem ter métodos concretos (com implementação);
    - Podem ter métodos abstratos (sem implementação);
    - Não podem ser instanciadas.

## Interfaces

- No mundo Java não existe **herança múltipla**.

- Utilizando interfaces temos uma outra forma de conseguir polimorfismo sem herança.

- Interface é um contrato onde quem assina se responsabiliza por implementar esses métodos (cumprir contrato).

- Podemos estender apenas uma classe abstrata, mas podemos implementar várias interfaces.

- Todos os métodos de uma interface são abstratos.

- Para usar uma interface, usamos a palavra `implements` na assinatura da classe.

## Praticando herança e interfaces

- A herança captura o que é comum e isola aquilo que é diferente entre classes.

- Interface garante que todos os métodos de classes que implementam uma interface possam ser chamados com segurança.

- Com composições e interfaces teremos mais flexibilidade com nosso código, já que não nos prenderemos ao acoplamento que a herança propõe.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-heranca-interfaces-polimorfismo)
- [Projeto final](https://caelum-online-public.s3.amazonaws.com/788-java-heranca-interfaces-polimorfismo/07/java3-projeto-completo.zip)

---

[Voltar](./README.md)




