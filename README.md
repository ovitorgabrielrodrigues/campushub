# campushub
Sistema de gestão acadêmica com Java, Spring Boot, Oracle e React Native

# CampusHub

Sistema de gestão acadêmica desenvolvido com Java, Spring Boot, React Native e Oracle Database.

O projeto tem como objetivo gerenciar alunos, cursos, matrículas, avaliações e notificações por meio de uma aplicação mobile integrada a três APIs REST.

A implementação utiliza arquitetura em camadas na API principal e dois microsserviços independentes, com responsabilidades e persistência de dados separadas.

## Tecnologias

**Backend**
- Java 21
- Spring Boot
- Spring Data JPA
- Spring Web
- Spring Validation
- Spring Security
- Maven
- Oracle Database
- Flyway
- JUnit 5
- Mockito

**Mobile**
- React Native
- JavaScripty
- Expo
- Axios

**Ferramentas**
- IntelliJ IDEA
- Visual Studio Code
- Git
- GitHub
- Postman
- DBeaver
- Docker

## Arquitetura

O sistema é dividido em quatro aplicações:

| Aplicação | Responsabilidade | Porta |
|---|---|---|
| campushub-api | Gerenciamento de alunos, cursos e matrículas | 8080 |
| notificacoes-service | Gerenciamento de notificações | 8081 |
| avaliacoes-service | Gerenciamento de avaliações e notas | 8082 |
| campushub-mobile | Interface mobile | Expo |

A API principal utiliza arquitetura em camadas, separando as responsabilidades de controller, service e repository.

Os microsserviços possuem suas próprias regras de negócio, entidades, repositórios e migrations. A comunicação entre os serviços será realizada por HTTP.

Cada API terá um schema próprio no Oracle Database, evitando o compartilhamento direto de tabelas.

## Estrutura do projeto

```text
campushub/
├── backend/
│   ├── campushub-api/
│   ├── notificacoes-service/
│   └── avaliacoes-service/
├── mobile/
│   └── campushub-mobile/
├── docker-compose.yml
├── .gitignore
└── README.md
```

### Estrutura das APIs

As aplicações Spring Boot seguem a organização abaixo:

```text
src/
├── main/
│   ├── java/
│   │   └── com/campushub/
│   │       ├── controller/
│   │       ├── service/
│   │       ├── repository/
│   │       ├── model/
│   │       ├── dto/
│   │       ├── enums/
│   │       ├── exception/
│   │       └── config/
│   └── resources/
│       ├── db/
│       │   └── migration/
│       └── application.properties
└── test/
```

A estrutura poderá ser adaptada conforme a necessidade de cada serviço.

## Funcionalidades

### CampusHub API

Responsável pelas operações principais do sistema.

- Cadastro e consulta de alunos
- Cadastro e consulta de cursos
- Gerenciamento de disciplinas
- Matrícula de alunos
- Atualização de informações cadastrais
- Ativação e inativação de registros
- Histórico de alterações
- Autenticação e autorização

### Notificações Service

Responsável pelo registro e gerenciamento de notificações.

- Cadastro de notificações
- Consulta de notificações por usuário
- Marcação de notificações como lidas
- Registro de notificações relacionadas a matrículas

### Avaliações Service

Responsável pelas avaliações acadêmicas.

- Cadastro de avaliações
- Registro de notas
- Consulta de notas por aluno
- Cálculo de médias
- Consulta de resultados

### CampusHub Mobile

Aplicação React Native responsável pela interação com o usuário.

- Autenticação
- Consulta de cursos
- Visualização de matrículas
- Consulta de avaliações e notas
- Visualização de notificações
- Gerenciamento de perfil

## Banco de dados

O banco de dados utilizado é o Oracle Database.

Cada serviço terá um schema independente:

| Serviço | Schema |
|---|---|
| campushub-api | CAMPUSHUB |
| notificacoes-service | CAMPUSHUB_NOTIFICACOES |
| avaliacoes-service | CAMPUSHUB_AVALIACOES |

O versionamento das estruturas do banco será realizado com Flyway.

Exemplo de organização das migrations:

```text
resources/
└── db/
    └── migration/
        ├── V1__create_table_alunos.sql
        ├── V2__create_table_cursos.sql
        ├── V3__create_table_matriculas.sql
        └── V4__create_indexes.sql
```

As migrations serão executadas individualmente por cada aplicação.

## Endpoints

Endpoints inicialmente previstos para a API principal:

| Método | Endpoint | Descrição |
|---|---|---|
| POST | /api/alunos | Cadastrar aluno |
| GET | /api/alunos | Listar alunos |
| GET | /api/alunos/{id} | Consultar aluno |
| PUT | /api/alunos/{id} | Atualizar aluno |
| POST | /api/cursos | Cadastrar curso |
| GET | /api/cursos | Listar cursos |
| POST | /api/matriculas | Realizar matrícula |
| GET | /api/matriculas/{id} | Consultar matrícula |

Os endpoints serão implementados e documentados conforme o desenvolvimento.

## Configuração do ambiente

### Pré-requisitos

- JDK 21
- Maven
- Node.js
- Oracle Database
- IntelliJ IDEA ou outra IDE compatível
- Visual Studio Code ou outro editor compatível com React Native

### Clonando o repositório

```bash
git clone https://github.com/SEU-USUARIO/campushub.git
cd campushub
```

### Configuração do banco

Cada API deverá possuir suas próprias configurações de conexão com o Oracle.

Exemplo de `application.properties`:

```properties
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}

spring.jpa.hibernate.ddl-auto=validate

spring.flyway.enabled=true
spring.flyway.locations=classpath:db/migration
```

As credenciais devem ser fornecidas por variáveis de ambiente e não devem ser adicionadas ao repositório.

### Executando o backend

Acesse a pasta da API desejada e execute:

```bash
./mvnw spring-boot:run
```

No Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Cada serviço deve estar configurado para executar em uma porta diferente.

### Executando o mobile

Acesse o diretório da aplicação React Native:

```bash
cd mobile/campushub-mobile
npm install
npx expo start
```

O aplicativo poderá ser executado em um dispositivo físico ou emulador Android.

## Testes

Os testes serão desenvolvidos utilizando JUnit 5 e Mockito.

Serão contemplados testes unitários, testes de integração, validação de regras de negócio e testes dos endpoints REST.

A comunicação entre os serviços também será validada durante a implementação.

## Organização das branches

O desenvolvimento seguirá a estrutura:

| Branch | Finalidade |
|---|---|
| main | Versão estável |
| homolog | Homologação |
| dev | Desenvolvimento integrado |
| feat/* | Novas funcionalidades |
| fix/* | Correções |

As funcionalidades serão desenvolvidas em branches específicas e integradas por meio de Pull Requests.

## Etapas de desenvolvimento

- [ ] Configuração inicial dos projetos
- [ ] Configuração do Oracle Database
- [ ] Implementação das migrations
- [ ] Desenvolvimento do módulo de alunos
- [ ] Desenvolvimento do módulo de cursos
- [ ] Implementação das matrículas
- [ ] Desenvolvimento do serviço de notificações
- [ ] Desenvolvimento do serviço de avaliações
- [ ] Comunicação entre as APIs
- [ ] Desenvolvimento da aplicação React Native
- [ ] Integração do mobile com o backend
- [ ] Implementação de autenticação JWT
- [ ] Implementação dos testes automatizados
- [ ] Configuração do Docker Compose

## Status

Projeto em desenvolvimento.

As funcionalidades serão implementadas gradualmente, com foco na organização do código, separação de responsabilidades, persistência de dados e integração entre aplicações.
