# Orientação a Objetos e SOLID para Ninjas: *Projetando classes flexíveis*
Maurício Aniche

## Sumário

1. [Orientação a Objetos, para que te quero?](#1-orientação-a-objetos-para-que-te-quero)
2. [A coesão e o tal do SRP](#2-a-coesão-e-o-tal-do-srp)
3. [Acoplamento e o tal do DIP](#3-acoplamento-e-o-tal-do-dip)
4. [Classes abertas e o tal do OCP](#4-classes-abertas-e-o-tal-do-ocp)
5. [O encapsulamento e a propagação de mudanças](#5-o-encapsulamento-e-a-propagação-de-mudanças)
6. [Herança x composição e o tal do LSP](#6-herança-x-composição-e-o-tal-do-lsp)
7. [Interfaces magras e o tal do ISP](#7-interfaces-magras-e-o-tal-do-isp)
8. [Consistência, objetinhos e objetões](#8-consistência-objetinhos-e-objetões)
9. [Maus cheiros de design](#9-maus-cheiros-de-design)
10. [Métricas de código](#10-métricas-de-código)

## 1. Orientação a Objetos, para que te quero?

A diferença entre código procedural e orientado a objetos é basicamente que em códigos procedurais, a implementação é o que importa. O desenvolvedor pensa o tempo todo em escrever o melhor algoritmo para aquele problema. Já em linguagens orientadas a objeto, a implementação também é fundamental, mas pensar no projeto de classes, em como elas se encaixam e como elas serão estendidas é o que importa.

## 2. A coesão e o tal do SRP

**Uma classe coesa é aquela que possui uma única responsabilidade**. Ou seja, ela não toma conta de mais de um conceito no sistema. 

Toda classe que é não coesa não para de crescer nunca.

#### MVC - Model View Controller

MVC é um padrão arquitetural que divide a aplicação em três grandes partes: a camada de modelo, onde vivem as classes e entidades responsáveis por todas as regras de negócio da aplicação (classes Java convencionais, que usam e abusam de Orientação a Objetos); a camada de visualização, responsável pela interface com o usuário (em aplicações web, são os nossos arquivos JSP, HTML, CSS etc); e a camada de controlador, que faz a ligação entre a interação do usuário na camada de visualização e as regras de negócio que vivem no modelo.

#### Decorators e padrões de projeto

Decorator, Chain of Responsability, State, entre muito outros, são padrões que nos ajudam a manter nossas classes coesas. Recomendação de livro sobre: *Design Patterns com Java - Projeto orientado a objetos guiado por padrões* do Eduardo Guerra.

### Inveja da outra classe

Controllers são sempre um bom exemplo onde programadores costumam escrever maus pedaços de código. A boa prática é fazer com que classes como essas apenas coordenem processos. Mas, nessa tentativa, às vezes escrevemos classes "que invejam outras classes" (*feature envy*).

### SRP - Single Responsilibility Principle

É justamente o princípio que nos lembra de coesão. A descrição mais clara e formal do princípio diz que **a classe deve ter uma, e apenas uma, razão para mudar.** Classes coesas tendem a ser menores e mais simples, menos suscetíveis a problemas, reúso mais fácil e a chance de propagarem problemas para outras classes é menor. 

**Dois comportamentos "pertencem" ao mesmo conceito/responsabilidade se ambos mudam juntos.**

### Separação do modelo, infraestrutura, e a tal da arquitetura hexagonal

A sugestão é para que você sempre separe ao máximo toda e qualquer infraestrutura (seja sem seu framework MVC, ou seu framework de persistência ou mesmo a biblioteca que você usa para criar serviços web) dos seus modelos e regras de negócio. Nem que, em último caso, você precise escrever uma camada de adaptação para sua infraestrutura.

A regra é simples: se a classe tem algum contato com infraestura, você não escreve regras de negócio alguma nelas; se a classe tem regras de negócio, ela não deve conhecer nenhuma infraestrutura.

*Controllers* são um bom exemplo da camada intermediária. Eles fazem a ponte entre a parte web e a parte de domínio. Seus DAOs são outro bom exemplo, eles devem apenas acessar o banco de dados, sem ter nenhuma regra de negócio.

Na arquitetura hexagonal (ou *ports and adapters*), separamos as portas (classes do domínio) de adaptadores (classes que fazem a ponte entre mundos diferentes, como web e domínio, banco de dados e domínio etc).

### Conclusão

Classes coesas são mais fáceis de serem mantidas, reutilizadas e tendem a ter menos bugs. Coesão é fundamental, mas acoplamento também. Essa é uma balança interessante.

## 3. Acoplamento e o tal do DIP

A frase máxima da Orientação a Objetos é **tenha classes que são muito coesas e pouco acopladas**. O grande problema do acoplamento é que uma mudança em qualquer uma das classes pode impactar em mudanças na classe principal. **A partir do momento em que uma classe possui muitas dependências, todas elas podem propagar poblemas para a classe principal**. A classe, quando possui muitas dependências, torna-se muito frágil, fácil de quebrar. Mas como é **impossível não ter acoplamento**, é preciso diferenciá-los.

### Estabilidade de classes

O tipo de "acoplamento bom" é quando a dependência é estável, por exemplo, a interface `List`. Ela possui muitas implementações que estão utilizadas em praticamente todos os sistemas Java. 

Acoplamento é geralmente olhar quais classes de que uma determinada classe depende. Contar isso é importante para detectarmos classes muito acopladas. O outro lado, que é olhar quantas classes dependem de uma classe, nos ajuda a dizer se a classe é ou não estável.

### Buscando por classes estáveis

Interfaces são um bom caminho para isso. Afinal, interfaces são apenas contratos: elas não tem código que pode forçar uma mudança, e geralmente tem implementações dela, e isso faz com que o desenvolvedor pense duas vezes antes de mudar o contrato. A ideia de "programe voltado para interfaces" faz todo sentido. Além de ganhar flexibilidade - afinal, podemos ter várias implementações daquela interface -, a interface tende a ser estável.

> **Interfaces coesas** são aquelas cujos comportamentos são simples e bem definidos.

Alguns padrões de projeto ajudam você a desacoplar seus projetos de classe, como o caso do *Observer*, *Visitor* e *Factory*.

### DIP - Dependency Inversion Principle

A ideia é: **sempre que uma classe for depender de outra, ela deve depender sempre de outro módulo mais estável do que ela mesma**. 

Lembre-se de que abstrações tendem a ser estáveis, e implementações instáveis. Se você está programando alguma classe qualquer com regras de negócio, e precisa depender de outro módulo, idealmente esse outro módulo deve ser uma abstração. Tente ao máximo não depender de outras implementações. 

- Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.
- Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

Isso é o que chamamos de *Depndency Inversion Principle*, o Princípio de Inversão de Dependência. Não confunda com "injeção" de dependência. Injeção de dependência é a ideia de você ter os parâmetros no construtor, e alguém, geralmente um framework, automaticamente injetar essas dependências para você. Na *inversão* de dependência, você está invertendo a maneira de você depender das coisas. Passa a depender agora de abstrações.

> **Todas as classes devem ser estáveis?** Não! Se isso acontecesse, ou seja, todas nossas classes fossem estáveis ao máximo, não conseguiríamos mexer em nada!

### Dependências lógicas

Enxerger acoplamento entre classes é fácil, basta ver se uma depende da outra. Por exemplo, no código-fonte podemos ver a lista de `imports` daquela classe. Mas alguns desses acoplamentos não aparecem de forma clara no código. 

Por exemplo, em uma aplicação web MVC, muitas alterações no *controller* são propagadas para determinadas JSPs. Esse tipo de acoplamento é o que chamamos de **acoplamento lógico**. Esse tipo de acoplamento pode ser perigoso, pois quando um muda, o outro precisa mudar junto. Ou seja, o acoplamento lógico pode nos indicar um mau projeto de classes, ou mesmo código que não está bem encapsulado.

## 4. Classes abertas e o tal do OCP

Classes não coesas devem ter suas responsabilidades divididas em pequenas classes, e que classes devem tentar ao máximo se acoplar com classes que são estáveis, ou seja, mudam pouco.

> **Perceba: a discussão o tempo inteiro é sobre como balancear entre acoplamento e coesão. Buscar esse equilíbrio é fundamental!**

### OCP - Princípio do Aberto-Fechado

Um outro conceito que nos ajuda a ter classes coesas e que evoluam mais fácil é pensar sempre em escrever classes que são "abertas para extensão", mas "fechadas para modificação" (*Open Closed Principle*). A ideia é que suas classes sejam abertas para extensão. Ou seja, estender o comportamento delas deve ser fácil. Mas, ao mesmo tempo, elas devem ser fechadas para alteração. Ou seja, ela não deve ser modificada (ter seu código alterado) o tempo todo.

### Classes extensíveis

Programar orientado a objetos é lidar com acoplamento, coesão, pensando em abstrações para nossos problemas. Quando se tem uma boa abstração, é fácil evoluir o sistema. Seu sistema deve evoluir por meio de novas implementações dessas abstrações, previamente pensadas, e não por meio de diversos `ifs` espalhados por todo o código.

> **Ifs nunca mais? Abstrações sempre?** Códigos flexíveis são importantes, mas têm um custo agregado. Muitas vezes um simples `if` resolve o problema. Portanto, seja parcimonioso. Flexibilize código que realmente precise disso, e seja simples em códigos que podem ser simples.

### A testabilidade agradece!

A partir do momento em que a classe deixa clara todas as suas dependências, e possibilita a troca delas, criamos classes não só facilmente extensíveis, mas também altamente testáveis, pois conseguimos simular as dependências por meio de *mock objects*. Mocks são objetos que dublam outros objetos, simplesmente para facilitar a escrita dos testes.

> *"Se está difícil de testar, é porque seu código pode ser melhorado"*. Um código fácil de ser testado é provavelmente um código bem projetado; já um código difícil de ser testado tem grandes chances de conter problemas de design.

### Conclusão

Classes abertas são aquelas que deixam explícitas as suas dependências. Dessa maneira, podemos mudar as implementações concretas que são passadas para ela a qualquer momento, e isso faz com que o resultado final da sua execução mude de acordo com as classes que foram passadas para ela. Ou seja, conseguimos mudar o comportamento da classe sem mudar o seu código.

## 5. O encapsulamento e a propagação de mudanças

Encapsulamento é o nome que damos à ideia de a classe esconder os detalhes de implementação, ou seja, **como** o método faz o trabalho dele. Isso tem dois ganhos. O primeiro é a facilidade para alterar a implementação. O segundo é que, se o código não está bem encapsulado, isso implica em termos a regra de negócio espalhada por lugares diferentes.

### Intimidade inapropriada

*Intimidade inapropriada* são os códigos que entendem mais do que deveriam sobre o comportamento de uma outra classe.

### Tell, don't ask

Um conhecido princípio de Orientação a Objetos é o *Tell, Don't Ask*, ou seja, "Diga, não pergunte". Quando temos códigos que perguntam uma coisa para um objeto, para então tomar uma decisão, é um código que não está seguindo esse princípio. A ideia é que devemos sempre dizer ao objeto o que ele tem de fazer, e não primeiro perguntar algo a ele, para depois decidir.

### Procurando por encapsulamentos problemáticos

Perceber se um código está bem encapsulado ou não, não é tão difícil. Por exemplo, se pergunte:

- **O que esse método faz?** Provavelmente sua resposta será: eu sei o que o método faz pelo nome dele, calcula o valor do imposto. É um nome bem semântico, deixa claro que ele faz. Se conseguiu responder essa pergunta, está no bom caminho.

- A próxima pergunta é: **Como ele faz isso?** Sua resposta provavelmente é: se eu olhar só para esse código, não dá para responder. Isso é uma coisa boa. Isso é encapsulamento.

### A famosa Lei de Demeter

Ela sugere que evitemos o uso de invocações em cadeia. Por exemplo, dado o código:

```java
public void algumMetodo() {
    Fatura fatura = pegaFaturaDeAlgumLugar();
    fatura.getCliente().marcaComoInadimplente();
}
```

Uma melhor forma seria fazer assim:

```java
public void algumMetodo() {
    Fatura fatura = pegaFaturaDeAlgumLugar();
    fatura.marcaComoInadimplente();
}
```

Assim a própria fatura chamaria o método `cliente.marcaComoInadimplente();` dentro do método dela.
Desta forma, se classe `Cliente` mudar, a classe `Fatura` vai parar de funcionar. Mas agora mexeremos em um único lugar. Lembre-se de que a ideia é sempre diminuir pontos de mudança.

### Getters e setters para tudo, não!

Antes de criar *setters*, pense se eles não gerarão problemas de encapsulamento no futuro. É preferível você fornecer comportamentos que alterem o valor do atributo.

O *getter* é menos prejudicial, uma vez que ele apenas devolve a informação para o usuário. Mas alguns deles podem ser perigosos também. Por exemplo, o *getter* devolver uma lista, que consequentemente pode ser alterada e manipulada. Uma boa ideia é fazer que seus *getters* sempre devolvam cópias dos objetos originais, ou mesmo bloqueiem alterações de alguma forma. Para esse problema de listas em particular, podemos abusar da API da linguagem Java, e devolver uma lista não modificável:

```java
public List<Pagamento> getPagamentos() {
    return Collections.unmodifiablelist(pagamentos);
}
```

### Modelos anêmicos

Evite também os chamados modelos anêmicos, muito comuns no passado da JavaEE. Muitos sistemas têm classes que, ou têm atributos, ou têm métodos. Nunca os dois juntos. Ou seja, temos código procedural em linguagem OO novamente.

O interesante é que se você analisar com cuidado, alguns padrões de projeto separam dados de comportamento. É o caso de *State*, *Strategy*, e muitos outros padrões. Esses são casos particulares, em que optamos por desacoplá-lo para ganhar em flexibilidade. São decisões pontuais ao longo do sistema. Não é o caso de sistemas anêmicos, onde isso acontece o tempo todo.

### Conclusão

Esconda os detalhes da implementação, e diminua pontos de mudança. É isso que tornará seu sistema fácil de ser mantido.

## 6. Herança x composição e o tal do LSP

Já dizia Joshua Bloch: *"Crie suas classes pensando em herança, ou então proíba-a"*. Herança é sempre um assunto delicado. No começo das linguagens orientadas a objeto, a herança era a funcionalidade usada para vender a ideia. Afina, reúso de código de maneira fácil, quem não queria? Mas, na prática, utilizar herança pode não ser tão simples.

Note que as **classes filhas precisam respeitar os contratos definidos pela classe pai.** Mudar esses contratos pode ser perigoso.

### LSP - Liskov Substitutive Principle

Para usar herança de maneira adequada, o desenvolvedor deve pensar o tempo todo nas pré e pós-condições que a classe pai definiu.

Toda classe ou método tem as suas pré e pós-condições. Por précondições, entenda os dados que chegam nela. Quais são as restrições iniciais para que aquele método funcione corretamente? Por exemplo, o método `deposita()` deve receber um inteiro maior que zero. Se uma classe filha mudar essa precondição para somente números maiores que 10, por exemplo, poderemos ter problemas.

A pós-condição é o que aquele comportamento devolve? Por exemplo, o método `rende()` não devolve nada e não lança exceção. Mas se uma das classes filhas lançar um exceção neste método. Problema.

Podemos mudar as pré e pós-condições, mas com regras. A classe filho só pode afrouxar a precondição. Já a pós-condição é ao contrário, só pode ser apertada, ela nunca pode afrouxar. É sobre isso que o Princípio de Substituição de Liskov discute. Ao herdar, você deve sempre lembrar do contrato estabelecido pelo pai.

### Acoplamento entre a classe pai e a classe filho

É fácil notar que a classe filho é totalmente acoplada à classe pai. Afinal, qualquer mudança no pai impacta no filho. Sendo assim, é importante tentar ao máximo reduzir o acoplamento entre a classe pai e a classe filho. Podemos também usar o termo encapsulamento. Afinal, se a classe filho conhece demais da implementação da classe pai, é porque ela não encapsulou bem seus detalhes de implementação.

Além disso, uma boa maneira para diminuir a chance de quebrar o encapsulamento é evitar o uso de `protected`. 

### Favoreça a composição

Usar herança é sim complicado, e o seu mau uso pode trazer problemas. É por isso que muitos desenvolvedores sugerem o uso de composição.

A composição tem vantagens. A relação da classe principal com a classe dependida não é tão íntima quanto a relação existente entre classes pai e filho, portanto, quebrar o encapsulamento é mais difícil. A composição nos dá flexibilidade.

Escrever testes automatizados também é mais fácil. Mockar objetos e comportamentos e passá-los para classes que as usam para compor o comportamento é natural; com herança, muito mais difícil.

### Quando usar herança então?

Herança deve ser usada quando existe realmente a relação de X **é um** Y. Por exemplo, `Gerente` é um `Funcionário`, ou `ICMS` é um `Imposto`. Não use herança caso a relação seja de composição, ou seja, X **tem um** Y, ou X **faz uso de** Y.

Nada também o impede de usar herança e composição.

Enfim, não descarte herança, apenas favoreça a composição.

## 7. Interfaces magras e o tal do ISP
## 8. Consistência, objetinhos e objetões
## 9. Maus cheiros de design
## 10. Métricas de código

