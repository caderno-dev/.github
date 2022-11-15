# Java e java.io: Streams, Reader e Writers

## Leitura com java.io

- **Entrada concreta**: leitura de arquivo, rede ou ainda um teclado.
- `FileInputStream` é uma biblioteca para leitura de arquivos no Java.
- O método `read()` do `FileInputStream` retorna `int`, ou seja, ele é capaz de ler os bytes do arquivo.
- `InputStreamReader` transforma os bytes `int` em caracteres.
- `BufferedReader` lê linhas inteiras do arquivo através do método `readLine()`.

Exemplo de código: 

```
public class TesteLeitura {

  public static void main(String[] args) throws IOException {

    FileInputStream fis = new FileInputStream("lorem.txt");
    InputStreamReader isr = new InputStreamReader(fis);
    BufferedReader br = new BufferedReader(isr);

    String linha = br.readLine();
    br.close();
  }
}
```

## Escrita com java.io

Exemplo de código:
```
public class TesteEscrita {

  public static void main(String[] args) throws IOException {

    OutputStream fos = new FileOutputStream("lorem2.txt");
    Writer osw = new OutputStreamWriter(fos);
    BufferedWriter bw = new BufferedWriter(osw);

    bw.write("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod");
    bw.newLine();
    bw.newLine();
    bw.write("asfasdfsafdas dfs sdf asf assdß");

    bw.close();

  }
}
```

**Obs.:** Podemos trocar as implementações sem precisar fazer muitas alterações no código. Pois o `java.io` fornece classes abstratas genéricas tanto para leitura (InputStream e Reader) quanto para escrita (OutputStream e Writer). Com as classes abstratas não precisamos saber qual a implementação usada na execução do código.

**Resumindo**

De forma geral, os mundos da entrada `Input`, e da saída, `Output`. Estes mundos se subdividem em `InputStream` e `Reader` no primeiro caso, e `OutputStream` e `Writer` no segundo.

Além disso, temos a divisão entre *streams*, e *readers* e *writers*. `InputStream` e `OutputStream` lidam com dados binários, por exemplo imagens e PDFs, já se estivermos lidando com caracteres, utilizamos o `Reader` ou `Writer`.

Há ainda as classes que fazem a transição de um mundo para outro, como é o caso da `InputStreamReader`, que recebe um `InputStream` de *bytes* e o transforma em um `Reader`. Da mesma forma, temos o `OutputStreamWriter`, que faz o mesmo, só que para a escrita. Estas classes possuem padrões de projetos, próprios do `java.io`.

## FileWriter e PrintStream

### Sobre o FileWriter

- `FileWriter` pode ser combinado com outros `Writer`, como `BufferedWriter`.
- É usado para escrever caracteres.
- É usado para estabelecer uma saída com um arquivo.

### PrintWriter e PrintStream

Como os `Writers` e `Readers` foram criados após o `Stream`, eles têm funções muito similares. Inicialmente existia somente o `PrintStream`, mas como depois surgiu o mundo de `Writers`, viu-se a necessidade de criar um `PrintWriter`, este que não precisa utilizar um `Stream` internamente.

```
public class TesteEscrita {

  public static void main(String[] args) throws IOException {

    //Fluxo de Entrada com Arquivo
    //OutputStream fos = new FileOutputStream("lorem2.txt");
    //Writer osw = new OutputStreamWriter(fos);
    //Buff3eredWriter bw = new BufferedWriter(osw);

    //BufferedWriter bw = new BufferedWriter(new FileWriter("lorem2.txt"));
    //PrintStream ps = new PrintStream(new File("lorem2.txt"));

    PrintWriter ps = new PrintWriter("lorem2.txt");

    ps.println("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod");
    ps.println();
    ps.println("asfasdfsafdas dfs sdf asf assdß");

    ps.close();

  }
}
```

Alguns detalhes da classe `System`:
- O atributo `System.out` é do tipo `PrintStream`.
- O método `System.lineSeparator()` devolve os caracteres que representam uma nova linha.
- O método `System.currentTimeMillis()` devolve os milissegundos que passaram desde 1 de janeiro de 1970.

## Usando java.util.Scanner

```
import java.util.Scanner;

public class TesteLeitura {

  public static void main(String[] args) throws FileNotFoundException {

    Scanner scanner = new Scanner(new File("contas.csv"));
    while(scanner.hasNextLine()) {
      String linha = scanner.nextLine();
      System.out.println(linha);
    }

    scanner.close();

  }
}
```

- `scanner.useDelimiter(",");` 

### Formatação de valores
- Caso não exista uma definição de locale padrão para um país: `new Locale("pt", "BR");`
- Para mudar a localização de um texto para americano: `String.format(Locale.US, "Formatando %s", texto);`
- Para formatar um double e definir 3 casas decimais: `String.format("Formatando %06.3f", 45.3);`
- Quando for necessário completar um número inteiro até 4 caracteres com zeros a esquerda: `String.format("Formatando %04d", 20);`

## Encoding e Charsets

Há padrões de conversão de caracteres em binários, e um dos mais comuns está registrado na tabela ASCII (*American Standard Code for Information Interchange*). Temos a letra, e a ela há um número associado, a partir deste, é criada uma sequência binária. Por exemplo, a letra C é representada pelo número 67, e resulta na sequência 01000011.

Para tentar unificar os padrões, e minimizar este tipo de problemas, foi criado o unicode. Trata-se de uma tabela cujo objetivo é de apresentar todos os caracteres existentes no mundo.

Contudo, o unicode não define a forma como as informações devem ser armazenadas no HD, isto é tarefa dos *encodings*. É o caso dos "UTFs", como o `UTF-8` e `UTF-16`, esta sigla significa "*Unicode Transformation Format*". Ela está vinculada desde o nascimento com a tabela de Unicode, para traduzir os *codepoints* para um formato binário.

Além do `UTF` há outros exemplos de Encodings, como o `ASCII` e o `Windows 1252`.

O site do [Unicode Consortium](https://www.unicode.org/), instituição que mantém o Unicode e leia as [perguntas básicas](https://www.unicode.org/faq/basic_q.html) relacionadas (FAQ em inglês).

Outro link interessante é contem a [tabela completa](https://unicode-table.com/pt/) dos caracteres unicode.

## Serialização de objetos

A serialização é a transformação do objeto Java, localizado na memória, em um fluxo de bits e bytes, e vice-versa. Dentro da máquina virtual, ou JVM, temos a memória de objetos (HEAP), e o main, que controla estes objetos.

Isto é possível graças a duas classes:

- `java.io.ObjectOutputStream` = Objeto -> Bits e Bytes
- `java.io.ObjectInputStream` = Bits e Bytes -> Objeto

A primeira para transformar o objeto em um fluxo de bits e bytes, e a segunda para fazer o caminho inverso.

```
public class TesteSerializacao {

  public static void main(String[] args) throws IOException,  ClassNotFoundException {

    // String nome = "Nico Steppat";

    // ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("objeto.bin"));
    // oos.writeObject(nome);
    // oos.close();

    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("objeto.bin"));
    String nome = (String) ois.readObject();
    ois.close();
    System.out.println(nome);

  }
}
```

Para serializar qualquer objeto é necessário que o mesmo implemente a interface de marcação `Serializable`, ou seja, só marca os objetos, sem definir um "contrato formal". Quando o Java introduziu isso, não havia outra forma de marcação.

Ao trabalharmos com serialização, é uma boa prática inserirmos o `serialVersionUID`, que serve para administrar a versão da classe.

A justificativa por trás disso pode ser entendida da seguinte forma:

- Gravamos o `cliente.bin`, e em algum momento posterior o recuperaremos;
- Neste intervalo de tempo, a classe `Cliente` pode mudar, por exemplo, ela pode ganhar mais um método;
- Caso não haja o número serial, a cada alteração na classe utilizada para criar o arquivo `cliente.bin`, causa uma nova versão, ou seja, um novo número gerado;
- Por este motivo, é boa prática forçar um número de versão, desta forma, as alterações - desde que compatíveis - ficarão armazenadas.

Exemplo: `private static final long serialVersionUID = 1L;`

Sobre serialização, podemos afirmar:
- Funciona em cascata. Por exemplo, se um objeto `Livro` possui um `Autor`, ambos, o `Livro` e o `Autor`, serão serializados. Mas há a possibilidade de usar a palavra chave `transient` para "fugir" da serialização de um determinado atributo.
- Para o objeto se tornar *serializável*, é preciso implementar a interface `java.io.Serializable`.
- Não é preciso colocar o atributo `serialVersionUID` para a serialização funcionar, mas é boa prática.
- Os objetos sempre guardam a versão da classe. Se não colocarmos o atributo `serialVersionUID` explicitamente, a versão será gerada na hora de rodar.

### Resumo

- A criação do fluxo binário a partir de um objeto é chamado de **serialização**;
- A criação de um objeto a partir de um um fluxo binário é chamado de **desserialização**;
- A classe deve implementar a interface `java.io.Serializable`;
- A serialização/desserialização funciona em cascata e também com herança;
- Existe a palavra-chave `transient` para indicar que o atributo não deve ser serializado;
- É boa prática colocar o atributo estático `serialVersionUID` para versionar a classe;
- A versão sempre fica guardada no fluxo binário;
- Se não colocarmos explicitamente o `serialVersionUID`, a versão será gerada dinamicamente;
- É raro usar a serialização na "unha", mas é um conhecimento importante, pois será utilizado por outras bibliotecas.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-trabalhando-com-io)

---

[Voltar](./README.md)
