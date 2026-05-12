# Java 21 Spring Boot Auth Threads API

API autoral desenvolvida em **Java 21** com **Spring Boot**, criada para praticar autenticação, autorização, segurança de senhas e programação concorrente com threads.
Tenho um outro repositorio privado com algo semelhante feito para um SaaS.

O objetivo deste projeto é construir uma API REST com recursos reais de backend, incluindo cadastro e login de usuários, proteção de rotas, hash seguro de senhas com **Argon2id + pepper**, execução de tarefas assíncronas e uso de recursos modernos do Java 21.

## Objetivos do projeto

- Praticar Java 21 em um projeto backend real
- Desenvolver uma API REST com Spring Boot
- Implementar autenticação e autorização
- Estudar JWT e segurança com Spring Security
- Implementar hash de senhas com Argon2id + pepper
- Praticar threads, concorrência e processamento assíncrono
- Explorar `ExecutorService`, `CompletableFuture` e Virtual Threads
- Criar uma base sólida para estudos, testes e evolução técnica

## Tecnologias utilizadas

- Java 21
- Spring Boot
- Spring Web
- Spring Security
- Argon2id
- Pepper para senhas
- JWT
- Maven
- Jakarta Validation
- JPA / Hibernate
- PostgreSQL
- Docker
- JUnit
- Swagger / OpenAPI

## Segurança de senhas

O projeto utilizará **Argon2id + pepper** para armazenamento seguro de senhas.

### O que é Argon2id?

**Argon2id** é uma variação do algoritmo Argon2 recomendada para hash de senhas, combinando resistência contra ataques de GPU e ataques por canal lateral.

No ecossistema Java com Spring Security, a implementação pode ser feita com:

```java
Argon2PasswordEncoder
```

Exemplo planejado:

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return Argon2PasswordEncoder.defaultsForSpringSecurity_v5_8();
}
```

### O que é pepper?

O **pepper** é um segredo global da aplicação usado junto com a senha antes da geração do hash.

Diferente do salt, que normalmente é salvo junto ao hash, o pepper **não deve ser salvo no banco de dados**. Ele deve ficar em um local seguro, como:

- Variável de ambiente
- Secret manager
- Arquivo de configuração fora do repositório
- Serviço de gerenciamento de segredos em cloud

Exemplo conceitual:

```java
String passwordWithPepper = rawPassword + secretPepper;
String hash = passwordEncoder.encode(passwordWithPepper);
```

Na validação do login:

```java
String passwordWithPepper = rawPassword + secretPepper;
boolean matches = passwordEncoder.matches(passwordWithPepper, storedHash);
```

### Objetivo da escolha

A combinação **Argon2id + pepper** será usada para praticar uma abordagem mais robusta de segurança de senhas, evitando salvar senhas em texto puro e reduzindo riscos caso o banco de dados seja comprometido.

## Ideia do projeto

A API combina autenticação de usuários com execução de tarefas protegidas por login.

Usuários poderão se cadastrar, fazer login e executar tarefas simuladas em diferentes modos de processamento, permitindo estudar autenticação, permissões e concorrência dentro de um mesmo projeto.

## Funcionalidades planejadas

### Autenticação e segurança

- Cadastro de usuários
- Login com geração de token JWT
- Hash de senhas com Argon2id
- Uso de pepper fora do banco de dados
- Validação de token
- Proteção de rotas privadas
- Consulta do usuário autenticado
- Controle básico de permissões
- Tratamento seguro de credenciais

### Threads e concorrência

- Criar tarefas de processamento
- Executar tarefas de forma síncrona
- Executar tarefas de forma assíncrona
- Executar múltiplas tarefas em paralelo
- Consultar status de execução
- Cancelar tarefas em execução
- Simular processamento pesado
- Comparar execução sequencial e paralela
- Testar Virtual Threads do Java 21

## Endpoints planejados

### Auth

```txt
POST /auth/register
POST /auth/login
POST /auth/refresh-token
GET  /auth/me
```

### Tasks

```txt
POST   /tasks
GET    /tasks
GET    /tasks/{id}
POST   /tasks/{id}/execute
POST   /tasks/{id}/execute-async
POST   /tasks/execute-parallel
DELETE /tasks/{id}
```

## Estrutura inicial planejada

```txt

```

## Como executar o projeto

Clone o repositório:

```bash
git clone https://github.com/seu-usuario/java21-springboot-auth-threads-api.git
```

Acesse a pasta do projeto:

```bash
cd java21-springboot-auth-threads-api
```

Configure as variáveis de ambiente:

```bash
JWT_SECRET=sua-chave-jwt
PASSWORD_PEPPER=seu-pepper-secreto
```

Execute a aplicação:

```bash
./mvnw spring-boot:run
```

A API ficará disponível em:

```txt
http://localhost:8080
```

## Roadmap

- [ ] Criar projeto com Java 21 e Spring Boot
- [ ] Configurar banco de dados
- [ ] Criar entidade de usuário
- [ ] Implementar cadastro de usuários
- [ ] Configurar Argon2id para hash de senhas
- [ ] Implementar pepper via variável de ambiente
- [ ] Implementar login com JWT
- [ ] Configurar Spring Security
- [ ] Proteger rotas privadas
- [ ] Criar entidade de tarefa
- [ ] Implementar CRUD de tarefas
- [ ] Implementar execução síncrona
- [ ] Implementar execução assíncrona
- [ ] Implementar execução paralela
- [ ] Testar Virtual Threads
- [ ] Criar tratamento global de exceções
- [ ] Adicionar validações
- [ ] Criar testes unitários
- [ ] Criar testes de integração
- [ ] Adicionar Docker
- [ ] Documentar endpoints com Swagger/OpenAPI

## Conceitos praticados

- Java 21
- Spring Boot
- Spring Security
- JWT
- Argon2id
- Pepper
- Hash seguro de senhas
- REST APIs
- DTOs
- Services
- Repositories
- Validação com Jakarta Validation
- Tratamento de exceções
- Threads
- Virtual Threads
- ExecutorService
- CompletableFuture
- Testes automatizados
- Docker
- PostgreSQL

## Status do projeto

🚧 Projeto em desenvolvimento.

## Autor

Desenvolvido por **Tayron Rocha** como projeto autoral para prática de Java 21, Spring Boot, autenticação, segurança de senhas e programação concorrente. Sinta-se livre para contribuir com o projeto. 

## Licença

Este projeto está sob a licença MIT.
