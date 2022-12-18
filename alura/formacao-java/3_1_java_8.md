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

## Streams: trabalhando melhor com coleções

No Java 8 é possível, por exemplo, filtrar listas de forma interessante usando a interface [Stream](http://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html). Porém, filtrar é só um dos métodos possíveis com `Stream` e para pegar um, você pode invocar através de um coleção, por exemplo: `cursos.stream()` e para filtrar os cursos que tem mais de 100 alunos:

```
cursos.stream().filter(c -> c.getAlunos() > 100);
```

O filtro também devolve um `Stream`! É um exemplo do que chamam de `fluent interface`.

Detalhe: as **modificações em um stream não modificam a coleção/objeto que o gerou**. Tudo que é feito nesse fluxo de objetos, nesse `Stream`, não impacta, não tem efeitos colaterais na coleção original.

Outro método interessante é o `map()`, que podemos por exemplo, pegar só a quantidade de alunos por curso, desta forma:

```
cursos.stream()
    .filter(c -> c.getAlunos() > 100)
    .map(Curso::getAlunos);
```

Esse `map` irá retornar um `Stream<Integer>`.

### Streams primitivos

Há um cuidado a ser tomado: com os tipos primitivos. Quando fizemos o `map(Curso::getAlunos)`, recebemos de volta um `Stream<Integer>`, que acaba fazendo o autoboxing dos `int`s. Isto é, utilizará mais recursos da JVM. Claro que, se sua coleção é pequena, o impacto será irrisório. Mas é possível trabalhar só com `int`s, invocando o método `mapToInt`:

```
IntStream stream = cursos.stream()
   .filter(c -> c.getAlunos() > 100)
   .mapToInt(Curso::getAlunos);
```

Ele devolve um `IntStream`, que não vai gerar autoboxing e possui novos métodos específicos para trabalhar com inteiros. Um exemplo? A soma:

```
int soma = cursos.stream()
   .filter(c -> c.getAlunos() > 100)
   .mapToInt(Curso::getAlunos)
   .sum()
```

### Optional

[Optional](http://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) é uma importante nova classe do Java 8. É com ele que poderemos trabalhar de uma maneira mais organizada com possíveis valores `null`. Em vez de ficar comparando `if (algumaCoisa == null)`, o `Optional` já fornece uma série de métodos para nos ajudar nessas situações. Por exemplo, o `findAny()` do Stream retorna um `Optional` e podemos utilizar o método `ifPresent` para exibir o nome, assim: 

```
cursos.stream()
   .filter(c -> c.getAlunos() > 100)
   .findAny()
   .ifPresent(c -> System.out.println(c.getNome()));
```

### Gerando uma coleção a partir de um Stream

Invocar métodos no `stream` de uma coleção não altera o conteúdo da coleção original. Ele não gera efeitos colaterais. Porém, para gerar uma nova coleção a partir de um `stream`, utilizamos o método `collect`.

O método `collect` recebe um `Collector`, uma interface não tão trivial de se implementar. Podemos usar a classe `Collectors`, cheio de *factory methods* que ajudam na criação de coletores. Um dos coletores mais utilizados é o retornado por `Collectors.toList()`:

```
List<Curso> resultados = cursos.stream()
   .filter(c -> c.getAlunos() > 100)
   .collect(Collectors.toList());
```

Podemos gerar mapas também. Por exemplo, um mapa que, dado o nome do curso, o valor atrelado é a quantidade de alunos. Um `Map<String, Integer>`. Utilizamos o `Collectors.toMap`. Ele recebe duas `Functions`. A primeira indica o que vai ser a chave, e a segunda o que será o valor:

```
Map mapa = cursos 
.stream() 
.filter(c -> c.getAlunos() > 100) 
.collect(Collectors.toMap(c -> c.getNome(), c -> c.getAlunos())); 
```

### Outras vantagens do Stream

Os Streams foram desenhados de uma forma a tirar proveito da programação funcional. Se você utilizá-los das formas acima, eles nunca gerarão efeitos colaterais. Isso é, apenas o stream será alterado, e nenhum outro objeto será impactado.

Dada essa premissa, podemos pedir para que nosso `stream` seja processado em paralelo. Ele mesmo vai decidir quantas threads usar e fazer todo o trabalho, utilizando APIs mais complicadas (como a de fork join) para ganhar performance. Para fazer isso, basta utilizar `parallelStream()` em vez de `stream()`!

Tome cuidado. Para streams pequenos, o custo de cuidado dessas threads e manipular os dados entre elas é alto e pode ser bem mais lento que o `Stream` tradicional.

## A nova API de datas

Para representar uma data em Java nessa nova API utilizamos a classe `LocalDate`, presente no pacote `java.time`.

```
LocalDate hoje = LocalDate.now();
```

Atráves do método `of` podemos definir uma data:

```
LocalDate evento = LocalDate.of(2023, Month.JUNE, 5);
```

### Trabalhando com Period

Para saber a diferença entre duas datas podemos utilizar o método `between` da classe `Period`:

```
Period periodo = Period.between(hoje, evento);
System.out.println(periodo);
```

### Uma API imutável

Toda a API de datas é imutável. Ela nunca vai alterar a data original (ao contrário do `Calendar`).

### Formatando suas datas

Para formatar nossas datas podemos utilizar o `DateTimeFormatter`. Existem diversos já prontos, mas há ainda a alternativa de você criar o seu próprio formatador no padrão já conhecido de `dd/MM/yyyy`.

Para fazer isso basta usar o método `ofPattern`:

```
evento.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
```

### Trabalhando com medida de tempo

Para trabalhar com horas, minutos e segundos, utilizamos a classe `LocalDateTime`:

```
LocalDateTime agora = LocalDateTime.now();
```

### Lidando com modelos mais específicos

É muito comum ignorarmos valores quando precisamos apenas de algumas medidas de tempo, como por exemplo ano e mês. Nessa caso no lugar de criarmos um `LocalDate` ou algo assim e ignorar o seu valor de dia, podemos trabalhar com os modelos mais específicos da nova API.

Neste exemplo podemos usar o `YearMonth`, da seguinte forma:

```
YearMonth anoEMes = YearMonth.of(2015, Month.JANUARY);
```

Ou seja, existem diversas novas classes para expressar bem nossas intenções.

Outro exemplo, para trabalharmos apenas com tempo podemos utilizar o `LocalTime`. Representar o horario do nosso intervalo de almoço, por exemplo, poderia ser feito com:

```
LocalTime intervalo = LocalTime.of(12, 30);
```


## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-collections)
- [Projeto final](https://github.com/alura-cursos/JavaCollections/archive/final.zip)

---

[Voltar](./README.md)
