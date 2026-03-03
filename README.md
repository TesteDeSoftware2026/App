# 🛠 Configuração do Ambiente

## 1. Pré-requisitos

Antes de começar, instale:

✅ Docker Desktop

✅ Git

✅ VSCode

 Opcional 

(recomendado para melhor desempenho no Windows | Mais informações adiante):

✅ WSL2 com Ubuntu instalado


## 2. Onde criar a pasta do projeto?

Se você NÃO usa WSL

Pode abrir qualquer pasta da sua preferencia no vscode

No terminal integrado dentro vscode, se certifique do caminho da pasta, digite e rode UMA LINHA POR VEZ:
```
git clone https://github.com/TesteDeSoftware2026/App.git
cd ./App
code .
```
##  3. Configurar o Git (FAZER UMA VEZ SÓ)

Lembre-se configurar seu git:

```
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@gmail.com"
```

Para verificar:

```
git config --list
```
⚠️ O email deve ser o mesmo da sua conta GitHub.


##  4. Criando sua própria branch

Nunca trabalhar diretamente na main.

Sempre criar uma branch nova:

Exemplo:

```
git checkout -b nome-da-branch
```

## 5. Enviando sua branch para o GitHub

Primeiro push:

```
git push -u origin nome-da-branch
```

Depois disso, pode usar apenas:

```
git push origin nome-da-branch
```


#
# 🌿 Fluxo de Trabalho com Git

## 1. Regra de Ouro

🚫 Nunca fazer commit direto na main

🚫 Nunca fazer push direto na main

Sempre trabalhar em uma branch própria.

## 2. Antes de começar qualquer tarefa

Sempre atualizar sua main local primeiro:

```
git checkout main
git pull origin main
```

Isso garante que você está começando com a versão mais recente.

## 3. Criar sua branch

Sempre criar branch a partir da main atualizada:

```
git checkout -b nome-da-branch
```

O uso da flag "-b" é apenas no ato de criar a branch, depois para navegar entre as branchs não é mais necessário

## 4. Fazendo commits

Sempre ao final das alterações importantes, uma sequencia devera ser seguida:

```
git add
git commit 
git push
```
📌 Staging: Fase de preparar os arquivos a serem enviados

Adicionar todos os arquivos que foram modificados:
```
git add .
```

Ou mais específico, adicionando um por vez:

```
git add pasta/arquivo.txt
```

📌 Commit: Fase onde se cria um novo registro no histórico

```
git commit -m "mensagem"
```

Para fins de organização minima do historico, padronize as mensagens da seguinte forma:

```
git commit -m "feat: mensagem"
git commit -m "fix: mensagem"
```

Use "feat: ..." para alguma funcionalidade nova.

Use "fix: ..." para correções.

Exemplos:

```
git commit -m "feat: adiciona rota de login"
git commit -m "fix: corrige erro de conexão com banco"
git commit -m "docs: atualiza instruções do docker"
```

## 5. Antes de dar push (Passo MUITO IMPORTANTE)

Se você passou dias trabalhando, a main pode ter mudado.

Faça isso:

```
git checkout main
git pull origin main
git checkout nome-da-branch
git merge main
```

Se houver conflito:

Resolver manualmente

Depois:

```
git add .
git commit -m "resolve: conflitos com main"
```

Isso evita conflito no Pull Request.

## 6. Enviando para o GitHub

Primeiro push da branch:

```
git push -u origin nome-da-branch
```

Depois disso:
```
git push
```

## 7. Abrindo Pull Request

No GitHub:

- Abrir Pull Request

- Escolher base: main

- Pedir revisão de pelo menos 1 colega


## Fluxo resumido oficial

Toda tarefa segue isso:

```
# Inicio do dia, antes de alterar qualquer arquivo:

git checkout main
git pull origin main
git checkout -b nome-da-branch

# Alterações feitas, prepare o commit:

git add .
git commit -m "feat: minha feature"

# troca para a branch main da sua maquina, e traz a branch main do github:

git checkout main
git pull origin main

# troca para a sua brach e traz a branch main
git checkout feature/minha-feature
git merge main

# Se NÃO houver conflitos:
git push

# Se houver conflitos, veja onde estão, resolva-os manualmente, e depois:

git add .
git commit -m "resolve: conflitos entre a nome-da-branch com a main"
git push
```

Pull Request → revisão → merge.