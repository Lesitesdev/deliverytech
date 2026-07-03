# DeliveryTech API

API REST desenvolvida com Spring Boot para simular um sistema de delivery com cadastro de usuarios, clientes, restaurantes, produtos e pedidos.

## Objetivo do Projeto

O objetivo deste projeto e disponibilizar uma API para gerenciar o fluxo principal de uma plataforma de delivery. A aplicacao permite autenticar usuarios, cadastrar entidades do sistema, consultar dados e criar pedidos com calculo automatico do valor total.

## Tecnologias Utilizadas

- Java 21
- Spring Boot 3.2.5
- Spring Web
- Spring Data JPA
- Spring Security
- Spring Validation
- JWT (`jjwt-api`, `jjwt-impl`, `jjwt-jackson`)
- H2 Database
- Swagger / SpringDoc OpenAPI
- Spring Boot Actuator
- Micrometer Observation e Tracing
- Spring Cache
- Spring Data Redis
- Lombok
- Maven
- Docker
- Docker Compose

## Pre-requisitos

Para executar o projeto, tenha instalado:

- Java 21
- Maven 3.8 ou superior
- Docker e Docker Compose (opcional)

## Como Executar o Projeto

### Opcao 1: via Maven

1. Abra o terminal na raiz do projeto.
2. Execute o build:

```bash
mvn clean install
```

3. Inicie a aplicacao:

```bash
mvn spring-boot:run
```

4. A API ficara disponivel em:

```text
http://localhost:8080
```

### Opcao 2: via Docker

1. Na raiz do projeto, execute:

```bash
docker-compose up --build
```

2. A API ficara disponivel em:

```text
http://localhost:8080
```

## Documentacao da API

Swagger:

```text
http://localhost:8080/swagger-ui.html
```

ou

```text
http://localhost:8080/swagger-ui/index.html
```

Actuator:

```text
http://localhost:8080/actuator
```

Exemplos uteis:

- `/actuator/health`
- `/actuator/metrics`
- `/actuator/loggers`

## Banco de Dados

O projeto utiliza banco H2 em memoria.

- URL: `jdbc:h2:mem:deliverydb`
- Usuario: `sa`
- Senha: vazia

Console H2:

```text
http://localhost:8080/h2-console
```

## Estrutura de Pastas

```text
deliverytech
├── src
│   └── main
│       ├── java/com/deliverytech
│       │   ├── config
│       │   ├── controller
│       │   ├── dto
│       │   │   ├── request
│       │   │   └── response
│       │   ├── exception
│       │   ├── model
│       │   ├── repository
│       │   ├── security
│       │   ├── service
│       │   │   └── impl
│       │   └── DeliveryTechApiApplication.java
│       └── resources
│           ├── static
│           └── application.properties
├── test
│   └── java/com/deliverytech
│       ├── config
│       └── controller
├── Dockerfile
├── docker-compose.yml
└── pom.xml
```

## Explicacao das Camadas

- `controller`: recebe requisicoes HTTP e devolve respostas da API
- `service`: concentra as regras de negocio
- `repository`: faz o acesso ao banco de dados
- `model`: representa as entidades do dominio
- `dto`: organiza os dados de entrada e saida da API
- `config`: guarda configuracoes do Spring, Swagger e seguranca
- `security`: implementa JWT, autenticacao e autorizacao
- `exception`: trata erros da aplicacao

## Principais Fluxos do Sistema

### 1. Registro e login

- `POST /api/auth/register`
- `POST /api/auth/login`

O usuario se cadastra com email e senha. A autenticacao gera um token JWT para acesso aos endpoints protegidos.

### 2. Cadastro e gestao de clientes

- `POST /api/clientes`
- `GET /api/clientes`
- `GET /api/clientes/{id}`
- `PUT /api/clientes/{id}`
- `PATCH /api/clientes/{id}/status`

Permite criar, listar, buscar, atualizar e ativar/desativar clientes.

### 3. Cadastro e gestao de restaurantes

- `POST /api/restaurantes`
- `GET /api/restaurantes`
- `GET /api/restaurantes/{id}`
- `GET /api/restaurantes/categoria/{categoria}`
- `PUT /api/restaurantes/{id}`

Permite gerenciar restaurantes e consultar por categoria.

### 4. Cadastro e gestao de produtos

- `POST /api/produtos`
- `GET /api/produtos/restaurante/{restauranteId}`
- `PUT /api/produtos/{id}`
- `PATCH /api/produtos/{id}/disponibilidade`

Permite associar produtos a restaurantes e controlar disponibilidade.

### 5. Criacao de pedidos

- `POST /api/pedidos`

O pedido recebe cliente, restaurante, itens e endereco. O sistema busca os produtos, calcula o total automaticamente e persiste o pedido.

## Arquitetura Simplificada

```text
Cliente / Postman / Swagger
          |
          v
      Controllers
          |
          v
       Services
          |
          v
     Repositories
          |
          v
       Banco H2
```

![arquitetura](/src/imagem.png)

## Seguranca

O sistema utiliza Spring Security com JWT.

Perfis identificados no projeto:

- `ROLE_ADMIN`
- `ROLE_CLIENTE`
- `ROLE_RESTAURANTE`
- `ROLE_ENTREGADOR`

Endpoints publicos principais:

- `/api/auth/**`
- `/swagger-ui/**`
- `/api-docs/**`
- `/h2-console/**`
- `/actuator/**`

## Observabilidade e Monitoramento

O projeto possui:

- Swagger com grupo da API e grupo de monitoramento
- Spring Boot Actuator
- logs com `traceId` e `spanId`
- endpoint de health e metrics

## Testes

Atualmente existem testes automatizados na pasta:

```text
test/java/com/deliverytech
```

Para rodar os testes:

```bash
mvn test
```

## Comandos Uteis

Build:

```bash
mvn clean install
```

Executar:

```bash
mvn spring-boot:run
```

Rodar testes:

```bash
mvn test
```

## Autor

- Projeto academico desenvolvido para a disciplina de Arquitetura de Sistemas
- Sistema: DeliveryTech API
