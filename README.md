# Lanchonete - Pedidos

Microsserviço responsável pelo registro de pedidos e catálogo de produtos.

## Tecnologias

- Java 17
- Spring Boot 3
- MySQL (RDS)
- RabbitMQ

## Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | /pedidos | Criar novo pedido |
| GET | /pedidos | Listar pedidos |
| GET | /pedidos/{id} | Buscar pedido por ID |
| PATCH | /pedidos/{id}/retirar | Marcar pedido como retirado |
| GET | /produtos | Listar produtos |
| GET | /produtos/categoria/{categoria} | Listar produtos por categoria |

## Executar Localmente

```bash
mvn spring-boot:run
```

## Testes

```bash
mvn test
```

## Cobertura

[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=andersonfer_lanchonete-pedidos&metric=coverage)](https://sonarcloud.io/project/overview?id=andersonfer_lanchonete-pedidos)
