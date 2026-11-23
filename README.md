# API REST com Node.js, Express, MySQL e MVC

**Aluno:** Gustavo Henrique dos Santos  e Murilo Morales
**Turma:** 3º NDN  
**Disciplina:** Programação Web III (PW3)  
**Atividade:** 02 – Refatoração para Arquitetura MVC

## Objetivo

Esta atividade consiste na refatoração da API REST de usuários, separando as responsabilidades do projeto de acordo com o padrão MVC. A API permite cadastrar, listar, consultar, atualizar e excluir usuários.

## Tecnologias utilizadas

- Node.js
- Express
- MySQL
- mysql2
- dotenv
- cors

## Estrutura do projeto

```text
atividade_pw3_mvc/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── models/
│   │   └── usuarioModel.js
│   ├── controllers/
│   │   └── usuarioController.js
│   ├── routes/
│   │   └── usuarioRoutes.js
│   ├── app.js
│   └── server.js
├── .env.example
├── .gitignore
├── package.json
├── schema.sql
└── README.md
```

## Arquitetura MVC utilizada

- **Config:** configura a conexão com o MySQL por meio de um pool e carrega as variáveis de ambiente.
- **Model:** contém exclusivamente as consultas SQL e as operações de acesso aos dados, utilizando queries parametrizadas.
- **Controller:** recebe as requisições, valida os dados, chama o Model e retorna as respostas HTTP em JSON.
- **Routes:** define os endpoints e associa os métodos HTTP às funções do Controller.
- **View:** como o projeto é uma API REST, as respostas em JSON representam a camada de visualização.
- **app.js/server.js:** configuram os middlewares, registram as rotas e iniciam o servidor, sem consultas SQL.

## Como executar o projeto

### 1. Pré-requisitos

Instale o Node.js 18 ou superior e tenha o MySQL em execução.

### 2. Instalar as dependências

Na pasta do projeto, execute:

```bash
npm install
```

### 3. Criar o banco de dados

Execute o arquivo `schema.sql` no MySQL Workbench ou pelo terminal:

```bash
mysql -u root -p < schema.sql
```

### 4. Configurar as variáveis de ambiente

Faça uma cópia do arquivo `.env.example` com o nome `.env` e informe os dados da sua conexão MySQL.

Exemplo:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=sua_senha
DB_DATABASE=dev_db
DB_PORT=3306
PORT=3000
```

### 5. Iniciar a API

```bash
npm start
```

Para iniciar em modo de desenvolvimento:

```bash
npm run watch
```

A API ficará disponível em `http://localhost:3000`.

## Endpoints disponíveis

| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/usuarios` | Cadastra um usuário |
| GET | `/usuarios` | Lista todos os usuários |
| GET | `/usuarios/:id` | Consulta um usuário pelo ID |
| PUT | `/usuarios/:id` | Atualiza os dados de um usuário |
| DELETE | `/usuarios/:id` | Exclui um usuário |

### Exemplo de cadastro

Requisição `POST /usuarios`:

```json
{
  "nome": "Maria",
  "email": "maria@exemplo.com"
}
```

## Códigos HTTP utilizados

- `200` – Operação realizada com sucesso.
- `201` – Usuário cadastrado.
- `400` – Dados inválidos.
- `404` – Usuário ou rota não encontrada.
- `409` – Email já cadastrado.
- `500` – Erro interno do servidor.

## Organização e segurança

As consultas SQL ficam isoladas no Model e utilizam parâmetros (`?`) para evitar a concatenação direta de dados nas instruções SQL. O arquivo `.gitignore` impede o envio da pasta `node_modules` e do arquivo `.env`. O `.env.example` apresenta as variáveis necessárias sem expor senhas reais.
