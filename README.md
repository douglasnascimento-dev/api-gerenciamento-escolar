# API de Gerenciamento Escolar
![Banner da API de Gerenciamento Escolar](./assets/banner-api-gerenciamento-escolar.png)
Uma API RESTful desenvolvida em Node.js com Express e Sequelize para o gerenciamento de uma pequena aplicação escolar. A API permite o controle de alunos, usuários, autenticação e upload de fotos.

-----

## Índice

  - [Descrição do Projeto](#descrição-do-projeto)
  - [Funcionalidades](#funcionalidades)
  - [Tecnologias Utilizadas](#tecnologias-utilizadas)
  - [Como Rodar o Projeto](#como-rodar-o-projeto)
      - [Pré-requisitos](#pré-requisitos)
      - [Passo a Passo](#passo-a-passo)
  - [Estrutura da API (Endpoints)](#estrutura-da-api-endpoints)

-----

## Descrição do Projeto

Este projeto é o back-end de um sistema de gerenciamento escolar. Ele fornece uma interface segura e organizada para manipular dados de alunos e usuários, utilizando um sistema de autenticação baseado em JSON Web Tokens (JWT) para proteger as rotas.

-----

## Funcionalidades

  - [x] **Autenticação:** Sistema de login com geração de token JWT.
  - [x] **Gerenciamento de Usuários:** CRUD completo para usuários (Create, Read, Update, Delete).
  - [x] **Gerenciamento de Alunos:** CRUD completo para alunos.
  - [x] **Gerenciamento de Fotos:** Upload, exclusão de uma foto específica ou de todas as fotos de um aluno.
  - [x] **Estatísticas:** Endpoint principal que retorna dados agregados, como total de alunos, total de fotos e médias de idade, peso e altura.

-----

## Tecnologias Utilizadas

As seguintes ferramentas e tecnologias foram usadas na construção do projeto:

  - **Node.js**: Ambiente de execução do JavaScript no servidor.
  - **Express.js**: Framework para a construção da API.
  - **Sequelize**: ORM (Object-Relational Mapper) para interagir com o banco de dados.
  - **JSON Web Token (JWT)**: Para criação de tokens de autenticação.
  - **Multer**: Middleware para upload de arquivos.
  - **Dotenv**: Para gerenciamento de variáveis de ambiente.

-----

## Como Rodar o Projeto

Siga os passos abaixo para executar o projeto em seu ambiente local.

### Pré-requisitos

  - Node.js (>14) e NPM
  - Um banco de dados relacional compatível com o Sequelize (PostgreSQL, MySQL, MariaDB, etc.)

### Passo a Passo

1.  **Clone o repositório:**

    ```bash
    git clone https://github.com/douglasnascimento-dev/api-gerenciamento-escolar.git
    cd nome-do-repositorio
    ```

2.  **Instale as dependências:**

    ```bash
    npm install
    ```

3.  **Configure as variáveis de ambiente:**

      - Crie um arquivo `.env` na raiz do projeto, copiando o conteúdo de `.env.example` ou usando o modelo abaixo.
      - Preencha com as suas credenciais do banco de dados e segredos da aplicação.
    <br>
    
    ```dotenv
    DB_NAME=
    DB_HOST=
    DB_PORT=
    DB_USER=
    DB_PASSWORD=
    TOKEN_SECRET=
    TOKEN_EXPIRATION=
    APP_PORT=
    APP_URL=
    ```

4.  **Execute as migrations do Sequelize:**

    ```bash
    npx sequelize-cli db:migrate
    ```

5.  **Inicie o servidor:**

    ```bash
    npm start
    ```

O servidor estará rodando em `http://localhost:3001` (ou na porta que você configurar).

-----

## Estrutura da API (Endpoints)

A seguir estão os endpoints disponíveis na API. Rotas marcadas com 🔒 requerem um token de autenticação Bearer no cabeçalho `Authorization`.

### Home / Estatísticas

| Método | Rota | Descrição                                        | Protegido |
| :----- | :--- | :------------------------------------------------- | :-------- |
| `GET`  | `/`  | Retorna estatísticas agregadas da base de dados. | Não    |

### Autenticação

| Método | Rota      | Descrição                                 | Protegido |
| :----- | :-------- | :---------------------------------------- | :-------- |
| `POST` | `/tokens` | Autentica um usuário e retorna um token JWT. |  Não    |

### Usuários

| Método   | Rota    | Descrição                                       | Protegido |
| :------- | :------ | :------------------------------------------------ | :-------- |
| `POST`   | `/users`| Cria um novo usuário.                             |  Não    |
| `GET`    | `/users`| Retorna os dados do usuário logado.               | 🔒 Sim    |
| `PUT`    | `/users`| Atualiza os dados do usuário logado.              | 🔒 Sim    |
| `DELETE` | `/users`| Deleta a conta do usuário logado.                 | 🔒 Sim    |

### Alunos

| Método   | Rota          | Descrição                         | Protegido |
| :------- | :------------ | :-------------------------------- | :-------- |
| `GET`    | `/students`   | Lista todos os alunos.            | 🔒 Sim    |
| `GET`    | `/students/:id` | Busca um aluno específico por ID. | 🔒 Sim    |
| `POST`   | `/students`   | Cria um novo aluno.               | 🔒 Sim    |
| `PUT`    | `/students/:id` | Atualiza um aluno existente.      | 🔒 Sim    |
| `DELETE` | `/students/:id` | Deleta um aluno.                  | 🔒 Sim    |

### Fotos

| Método   | Rota                             | Descrição                                     | Protegido |
| :------- | :------------------------------- | :-------------------------------------------- | :-------- |
| `POST`   | `/photos`                        | Faz upload de uma foto para um aluno.         | 🔒 Sim    |
| `DELETE` | `/photos/:studentId/:photoId`    | Deleta uma foto específica de um aluno.       | 🔒 Sim    |
| `DELETE` | `/photos/:studentId/all`         | Deleta **todas** as fotos de um aluno.        | 🔒 Sim    |

-----

Feito por **Douglas Nascimento**
