# Relatorio Tecnico - DeliveryTech API

## 1. Objetivo e Escopo do Projeto

O projeto DeliveryTech API foi desenvolvido com o objetivo de criar uma API REST para um sistema de delivery. A aplicacao permite autenticar usuarios, cadastrar clientes, restaurantes e produtos, alem de criar pedidos com calculo automatico do valor total.

O escopo do sistema inclui:

- cadastro de usuarios com perfis
- autenticacao com JWT
- gerenciamento de clientes
- gerenciamento de restaurantes
- gerenciamento de produtos
- criacao de pedidos
- documentacao automatica com Swagger
- monitoramento com Actuator

O sistema foi pensado para fins academicos, com foco em arquitetura em camadas, seguranca, organizacao do codigo e documentacao tecnica.

## 2. Arquitetura do Sistema

O sistema foi estruturado utilizando arquitetura em camadas, separando responsabilidades para facilitar manutencao e evolucao.

### Camadas da aplicacao

- `controller`: recebe requisicoes HTTP e retorna respostas da API
- `service`: concentra a logica de negocio
- `repository`: acessa o banco de dados via JPA
- `model`: representa as entidades do dominio
- `dto`: organiza os dados trafegados na API
- `config`: configura seguranca e documentacao
- `security`: implementa autenticacao e autorizacao
- `exception`: centraliza o tratamento de erros

### Diagrama simples da arquitetura

```text
Usuario / Swagger / Postman
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

## 3. Estrutura de Pacotes

```text
com.deliverytech
├── config
├── controller
├── dto
│   ├── request
│   └── response
├── exception
├── model
├── repository
├── security
├── service
│   └── impl
└── DeliveryTechApiApplication
```

Essa separacao permite identificar rapidamente onde cada responsabilidade esta implementada.

## 4. Funcionalidades Implementadas

### 4.1 Autenticacao e autorizacao

O sistema possui endpoints de registro e login:

- `POST /api/auth/register`
- `POST /api/auth/login`

Ao autenticar, o sistema gera token JWT para acesso aos endpoints protegidos.

### 4.2 Clientes

Funcionalidades implementadas:

- cadastro de cliente
- listagem paginada de clientes ativos
- busca por id
- atualizacao de dados
- ativacao e desativacao

### 4.3 Restaurantes

Funcionalidades implementadas:

- cadastro de restaurante
- listagem paginada
- busca por id
- busca por categoria
- atualizacao

### 4.4 Produtos

Funcionalidades implementadas:

- cadastro de produto vinculado a restaurante
- listagem por restaurante
- atualizacao
- alteracao de disponibilidade

### 4.5 Pedidos

Funcionalidades implementadas:

- criacao de pedido
- associacao com cliente e restaurante
- validacao dos itens enviados
- calculo automatico do valor total
- persistencia do pedido no banco

## 5. Tecnologias e Bibliotecas Utilizadas

### Linguagem e plataforma

- Java 21
- Spring Boot 3.2.5

### Dependencias principais

- Spring Web: construcao da API REST
- Spring Data JPA: persistencia de dados
- Spring Security: autenticacao e autorizacao
- Spring Validation: validacao de entrada
- H2 Database: banco em memoria para desenvolvimento
- JWT (`jjwt-api`, `jjwt-impl`, `jjwt-jackson`): autenticacao por token
- SpringDoc OpenAPI: documentacao automatica com Swagger
- Spring Boot Actuator: monitoramento da aplicacao
- Micrometer Observation e Tracing: observabilidade e rastreamento
- Lombok: reducao de codigo repetitivo
- Spring Cache: suporte a cache
- Spring Data Redis: dependencia adicionada para evolucao do projeto
- Maven: gerenciamento de build e dependencias
- Docker e Docker Compose: containerizacao

## 6. Documentacao e Monitoramento

### Swagger

A documentacao da API esta disponivel por meio do Swagger:

```text
http://localhost:8080/swagger-ui.html
```

### Actuator

O projeto tambem expoe endpoints de monitoramento, como:

- `/actuator`
- `/actuator/health`
- `/actuator/metrics`
- `/actuator/loggers`

### Logs

Foram adicionadas configuracoes para observabilidade, incluindo:

- logs com nivel `DEBUG` para o pacote `com.deliverytech`
- `traceId` e `spanId` no padrao de logs

## 7. Banco de Dados

O sistema utiliza H2 em memoria:

- URL: `jdbc:h2:mem:deliverydb`
- usuario: `sa`
- senha: vazia

O console H2 pode ser acessado em:

```text
http://localhost:8080/h2-console
```

## 8. Seguranca da Aplicacao

O projeto utiliza Spring Security com autenticacao baseada em JWT.

Perfis de usuario utilizados:

- `ADMIN`
- `CLIENTE`
- `RESTAURANTE`
- `ENTREGADOR`

As permissoes sao controladas em `SecurityConfig`, separando endpoints publicos dos protegidos.

Exemplos:

- autenticacao e monitoramento: acesso publico
- clientes: `ROLE_ADMIN` e `ROLE_CLIENTE`
- pedidos: `ROLE_CLIENTE`
- restaurantes e produtos: `ROLE_ADMIN`

## 9. Testes Realizados

O projeto possui testes automatizados localizados em:

```text
test/java/com/deliverytech
```

Foram identificados testes para:

- criacao de cliente com sucesso
- validacao de entrada em cliente
- configuracao de seguranca para testes

Comando para execucao:

```bash
mvn test
```

## 10. Desafios Enfrentados e Solucoes Aplicadas

Durante o desenvolvimento do projeto, alguns desafios foram encontrados:

### 10.1 Configuracao de seguranca

Foi necessario ajustar o `SecurityConfig` para liberar corretamente Swagger, H2 Console e Actuator, sem comprometer a protecao dos endpoints de negocio.

### 10.2 Organizacao por camadas

Foi importante separar controller, service, repository, model e dto para manter o projeto mais legivel e facil de evoluir.

### 10.3 Documentacao e monitoramento

Foi necessario configurar Swagger e Actuator para documentar e monitorar a API, alem de ajustar propriedades de log e tracing.

### 10.4 Testes

O projeto possui base de testes, mas ainda ha espaco para ampliar a cobertura automatizada em outras camadas, como service e repository.

## 11. Conclusoes

O projeto DeliveryTech API permitiu aplicar conceitos importantes de Arquitetura de Sistemas, como separacao em camadas, seguranca com JWT, documentacao automatica, monitoramento e organizacao do codigo.

O resultado e uma API funcional, documentada e estruturada de forma profissional para fins academicos e para evolucoes futuras.

## 12. Melhorias Futuras

Como possiveis melhorias para as proximas versoes, destacam-se:

- ampliar a cobertura de testes automatizados
- usar banco relacional externo, como PostgreSQL ou MySQL
- implementar cache real com Redis configurado
- melhorar padronizacao das respostas de erro
- adicionar deploy em nuvem
- criar frontend para consumo da API
- evoluir observabilidade com dashboards e metricas externas

## 13. Evidencias Sugeridas para Entrega

Para fortalecer a apresentacao do projeto, recomenda-se anexar:

- print do Swagger funcionando
- print do Actuator com `/health`
- print do console H2
- print dos testes executando
- print dos logs com `traceId` e `spanId`
