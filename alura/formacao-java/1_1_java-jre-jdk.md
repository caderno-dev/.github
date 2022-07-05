# Java JRE e JDK: compile e execute o seu programa

## O que é Java?

> "Pai do Java": James Gosling

Plataforma Java:

- Portabilidade
- Fácil acesso e desenvolvimento
- Segurança
- Onipresença

Principais componentes da plataforma:

- Java Virtual Machine (JVM)
- Linguagem Java
- Bibliotecas Java (API)

**Java Virtual Machine:**

- Multiplataforma
- Gerenciamento de memória
- Segurança
- Sandbox
- Otimizações
- JIT Compiler

A JVM não é meramente um interpretador por conta de alguns detalhes internos que vão além da interpretação.

O código seria a linguagem Java, e o código "executável", quando compilado, não gera um `.exe`, e sim um formato chamado **bytecode Java**, de extensão `.class`, lido pela JVM, que passaria a informação aos sistemas operacionais.

Características da linguagem Java:

- Orientado a Objeto
- Muitas bibliotecas
- Parece com C++ (hoje em dia isso pode até ser uma desvantagem)
- Roda em vários sistemas operacionais

> **Para saber mais: o nome Bytecode**
> Existe um conjunto de comandos que a máquina virtual Java entende. Esses comandos também são chamados de _opcodes_ (_operation code_), e cada _opcode_ possui o tamanho de exatamente 1 Byte! E aí temos um **opcode de 1 Byte** ou, mais simples, **Bytecode**.

## Instalação

- [Instalando o JDK no Linux](./docs/install-jdk-linux.pdf)
- [Instalando o JDK no Mac](./docs/install-jdk-mac.pdf)
- [Instalando o JDK no Windows](./docs/install-jdk-windows.pdf)

> **Para saber mais:**
> Java Runtime Environment (JRE) = JVM + bibliotecas;
> Java Development Kit (JDK) = JRE + ferramentas

## Tipos e variáveis

### Para saber mais: Type Casting

Tabela de cast implícito e explícito:

| DE/PARA |  byte  |  short  |  char  |   int   |  long   |  float  | double  |
| :------ | :----: | :-----: | :----: | :-----: | :-----: | :-----: | :-----: |
| byte    |  ----  | _Impl._ | (char) | _Impl._ | _Impl._ | _Impl._ | _Impl._ |
| short   | (byte) |  ----   | (char) | _Impl._ | _Impl._ | _Impl._ | _Impl._ |
| char    | (byte) | (short) |  ----  | _Impl._ | _Impl._ | _Impl._ | _Impl._ |
| int     | (byte) | (short) | (char) |  ----   | _Impl._ | _Impl._ | _Impl._ |
| long    | (byte) | (short) | (char) |  (int)  |  ----   | _Impl._ | _Impl._ |
| float   | (byte) | (short) | char)  |  (int)  | (long)  |  ----   | _Impl._ |
| double  | (byte) | (short) | char)  |  (int)  | (long)  | (float) |  ----   |

Tamanhos dos tipos primitivos:

| TIPO    | TAMANHO |
| ------- | ------- |
| boolean | 1 bit   |
| byte    | 1 byte  |
| short   | 2 bytes |
| char    | 2 bytes |
| int     | 4 bytes |
| float   | 4 bytes |
| long    | 8 bytes |
| double  | 8 bytes |

## Trabalhando com caracteres

- `char`: um único caractere. Inicializa-se com aspas simples `''`.
- `String`: conjunto de caracteres. Inicializa-se com aspas duplas `""`.

> Variáveis do tipo primitivo guardam valores e não referências. `String` não é tipo primitivo.

## Links de referência

- [Página do curso](https://cursos.alura.com.br/course/java-primeiros-passos)

---

[Voltar](./README.md)
