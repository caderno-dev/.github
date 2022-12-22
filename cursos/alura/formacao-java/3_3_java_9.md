# Novidades do Java 9 e para frente

A partir do java 9, tivemos **várias mudanças na linguagem**. O java passou a ser **modular**, acabando com problemas recorrentes, como o *classpath hell*. Tivemos a polêmica **inferência de variáveis**, que há quem ame e quem odeie a prática. Houve **melhorias nas API's** de `Socket` e `HttpClient`, que há 20 anos eram usadas da mesma maneira. Inserção de novos *garbage collectors* e diversos melhorias que atacam a verbosidade da linguagem. 

## Java 9 (07/2017)

- Factory Method para coleções (06/2014):

```java
List<String> nomes = List.of("nome1", "nome2", "nome3");
```

- Fluxo Reativo (08/2015):

```java
NotaFiscalSubscriber nfs = new NotaFiscalSubscriber();
SubmissionPublisher<NotaFiscal> publisher = new SubmissionPublisher<NotaFiscal>();

publisher.subscribe(nfs);

NotaFiscal nota = new NotalFiscal("João", 39.99, LocalDate.now());

publisher.submit(notaFiscal);
```

- Java Modular (08/2015):

```java
module br.com.alura {
    requires br.com.alura.nf;
    requires br.com.alura.http;
}
```

## Java 10 (03/2018)

- Releases baseada em tempo (11/2017);
- Inferência de variável (03/2016):

```java
var nomes = new ArrayList<String>();
```

- Interface para garbage collector (08/2016);

## Java 11 (09/2018)

- Execução de um arquivo Java com um único comando (12/2017). No terminal: `java Principal.java`
- HttpClient (05/2014)

```java
HttpClient httpClient = HttpClient.newHttpClient();

HttpRequest httpRequest = HttpRequest.newBuilder(uri).GET().build();
HttpResponse<String> httpResponse = httpClient.send(httpRequest, BodyHandlers.ofString());
```

## Java 12 (03/2019)

- Inclusão do novo garbage collector - Shenandoah (01/2014);

## Java 13 (09/2019)

- Mudanças na Socket API (02/2019);
- Text Blocks (04/2019)

```java
public void escreverSQL() {
    String txt = """
        SELECT * FROM
        PRODUTO
        INNER JOIN CLIENTE...
        """;
    txt.length();
}
```

## Java 14 (03/2020)

- Helpful NullPointerExceptions (03/2019);
- Switch Expressions (12/2017)

```java
switch (nome) {
    case "nome1", "nome2" -> System.out.println("Achou o nome: " + nome);
    default -> System.out.println("Não achou");
}
```

- Records (Preview) (04/2019)

```java
record ClienteDTO(String nome, String cpf) { }
```


## Links de referência

- [Página do curso](https://cursos.alura.com.br/extra/alura-mais/novidades-do-java-9-e-para-frente-c228)
- [Mudanças Java - Link oficial](https://docs.oracle.com/en/java/javase/)


---

[Voltar](./README.md)
