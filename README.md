# Mandacaru Games — Cadastro e Listagem de Usuários

Projeto desenvolvido para a disciplina de **Design de Interfaces Gráficas**, do curso de **Sistemas e Mídias Digitais**.

O trabalho simula o site institucional de uma produtora fictícia de jogos (*Mandacaru Games*), contendo uma página inicial, um formulário de cadastro de usuários com validações completas (front-end e back-end) e uma página de listagem dos usuários cadastrados, consumindo uma API própria construída em Node.js/Express.

## 🎯 Sobre o projeto

O portfólio é composto por três páginas principais:

- **`home.html`** — Página inicial com a apresentação da empresa fictícia e um showcase dos jogos do portfólio (com links diretos para as páginas na Steam).
- **`cadastro.html`** — Formulário de cadastro de usuários com:
  - Validação de nome, e-mail, senha e campos de endereço;
  - Exibição/ocultação de senha e verificação de força em tempo real (mínimo de 10 caracteres, letra maiúscula, número e caractere especial `*`, `;` ou `#`);
  - Confirmação de senha com checagem de igualdade ao vivo;
  - Upload de foto (até 5MB);
  - Preenchimento automático de endereço a partir do **CEP**, via integração com a API pública [ViaCEP](https://viacep.com.br/);
  - Opção de endereço "sem número".
- **`listagem.html`** — Lista os usuários cadastrados, consumindo a API do back-end com **paginação**.

O back-end (`server.js`) é responsável por:
- Receber e validar os dados do cadastro (nome, e-mail, endereço e senha) com regras de negócio duplicadas no servidor (defesa em profundidade);
- Fazer o upload e armazenamento da foto do usuário via `multer`;
- Simular uma proteção contra tentativas de injeção de SQL nos campos recebidos;
- Expor endpoints REST para cadastro e listagem paginada de usuários (armazenados em memória, sem banco de dados persistente).

## 🛠️ Tecnologias utilizadas

**Front-end**
- HTML5, CSS3 e JavaScript puro (vanilla JS)
- Google Fonts (`DM Sans`, `Montserrat`, `Inter`)
- API externa [ViaCEP](https://viacep.com.br/) para busca de endereço por CEP

**Back-end**
- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/) `^5.2.1`
- [Multer](https://github.com/expressjs/multer) `^2.0.2` (upload de arquivos)
- [CORS](https://github.com/expressjs/cors) `^2.8.5`

## 📁 Estrutura de arquivos

```
├── home.html          # Página inicial
├── cadastro.html       # Formulário de cadastro
├── listagem.html       # Listagem de usuários cadastrados
├── style.css            # Estilos globais
├── scrypt.js            # Lógica do front-end (validações, fetch, CEP, paginação)
├── server.js            # Servidor Express (API e arquivos estáticos)
├── package.json         # Dependências do projeto
└── package-lock.json
```

> Observação: a pasta `fotos_usuarios/` é criada automaticamente pelo servidor na primeira vez que uma foto for enviada no cadastro.

## ✅ Pré-requisitos

Para rodar o projeto localmente você precisa ter instalado:

- **[Node.js](https://nodejs.org/)** versão **18 ou superior** (requisito do Express 5)
- **npm** (já vem junto com o Node.js)

## ▶️ Como rodar o projeto

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/YuriCardosoSMD/DIG_Interface_Completa.git
   cd DIG_Interface_Completa
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   ```

3. **Inicie o servidor:**
   ```bash
   node server.js
   ```
   Você verá a mensagem `Servidor rodando em http://localhost:3000` no terminal.

4. **Acesse no navegador:**
   - Página inicial: [http://localhost:3000/home.html](http://localhost:3000/home.html)
   - Cadastro: [http://localhost:3000/cadastro.html](http://localhost:3000/cadastro.html)
   - Listagem: [http://localhost:3000/listagem.html](http://localhost:3000/listagem.html)

> ⚠️ Importante: como o front-end faz requisições para `http://localhost:3000`, abra as páginas **através do servidor** (passo 4 acima) e não diretamente pelo navegador como arquivo local, para que o cadastro e a listagem funcionem corretamente.

## 🔌 Endpoints da API

| Método | Rota                              | Descrição                                               |
|--------|------------------------------------|----------------------------------------------------------|
| `POST` | `/cadastrar_usuario`               | Cadastra um novo usuário (multipart/form-data, com foto) |
| `GET`  | `/listar_usurios?page=<n>`         | Lista os usuários cadastrados, paginados (5 por página)  |

## 📌 Observações

- O armazenamento dos usuários é **em memória** (array no próprio servidor), ou seja, os dados são perdidos ao reiniciar o servidor.
- Este projeto tem finalidade **acadêmica**, sendo uma atividade da disciplina de Design de Interfaces Gráficas.
