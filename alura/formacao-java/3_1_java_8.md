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



## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-collections)
- [Projeto final](https://github.com/alura-cursos/JavaCollections/archive/final.zip)

---

[Voltar](./README.md)
