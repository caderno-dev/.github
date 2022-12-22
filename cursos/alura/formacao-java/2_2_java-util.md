# Java e java.util: Coleções, Wrappers e Lambda expressions

## Conhecendo Arrays

- Um array é sempre *zero-based* (o primeiro elemento se encontra no *index* 0).
- Um array é sempre inicializado com os valores padrões.
- É uma estrutura de dados
- Um exemplo de sintaxe: `double[] precos = new double[5];`.
- Forma literal para criação: `int[] nums = {1, 2, 3, 4, 5};`.
- Arrays possuem um atributo `length` para saber o tamanho.
- Ao acessar uma posição inválida recebemos a exceção `ArrayIndexOutBoundException`.

## Guardando qualquer referência

### Cast explícito e implícito

**Cast implícito e explícito de primitivos**

```java
int numero = 3;
double valor = numero; // cast implícito
```

```java
double valor = 3.56;
int numero = (int) valor; // cast explícito 
```

**Cast implícito e explícito de referências**

```java
ContaCorrente cc1 = new ContaCorrente(22, 33);
Conta conta = cc1; // cast implícito
Conta conta2 = (Conta) cc1; // cast explícito, mas desnecessário
```

Porém, o cast explícito de referência só funciona se ele for possível, caso contrário **nem compila**, por exemplo:

```
Cliente cliente = new Cliente();
Conta conta = (Conta) cliente;
```

**`ClassCastException`** é do pacote `java.lang`, é uma exceção `unchecked` e é lançada quando o *type cast* falha.

## ArrayList e Generics

### Desvantagens do array

- Array não sabe quantas posições estão ocupadas (apenas tamanho total).
- Array tem um tamanho fixo (não pode crescer dinamicamente).
- Sintaxe fora do padrão "OO Java".

### Conhecendo o ArrayList

- Guarda referências.
- É do pacote `java.util`.
- Usa internamente um array.
- O limite de elementos é o quanto a memória da JVM suporta.
- Inicializando uma lista com capacidade predefinida: `ArrayList lista = new ArrayList(26);`
- Inicializando lista a partir de outra:
```
ArrayList lista = new ArrayList(26);
lista.add("RJ");
lista.add("SP");
// ...outros estados
ArrayList novaLista = new ArrayList(lista);
```

### Benefícios do Generics

- Os *generics* entraram na versão 1.5 na plataforma Java e foram levemente melhorados no Java 1.7.
- O código mais legível, já que fica explícito o tipo dos elementos.
- Evita *casts* excessivos.
- Antecipa problemas de *casts* no momento de compilação. Por exemplo:
```
ArrayList<String> lista = new ArrayList<String>();
lista.add("Nico");
Conta conta = lista.get(0); // não compila
```

## Equals e mais listas

### O método equals

- Assinatura do método: `public boolean equals(Object ref)`.
- Devemos sobrescrever para definir o critério de igualdade.
- A implementação padrão compara as referências.
- É definido na classe `Object`.

### List e LinkedList

- `List` é uma *interface*, a `ArrayList` e a `LinkedList` são implementações.
- Todas as listas garantem a ordem de inserção.
- Todas as listas possuem um índice.
- A `LinkedList` é uma lista duplamente "linkada" e a `ArrayList` representa um array com redimensionamento dinâmico.
- `ArrayList`: Acesso fácil e performático pelo índice; Os elementos precisam ser copiados quando não há mais capacidade.
- `LinkedList`: Inserção e remoção performática em qualquer posição, também no início; Acesso mais demorado pelo índice, é preciso pesquisar os elementos.

## Vetor e a interface Collection

### Vector

- `Vector` é threadsafe.
- Também usa um array por baixo.
- Implementa a interface `List`.

### A interface Collection

- As listas são coleções, garantem a ordem de inserção e são sequências (têm índice).
- `java.util.Collection` é a interface mãe de todas as coleções.
- Os conjuntos (`java.util.Set`) também são coleções, mas não aceitam duplicados nem são listas.

## As classes Wrappers

- *Wrappers* são classes que contém funcionalidades e encapsulam a variável de tipo primitivo!
- `java.lang.Integer` é um Wrapper.
- Aliás, para cada primitivo existe uma classe chamada Wrapper.
- Para guardar um primitivo numa coleção é preciso criar um objeto que embrulha o valor.
- A criação do objeto Wrapper é chamada de *autoboxing*.
- A retirada do valor primitivo do objeto Wrapper é chamada de *unboxing*.
- *Autoboxing* e *unboxing* acontecem automaticamente.
- As classes Wrapper possuem vários métodos auxiliares, por exemplo para *parsing*.
- Todas as classes wrappers que representam um valor numérico possuem a classe `java.lang.Number` como mãe.

## Ordenação de listas

- Para ordenar uma lista é preciso definir um critério de ordenação.
- Existe duas interfaces para ordenar: `java.util.Comparator` e `java.lang.Comparable`.
- `Comparator` é um parâmetro do método `sort` da lista e da classe `Collections`.
- `Comparable` é usado para definir a ordem natural dos elementos.
- Ordem natural é a ordem definida pelo próprio elemento da lista.
- A classe `Collections` é uma fachada com vários métodos auxiliares para trabalhar com as coleções, principalmente listas.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-util-lambdas)
- [Projeto final](https://caelum-online-public.s3.amazonaws.com/850-java-util/08/java6-final.zip)

---

[Voltar](./README.md)
