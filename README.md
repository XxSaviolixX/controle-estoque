# Sistema de Controle de Estoque

Projeto Integrador — Curso Técnico em Desenvolvimento de Sistemas.

Sistema web de controle de estoque com três camadas: banco de dados (MySQL), back-end (API REST em Node.js/Express) e front-end (HTML, CSS e JavaScript puro).

## Funcionalidades

- Cadastro e autenticação de usuários (com senha criptografada e login via JWT)
- CRUD completo de categorias
- CRUD completo de produtos
- Registro de movimentações de entrada e saída de estoque
- Atualização automática da quantidade disponível a cada movimentação
- Dashboard com indicadores gerais e alerta de produtos abaixo do estoque mínimo
- API REST organizada em camadas (rota → controller → service → model)
- Validações e tratamento centralizado de erros

## Tecnologias

Node.js, Express, MySQL (mysql2), JWT (jsonwebtoken), bcryptjs, HTML, CSS e JavaScript.

## Estrutura do projeto

```
controle-estoque/
├── database/           # scripts do banco de dados
│   ├── schema.sql       (cria o banco e as tabelas)
│   └── seed.sql         (insere dados de exemplo)
├── backend/             # API em Node.js
│   ├── package.json
│   ├── .env.example
│   ├── requests.http    (exemplos de requisições para testar a API)
│   ├── testar-conexao.js
│   └── src/
│       ├── config/db.js
│       ├── models/
│       ├── services/
│       ├── controllers/
│       ├── routes/
│       ├── middlewares/
│       ├── app.js
│       └── server.js
└── frontend/            # telas do sistema
    ├── index.html        (login)
    ├── app.html          (sistema)
    ├── css/style.css
    └── js/ (config.js, api.js, login.js, app.js)
```

## Como rodar o projeto

### 1. Pré-requisitos

- Node.js (versão LTS)
- MySQL Server (+ MySQL Workbench, opcional)
- Um servidor estático simples para o front-end (ex.: extensão **Live Server** do VS Code)

### 2. Banco de dados

No MySQL Workbench (ou outro cliente MySQL), execute nesta ordem:

1. `database/schema.sql` — cria o banco `controle_estoque` e as tabelas.
2. `database/seed.sql` — insere dados de exemplo, incluindo o usuário de teste.

### 3. Back-end

```bash
cd backend
cp .env.example .env
# edite o .env com a senha do seu MySQL
npm install
npm start
```

Se tudo estiver correto, o terminal mostrará:

```
Servidor rodando em http://localhost:3000
[OK] Conectado ao banco MySQL: controle_estoque
```

Caso a conexão com o banco falhe, rode `node testar-conexao.js` dentro da pasta `backend` para um diagnóstico detalhado do problema.

### 4. Front-end

Abra a pasta `frontend` no VS Code, clique com o botão direito em `index.html` e escolha **"Open with Live Server"** (ou sirva a pasta com qualquer servidor estático). A tela de login abrirá no navegador.

### 5. Login de teste

```
E-mail: admin@estoque.com
Senha:  123456
```

## Backup do banco de dados

Gerar backup:

```bash
mysqldump -u root -p controle_estoque > backup.sql
```

Restaurar:

```bash
mysql -u root -p controle_estoque < backup.sql
```

## Endpoints principais da API

| Método | Rota                          | Descrição                          | Autenticação |
|--------|-------------------------------|-------------------------------------|--------------|
| POST   | /auth/registrar               | Cria um novo usuário                | Não          |
| POST   | /auth/login                   | Autentica e retorna o token JWT     | Não          |
| GET    | /categorias                   | Lista categorias                    | Sim          |
| POST   | /categorias                   | Cria categoria                      | Sim          |
| PUT    | /categorias/:id                | Atualiza categoria                  | Sim          |
| DELETE | /categorias/:id                | Exclui categoria                    | Sim          |
| GET    | /produtos                     | Lista produtos                      | Sim          |
| POST   | /produtos                     | Cria produto                        | Sim          |
| PUT    | /produtos/:id                  | Atualiza produto                    | Sim          |
| DELETE | /produtos/:id                  | Exclui produto                      | Sim          |
| GET    | /movimentacoes/dashboard      | Indicadores gerais do estoque       | Sim          |
| GET    | /movimentacoes                | Lista movimentações                 | Sim          |
| POST   | /movimentacoes                | Registra entrada/saída              | Sim          |
| DELETE | /movimentacoes/:id             | Exclui movimentação                 | Sim          |

Use o arquivo `backend/requests.http` (extensão REST Client/Thunder Client do VS Code) para testar todas as rotas prontas.

## Histórico de commits

O desenvolvimento foi feito de forma gradual e incremental, com um commit para cada arquivo/etapa criada, seguindo a apostila de referência do projeto (Parte 0 a Parte 4: preparação do ambiente, banco de dados, back-end e front-end).
