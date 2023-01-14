# TDD e Java: Testes automatizados com JUnit

## Testes automatizados

O **JUnit** é a principal biblioteca Java utilizada para escrever **testes de unidades**

Vantagens dos testes automatizados: Automização de ações repetitivas, feedback mais rápido, segurança para mudar o código, favorecimento de melhorias (refactoring).

## JUnit

O JUnit foi criado em 1995 por Kent Beck e Erich Gamma. Beck é considerado o "pai dos testes automatizados", publicou livros e estudos na área, enquanto Gamma é um dos autores do livro "Padrões de Projetos: Reutilizáveis de Software Orientados a Objetos".

É uma biblioteca gratuita e de [código aberto](https://github.com/junit-team/junit5).

Sua função principal é simplificar a escrita de **testes de unidade (ou testes unitários)**, que são a categoria mais simples dos testes automatizados.

Outros tipos de teste: teste de integração, de API, *end-to-end*, aceitação, performance, estresse, etc.

No JUnit, existe a convenção de que o nome da classe do teste deve ser composto pelo nome da classe que você quer testar acompanhada do sufixo `Test`. Por exemplo: 

```java
public class CalculadoraTest {

    @Test
    public void deveriaSomarDoisNumerosPositivos() {
        Calculadora calc = new Calculadora();
        int soma = calc.somar(3, 7);
        Assert.assertEquals(10, soma);
    }
}
```

Onde:
- O nome do método é bem descritivo;
- Está anotado com `@Test` (pacote `org.junit.jupiter.api.Test`);
- Chamada `Assert` para fazer a verificação.

Para o rodar o teste no Eclipse, clique com o botão direito em cima da classe e escolha a opção *Run as > JUnit Test*.


## TDD: Test-Drive Development

Desenvolvimento guiado pelo teste é o conceito onde você primeiramente escreve o teste para depois implementar o código mínimamente necessário para ele funcionar corretametne num determinado cenário, pois a próxima etapa é a refatoração, prática usada para melhorar um código existente.

Vantagens:

- Código já sai "testado";
- Evita testes "viciados" na implementação;
- Refatoração faz parte do processo;
- Ajuda a manter o foco;
- Tendência a escrever um código mais simples;

### Quando utilizar?

No geral, usado para implementar funcionalidades mais complexas, cuja estrutura ainda não está totalmente clara desde o começo, pois assim, o TDD funciona como um rascunho.

## Lidando com exceptions

Existem duas formas de testar exceptions:

- Usando o `assertThrows`

```java
@Test
void bonusDeveriaSerZero() {
    BonusService service = new BonusService();
    assertThrows(IllegalArgumentException.class, 
        () -> service.calcularBonus(new Funcionario(...)));
}
```

- Ou com *try/catch*

```java
@Test
void bonusDeveriaSerZero() {
    BonusService service = new BonusService();
    try {
        service.calcularBonus(new Funcionario(...));
        fail("Não deu exception");
    } catch (Exception e) {
        // pode até validar a mensagem do exception
         assertEquals("Funcionario com salario maior do que R$10000 nao pode receber bonus!", e.getMessage());
    }
}
```

## Mais recursos

- `@BeforeEach`: Anotação para informar ao JUnit que esse método precisa ser executando antes de cada teste.
- `@AfterEach`: Mesma coisa que o `@BeforeEach`, porém para ser executado após cada teste.
- `@BeforeAll` e `@AfterAll`: Métodos que serão executando no início do teste e no final do teste. Os métodos precisam ser **estáticos**.

### Como testar métodos privados?

Se um método é privado, ele não precisa ser testado porque já está sendo usado internamente na classe por outros métodos que passam pelos testes.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/tdd-java-testes-automatizados-junit)
- [Projeto final](https://github.com/alura-cursos/2108-java-testes-unitarios-tdd/archive/aula_5.zip)

---

[Voltar](./README.md)
