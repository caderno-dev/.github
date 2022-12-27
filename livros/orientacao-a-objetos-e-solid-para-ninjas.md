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



## 4. Classes abertas e o tal do OCP
## 5. O encapsulamento e a propagação de mudanças
## 6. Herança x composição e o tal do LSP
## 7. Interfaces magras e o tal do ISP
## 8. Consistência, objetinhos e objetões
## 9. Maus cheiros de design
## 10. Métricas de código

