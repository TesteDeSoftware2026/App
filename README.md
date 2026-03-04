# 🚀 Projeto Fullstack com Docker

Aplicação fullstack containerizada utilizando:

* **Backend:** Python + FastAPI + Alembic
* **Frontend:** React + Vite + JavaScript + CSS
* **Banco de Dados:** PostgreSQL
* **Orquestração:** Docker + Docker Compose

Este projeto foi estruturado para funcionar tanto em **Windows puro** quanto em **Windows com WSL (Linux)**.

---

# 📦 Arquitetura do Projeto

```
App/
│
├── backend/        # API FastAPI + Alembic
├── frontend/       # React Vite
├── docker-compose.yml
└── README.md
```

Containers:

* `backend` → API FastAPI
* `frontend` → Aplicação React
* `db` → PostgreSQL

---

# 🧰 Pré-requisitos

## 🔹 Para TODOS (Windows ou Linux/WSL)

1. **Git**
2. **Docker Desktop**
3. **VSCode** (recomendado)

---

# 🖥️ Configuração do Ambiente

## ✅ 1. Instalar Git

Baixe e instale:

[https://git-scm.com/](https://git-scm.com/)

Verifique instalação:

### Windows

CMD ou Powershell
```powershell
git --version
```

### WSL / Linux

Terminal bash
```bash
git --version
```

---

## ✅ 2. Instalar Docker Desktop

Baixe:

[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

⚠️ Durante a instalação:

* Marque a opção **"Enable WSL 2"** (caso use WSL)
* Reinicie o computador após instalar

Verifique instalação:

### Windows (PowerShell)

```powershell
docker --version
docker compose version
```

### WSL (Ubuntu ou outro)

```bash
docker --version
docker compose version
```

---

## ✅ 3. Instalar WSL (Somente para quem for usar Linux no Windows)

No PowerShell como administrador:

```powershell
wsl --install
```


Depois reinicie o computador.

Verifique:

```powershell
wsl --status
```
Ao reiniciar, uma janela de terminal abrirá automaticamente para finalizar a instalação.

- Escolha um usuário (não precisa ser o mesmo do Windows).

- Defina uma senha (ao digitar, os caracteres não aparecem por segurança).

---

# 📥 Clonando o Repositório

Escolha uma pasta adequada para receber o projeto

## Windows (PowerShell ou CMD)

```powershell
git clone https://github.com/TesteDeSoftware2026/App.git
cd App
code .
```

## WSL / Linux

```bash
git clone https://github.com/TesteDeSoftware2026/App.git
cd App
code .
```

---

# 🌿 Fluxo de Trabalho com Git

## ⚠️ Regra Principal

❌ Nunca commitar direto na `main`

Sempre fique atento no caminho que o terminal aponta. Operações com `git` devem ser feitas no caminho com final `/App`

Exemplo:

```
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ git status
```

Para facilitar, use os terminais integrados do vscode, uma vez com a pasta `/App` puxada no `git clone` esteja aberta na IDE.


## 🔹 Criar sua branch individual

O comando `git checkout` premite trocar de branch, seguido pelo nome da branch de destino.

Caso essa branch ainda não exista, ou seja, a intenção é criar uma nova, é necessario usar a flag `-b`
```bash
git checkout -b nome-da-sua-branch
```

Exemplo:

```bash
git checkout -b feature/login
```

---

## 🔹 Atualizar projeto antes de começar

Novamente `git checkout` para trocar de branch

Seguido de `git pull` que vai puxar a versão mais recente no github

```bash
git checkout main
git pull origin main
```

Depois volte para sua branch:

```bash
git checkout nome-da-sua-branch
```

---

## 🔹 Fluxo para enviar alterações

```bash
git add .
git commit -m "Descrição clara do que foi feito"
git push origin nome-da-sua-branch
```

Depois:

1. Vá ao GitHub
2. Clique em **Compare & Pull Request**
3. Abra a Pull Request
4. Aguarde revisão

---

## 🔹 Atualizar sua branch com mudanças da main


Sempre antes de começar alguma alteração, lembre-se de usar a versão mais recente do código, para isso:
```bash
git checkout main
git pull origin main
git checkout nome-da-sua-branch
git merge main
```

Se houver conflito:

1. Resolva manualmente
2. Faça novo commit
3. Push novamente

---

# 🐳 Fluxo com Docker

Sempre execute os comandos na raiz do projeto (onde está o `docker-compose.yml`).
```
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
```

---

## 🔹 Primeira execução

```bash
docker compose up --build
```

Isso:

* Cria as imagens
* Instala dependências
* Sobe os containers

---

## 🔹 Execuções seguintes

```bash
docker compose up
```

---

## 🔹 Parar containers

```bash
docker compose stop
```

---

# 🗄️ Migrations com Alembic

Sempre que modificar algo em `models.py` que impacte o banco:

## 1️⃣ Criar nova migration

```bash
#caminho dos arquivos
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
```

```bash
#digite em seguida
docker compose exec backend alembic revision --autogenerate -m "descrição da alteração"
```

---

## 2️⃣ Aplicar migration

```bash
docker compose exec backend alembic upgrade head
```

---

⚠️ Nunca altere migrations antigas já aplicadas.
Sempre crie uma nova.

---

# 🐍 Criar .venv no Backend (para evitar erros no VSCode)

Mesmo usando Docker, criar um ambiente virtual evita erros falsos de importação no editor.

Entre na pasta backend:

## Windows

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

## WSL / Linux

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Depois, no VSCode:

1. Ctrl + Shift + P
2. "Python: Select Interpreter"
3. Escolha o `.venv`
4. Reinicie o vscode se necessario

### ⚠️ O `.venv` modifica o caminho no terminal
O .venv é necessário apenas para resolver erros falsos do vscode, entretanto, ele pode acabar ativando automaticamente, modificando o terminal:

Exemplo:
```bash
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
(.venv) user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
```

Para desativa-lo (sem excluir o arquivo) basta digitar `deactivate`

Exemplo:
```bash
(.venv) user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ deactivate
user@local:~/nova_pasta/projetos/TesteDeSoftware/App$ 
```

Nenhum comando de docker ou git vai rodar dentro desse (.venv), novamente ele é necessario apenas para resolver os erros falsos que o vscode vai apontar.

---

# 🌍 Portas Padrão

* Frontend → [http://localhost:5173](http://localhost:5173)
* Backend → [http://localhost:8000](http://localhost:8000)
* Banco → Porta 5432

---

# 🛠️ Problemas Comuns

## Docker não inicia

* Verifique se Docker Desktop está aberto
* Reinicie o Docker

## Erro de porta em uso

* Verifique se outra aplicação já usa a porta

## Banco não conecta

* Aguarde o container do PostgreSQL terminar de iniciar

---

# 📌 Boas Práticas

* Sempre atualizar a `main` antes de começar
* Nunca subir código quebrando o build
* Nunca commitar `.venv`
* Nunca JAMAIS commitar `.env`
* Sempre usar Pull Request

---

# 👨‍💻 Objetivo

Este projeto foi estruturado para:

* Padronizar ambiente
* Evitar conflitos de dependência
* Permitir que qualquer integrante rode o projeto com poucos comandos

---

Se todos seguirem este guia, o projeto funcionará de forma consistente em qualquer máquina.
