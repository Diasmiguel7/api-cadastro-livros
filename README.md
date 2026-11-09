# API REST para Cadastro de Livros

API REST simples, feita com Java e Spring Boot, que recebe os dados de um livro via requisição HTTP POST e devolve as informações recebidas em JSON. Atividade prática de introdução a APIs REST.

Não há banco de dados: os livros não são armazenados, a API apenas devolve o que recebe.

## Tecnologias

- Java 17
- Spring Boot 4.1.2
- Maven
- Spring Web (`spring-boot-starter-webmvc`)

## Estrutura do projeto

```
src/main/java/br/com/aula/biblioteca/
├── BibliotecaApplication.java   # classe principal
├── Livro.java                   # modelo: titulo, autor e ano
└── LivroController.java         # endpoint POST /livros
```

## Como executar

### Pré-requisitos

- JDK 17 ou superior instalado
- Porta 8080 livre

### Pela IDE (IntelliJ ou Eclipse)

1. Clone o repositório:
   ```bash
   git clone <URL-DO-REPOSITORIO>
   ```
2. Abra a pasta do projeto na IDE (a que contém o `pom.xml`) e aguarde o Maven baixar as dependências.
3. Execute a classe `BibliotecaApplication`.
4. Quando aparecer `Tomcat started on port 8080` no console, a API está no ar.

### Pelo terminal

Na pasta do projeto:

```bash
# Linux / macOS
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

## Como utilizar

### Cadastrar um livro

- **Método:** `POST`
- **URL:** `http://localhost:8080/livros`
- **Header:** `Content-Type: application/json`

Corpo da requisição:

```json
{
  "titulo": "Java para Iniciantes",
  "autor": "Maria Silva",
  "ano": 2026
}
```

Resposta esperada: status `201 Created` e o mesmo JSON no corpo.

```json
{
  "titulo": "Java para Iniciantes",
  "autor": "Maria Silva",
  "ano": 2026
}
```

### Exemplo com curl

```bash
curl -i -X POST http://localhost:8080/livros \
  -H "Content-Type: application/json" \
  -d '{"titulo":"Java para Iniciantes","autor":"Maria Silva","ano":2026}'
```

## Problemas comuns

| Erro | Causa provável |
|------|----------------|
| `415 Unsupported Media Type` | O body não foi enviado como JSON (no Postman: Body > raw > JSON) |
| `404 Not Found` | URL incorreta; confira se é `/livros` |
| Porta 8080 em uso | Feche o processo que usa a porta ou adicione `server.port=8081` em `application.properties` |
