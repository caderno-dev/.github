# Java Exceções: aprenda a criar, lançar e controlar exceções

## Pilha de execução

- A **pilha** ou *stack* existe para organizar a execução do código. 
- Todo programa em Java sempre começa no método `main()`.
- Através da pilha sabemos qual método está sendo executado (o que está no topo) e quais ainda precisam ser executados.

> Uma pilha Java faz parte da JVM e armazena os métodos que estão sendo executados. Além do bloco de código a pilha guarda as variáveis e as referências desse bloco. Assim a JVM organiza a execução e sabe exatamente qual método está sendo executado que é sempre o método no topo da pilha. A JVM também sabe quais outros precisam ser executados ainda, que são justamente os métodos abaixo.

## Tratamento de exceções

As exceções são problemas que acontecem na hora de compilar o código. Considerando que existe uma variedade imensa, elas possuem nomes explicativos e, às vezes, mostram claramente o motivo do seu surgimento, facilitando a identificação delas.

As exceções mudam o fluxo do código. Se soluções não forem encontradas dentro da pilha de execução, elas serão impressas no console.

### Try Catch

Para **tratarmos** uma exceção, é preciso sinalizar para a máquina virtual que isso pode acontecer, por meio de um código específico (`try`). Assim, ela entenderá que deve **tentar** executar esse código, entre chaves (`{}`) e com mais cautela. Caso algo dê errado, o bloco `catch` é acionado para tratar o problema. Por exemplo:

```java
try {
    int a = i / 0;
} catch (ArithmeticException e) {
    System.out.println("ArithmeticException);
}
```

### Multi-Catch

Podemos escrever mais de um catch desta forma:

```java
try {
    System.out.println(1/0);
} catch(ArithmeticException e) {
    e.printStackTrace();
} catch(NullPointerException e) {
    e.printStackTrack();
}
```

ou utilizando *pipes*:

```java
try {
    System.out.println(1/0);
} catch(ArithmeticException | NullPointerException e) {
    e.printStackTrace();
}
```

## Lançando exceções

- Para lançar uma exceção, além de instanciá-la, é necessário lançá-la através do `throw`. Exemplo: `throw new ArithmeticException();`.

- Quando a exceção é lançada, o código para de executar abruptamente.

## Checked e Unchecked 

### Hierarquia de exceções

![Hierarquia](./docs/1_4_hierarquia-error.png)

- Na hierarquia, objetos que fazer parte de qualquer classe que estenda `Throwable`, podem ser jogados na pilha (através da palavra reservada `throw`).
- `RuntimeException` herda de `Exception`, que por sua vez é filha da classe mais ancestral das exceções.
- Na classe `Throwable` temos praticamente todo o código relacionado às exceções, inclusive `getMessage()` e `printStackTrace()`. Todo o resto da hierarquia apenas possui algumas sobrecargas de construtores para comunicar mensagens específicas.
- A hierarquia iniciada com a class `Throwable` é dividida em **exceções** e **erros**.
    - **Exceções** são usadas em códigos de aplicação. 
    - **Erros** são usados exclusivamente pela máquina virtual.
- Classes que herdam de `Error` são usadas para comunicar erros na máquina virtual. Desenvolvedores de aplicação não devem criar erros que herdam de `Error`. Por exemplo, `StackOverflowError` é um erro da máquina virtual para informar que a pilha de execução não tem mais memória.

### Checked e Unchecked

Exceções são separadas em duas grandes categorias: aquelas que são obrigatoriamente verificadas pelo compilador e as que não são verificadas.

- *Checked*: é verificado pelo compilador. Somos obrigados a colocar `throws` na assinatura do método. São criadas do pertencimento a uma hierarquia que não passe por `RuntimeException`e sim direto de `Exception`, por exemplo.
- *Unchecked*: o compilador não dá muita importância. Se dermos `throws` ou não, ele não toma atitude, ou seja, ele não **verifica**. São criadas como descendente de `RuntimeException`.

Esse conceito de *checked* e *unchecked* é específico do mundo Java.

## Finally e try with resources

O bloco `finally` sempre será executado, independente se der erro ou não. Geralmente, usado para fechar conexões.

```java
Conexao conexao = null;
try {
    conexao = new Conexao();
    conexao.leDados();
} catch(IllegalStateException e) {
    System.out.println("Deu erro na conexão");
} finally {
    conexao.fecha();
}
```

### Try with resoruces

A partir do Java `1.7` é possível fazer uma simplicação para esses casos de fechamento de conexão, inicializando a variável dentro do `()` do `try`, desta forma:

```java
try (Conexao conexao = new Conexao()) {
    conexao.leDados();
}
```

Entretanto, para isso funcionar, a classe `Conexao` precisa implementar uma interface chamada `AutoCloseable`:

```java
public class Conexao implements AutoCloseable() {
    // ...

    @Override
    public void close() {
        // ...
    }
}
```

> Para implementar, você é obrigado a escrever o método `close()`.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-excecoes)
- [Projeto final](https://caelum-online-public.s3.amazonaws.com/834-java-excecoes/06/java4-projetos-finais.zip)

---

[Voltar](./README.md)
