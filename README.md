
Este repositório contém o projeto GRT System, composto por múltiplos microsserviços, cada um com seu próprio banco de dados e lógica de negócios. Abaixo estão as instruções para compilar e rodar a aplicação localmente utilizando Docker e Docker Compose.

## Requisitos

Antes de rodar a aplicação, você precisa ter as seguintes ferramentas instaladas:

- **Java JDK 21** (ou versão superior)
- **Maven**
- **Docker**
- **Docker Compose**

## Estrutura do Projeto

O projeto contém três microsserviços, sendo:

1. **Ecommerce** - Serviço relacionado à plataforma de ecommerce.
2. **Fidelity** - Serviço relacionado ao sistema de fidelidade de clientes.
3. **Store** - Serviço relacionado ao gerenciamento de lojas e seus produtos.

Cada microsserviço possui seu próprio banco de dados MySQL e se comunica com outros serviços conforme necessário.

## Instruções para rodar a aplicação

### Passo 1: Gerar o arquivo `.jar` para cada microsserviço

Para cada microsserviço, é necessário compilar o projeto utilizando Maven e gerar o arquivo `.jar`. Para isso, no diretório de cada microsserviço, execute o seguinte comando:

```bash
mvn clean install -DskipTests
```

Este comando irá compilar o código fonte e gerar o arquivo `.jar` na pasta `target/`. A opção `-DskipTests` é utilizada para pular a execução dos testes unitários durante a compilação.

### Passo 2: Criar a imagem Docker para cada microsserviço

Depois de gerar o arquivo `.jar` para cada microsserviço, você deve criar a imagem Docker para cada um. Para isso, execute o comando abaixo no diretório de cada microsserviço:

```bash
docker build -t <nome-do-microsserviço> .
```

Substitua `<nome-do-microsserviço>` pelo nome do microsserviço (por exemplo, `ecommerce`, `fidelity`, ou `store`). O comando irá construir a imagem Docker com base no Dockerfile presente no projeto.

### Passo 3: Subir os microsserviços com Docker Compose

Após gerar as imagens Docker para todos os microsserviços, o próximo passo é rodar os serviços utilizando o Docker Compose. Para isso, execute o seguinte comando no diretório raiz do projeto (onde está localizado o arquivo `docker-compose.yml`):

```bash
docker-compose up --build
```

Este comando irá:

1. Criar os containers para todos os microsserviços e seus respectivos bancos de dados.
2. Rodar os microsserviços e as dependências de forma integrada.

O comando `--build` garante que as imagens Docker sejam reconstruídas antes de iniciar os containers.

### Passo 4: Acessar os microsserviços

Após a execução do comando `docker-compose up --build`, os microsserviços estarão disponíveis nas portas configuradas no arquivo `docker-compose.yml`. Por exemplo:

- **Ecommerce**: Acessível em `http://localhost:8080`
- **Fidelity**: Acessível em `http://localhost:8081`
- **Store**: Acessível em `http://localhost:8082`

As portas podem variar dependendo das configurações no `docker-compose.yml`, mas por padrão, as portas são mapeadas para `8080`, `8081`, e `8082`.

### Passo 5: Parar os microsserviços

Quando você terminar de trabalhar com a aplicação, pode parar os containers utilizando o comando:

```bash
docker-compose down
```

Este comando irá parar e remover todos os containers, redes e volumes associados ao projeto.

## Estrutura de Diretórios

O projeto possui a seguinte estrutura de diretórios:

```
grt-system/
│
├── ecommerce/                   # Diretório do microsserviço ecommerce
│   ├── src/                     # Código fonte do microsserviço
│   ├── target/                  # Arquivo .jar gerado após mvn clean install
│   ├── Dockerfile               # Dockerfile para gerar a imagem do microsserviço
│   ├── pom.xml                  # Arquivo de configuração do Maven
│
├── fidelity/                    # Diretório do microsserviço fidelity
│   ├── src/
│   ├── target/
│   ├── Dockerfile
│   ├── pom.xml
│
├── store/                       # Diretório do microsserviço store
│   ├── src/
│   ├── target/
│   ├── Dockerfile
│   ├── pom.xml
│
├── docker-compose.yml           # Arquivo de configuração do Docker Compose
└── README.md                    # Este arquivo
```

## Docker Compose

O arquivo `docker-compose.yml` é utilizado para definir e configurar os containers do Docker. Ele inclui a configuração dos três microsserviços e suas respectivas dependências de banco de dados.


## Conclusão

Seguindo as instruções acima, você conseguirá rodar a aplicação GRT System com seus três microsserviços em containers Docker, utilizando o Docker Compose para orquestrar a execução dos serviços. 

Se você tiver qualquer dúvida ou precisar de ajuda, não hesite em abrir uma issue no repositório!

---

Este README fornece uma visão geral de como configurar e rodar o sistema localmente.

