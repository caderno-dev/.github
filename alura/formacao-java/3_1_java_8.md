# Java 8: Conheça as novidades dessa versão

## Default Methods

A partir do Java 8 foi criado um novo recurso que possibilita adicionar **métodos em interfaces com implementação**. Por exemplo, o código do método `sort` da interface `List`:

```
default void sort(Comparator<? super E> c) {
    Collections.sort(this, c);
}
```

Ou seja, é um método de interface que você não precisa implementar na sua classe se não quiser, pois você terá já essa implementação default. [Aqui estão os novos métodos default da interface List](http://docs.oracle.com/javase/8/docs/api/java/util/List.html).

Uma das grandes vantangens é poder evoluir um interface sem quebrar os códigos antigos.

### Como era feito a ordenação antes do Java 8

```
public class OrdenaString() {
    public static void main(String[] args) {
        List<String> palavras = Arrays.asList("felipe", "barbosa", "bomfim");

        // Ordenação padrão da classe String, pois ela implementa Comparable
        Collections.sort(palavras);

        // Se quiser ordenar de outra forma, tem que criar um comparador
        Collections.sort(palavras, new ComparadorDeStringPorTamanho());
    }
}

class ComparadorDeStringPorTamanho implements Comparator<String> {
    public int compare(String s1, String s2) {
        if (s1.length() < s2.length()) {
            return -1;
        }
        if (s1.length() > s2.length()) {
            return 1;
        }
        return 0;
    }
}

```

### foreach, Consumer e interfaces no java.util.functions

`forEach` um novo default method da interface `Iterable`. Ele recebe um `Consumer`, que é uma das muitas interfaces do novo pacote `java.util.functions`.

```
class ConsumidorDeString implements Consumer<String> {
    public void accept(String s) {
        System.out.println(s);
    }
}
```

Podemos passar no `forEach`:

```
palavras.forEach(new ConsumidorDeString());
```

## Que venha os lambdas!

Para quem está acostumado com Java (antes do 8), sabe que o método `forEach` do bloco anterior não precisa criar uma classe isolada só para consumir o `for`. Geralmente é criada **classes anônimas** diretamente no bloco do `for`, desta forma:

```
palavras.forEach(new Consumer<String>() {
    public void accept(String s) {
        System.out.println(s);
    }
});
```

Classes anônimas são usadas com frequência para implementar *listeners* e *callbacks* que não terão reaproveitamento.

Porém, classes anônimas produzem uma certa verbosidade na sintaxe e a partir do Java 8, existe uma nova forma de implementar essas interfaces ainda mais sucinta, atráves da **sintaxe do lambda**.

Em vez de escrever a classe anônima, deixamos de escrever alguns itens que podem ser inferidos. Como essa interface só tem um método, não precisamos escrever o nome do método. Também não daremos `new`. Apenas declaramos os argumentos e o bloco a ser executado, separados por `->`:

```
palavras.forEach((String s) -> {
    System.out.println(s);
});
```

Essa sintaxe funciona para qualquer interface que tenha **apenas um método abstrato**, e é por esse motivo que nem precisamos falar que estamos implementando o método `accept`, já que não há outra possibilidade.

Podemos também remover a declaração do tipo do parâmetro, que o compilador também infere:

```
palavras.forEach((s) -> {
    System.out.println(s);
});
```

Quando há apenas um parâmetro, nem mesmo os parenteses são necessários:

```
palavras.forEach(s -> {
    System.out.println(s);
});
```

E como só é uma única instrução, não precisamos das chaves e nem do ponto e vírgula:

```
palavras.forEach(s -> System.out.println(s));
```

Aplicando lambda no bloco do `Comparator`:

```
palavras.sort((s1, s2) -> Integer.compare(s1.length(), s2.length()));
```

> **Interface funcional** só pode conter um único método abstrato. Porém, além desse método, ela pode ter outros, contanto que sejam `default` ou `static`. Essa estrutura é fundamental, pois assim o compilador sabe exatamente que o corpo da expressão lambda que escrevemos é a implementação de seu único método abstrato.

### Threads com lambda

Antes: 

```
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Executando um Runnable");
    }
}).start();
```

com Lambda:

```
new Thread(() -> System.out.println("Executando um Runnable")).start();
```

## Código mais sucinto com Method references

Usando esse código de exemplo:

```
palavras.sort((s1, s2) -> Integer.compare(s1.length(), s2.length()));
```

### Métodos default em Comparator

Na interface `Comparator` existe um método default estático que se chama `comparing`, que é uma fábrica, uma factory, de `Comparator`. Passamos o lambda para dizer qual será o critério de comparação desse `Comparator`:

```
palavras.sort(Comparator.comparing(s -> s.length()));
```

Veja a expressividade da linha, está escritor algo como "palavras ordene comparando s.length".

Quebrando em duas linhas para ver o que esse novo método faz exatamente:

```
Comparator<String> comparador = Comparator.comparing(s -> s.length());
palavras.sort(comparador);
```

Dizemos que `Comparator.comparing` recebe um lambda, mas essa é uma expressão do dia a dia. Na verdade, ela recebe uma instância de uma interface funcional. No caso é a interface `Function` que tem apenas um método, o `apply`. Para utilizarmos o `Comparator.comparing`, nem precisamos ficar decorando os tipos e assinatura do método dessas interfaces funcionais. Essa é uma vantagem dos lambdas.

### Method reference

É muito comum escrevermos lambdas curtos, que simplesmente invocam um único método. É o exemplo de `s -> s.length()`. Dada uma `String`, invoque e retorne o método `length`. Por esse motivo, há uma forma de escrever esse tipo de lambda de uma forma ainda mais reduzida. Em vez de fazer:

```
palavras.sort(Comparator.comparing(s -> s.length()));
```

Fazemos uma referência ao método:

```
palavras.sort(Comparator.comparing(String::length));
```

São equivalentes nesse caso! Sim, é estranho ver `String::length` e dizer que é equivalente a um lambda, pois não há nem a `->` e nem os parênteses de invocação ao método. Por isso é chamado de method reference.

**Outro exemplo**

O `forEach` que recebe um `Consumer`:

```
palavras.forEach(s -> System.out.println(s));
```

Dada uma `String`, invoque o `System.out.println` passando-a como argumento. É possível usar method reference aqui também! Queremos invocar o `println` de `System.out`:

```
palavras.forEach(System.out::println);
```

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-collections)
- [Projeto final](https://github.com/alura-cursos/JavaCollections/archive/final.zip)

---

[Voltar](./README.md)
