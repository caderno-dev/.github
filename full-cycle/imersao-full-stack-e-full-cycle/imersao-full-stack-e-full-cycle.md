# Imersão Full Stack && Full Cycle

## Aula 1 - Full Cycle, Projeto prático e Microsserviços

- **Dev Full Stack:** Focado mais no desenvolvimento de código
- **Dev Full Cycle:** Abrange, além do código, arquitetura e deploy (termo cunhado pelo Netflix)

### Apache Kafka

[Site oficial](https://kafka.apache.org/intro)

**Palavra-chave:** event-driven

#### Características

- É uma plataforma
- Trabalha de forma distribuída
- Banco de dados
- Extremamente rápido e com baixa latência
- Utiliza o disco ao invés de memória

- **NÃO** é apenas um sistema tradicional de filas como o RabbitMQ (ou SQS da Amazon)

#### O que é um "Topic"

- Stream de dados que atua como um banco de dados
- Todos os dados ficam armazenados, ou seja, cada Topic tem seu "local" para armazenar seus dados
- Tópico possui diversas partições
  - Cada partição é definido por número (Ex. partição 0, partição 1...)
  - Você é obrigado a definir a quantidade de partições quando for criar um Topic

#### Kafka Cluster

- Conjunto de Brokers
- Cada Broker é um server
- Cada Broker é responsável por armazenar os dados de uma partição
- Cada partição de Topic está distribuído em diferente Brokers

#### Ecossistema

- Kafka Connect (Connectors)
- Confluent Schema Registry
- Rest Proxy
- ksqlDB
- Streams