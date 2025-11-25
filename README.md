# Lanchonete Pedidos

Microserviço de gestão de pedidos e produtos do sistema de lanchonete.

## Tecnologias

- Java 17
- Spring Boot 3
- Spring JDBC
- Spring Cloud OpenFeign
- MySQL (RDS)
- RabbitMQ (mensageria)
- Docker
- Kubernetes (EKS)

## Funcionalidades

- Checkout de pedidos
- Gestão de produtos por categoria
- Atualização de status de pedidos
- Comunicação com serviço de Clientes (Feign)

## Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| POST | `/pedidos` | Criar pedido (checkout) |
| GET | `/pedidos` | Listar pedidos |
| GET | `/pedidos/{id}` | Buscar pedido por ID |
| PATCH | `/pedidos/{id}/retirar` | Marcar pedido como retirado |
| GET | `/produtos` | Listar produtos |
| GET | `/produtos/categoria/{categoria}` | Buscar produtos por categoria |
| GET | `/actuator/health` | Health check |

## Comunicação

**REST (Síncrono via OpenFeign):**
- Pedidos → Clientes: Valida cliente por CPF ao criar pedido

**RabbitMQ (Assíncrono):**
- Publica: `pedido.events` (PedidoCriado)
- Consome: `pagamento.events` (PagamentoAprovado, PagamentoRejeitado)
- Consome: `cozinha.events` (PedidoPronto)

## Executar Localmente

```bash
# Compilar
mvn clean package

# Executar (requer MySQL e RabbitMQ)
java -jar target/pedidos-1.0.0.jar
```

## Testes

```bash
# Executar testes
mvn test

# Gerar relatório de cobertura
mvn jacoco:report
```

## Docker

```bash
# Build
docker build -t lanchonete-pedidos .

# Run
docker run -p 8080:8080 lanchonete-pedidos
```

## Deploy

O deploy é automatizado via GitHub Actions:
- **CI**: Executado em Pull Requests (testes + SonarCloud)
- **CD**: Executado no merge para main (build + deploy no EKS)

## Repositórios Relacionados

- [lanchonete-infra](https://github.com/andersonfer/lanchonete-infra) - Infraestrutura
- [lanchonete-clientes](https://github.com/andersonfer/lanchonete-clientes)
- [lanchonete-cozinha](https://github.com/andersonfer/lanchonete-cozinha)
- [lanchonete-pagamento](https://github.com/andersonfer/lanchonete-pagamento)
