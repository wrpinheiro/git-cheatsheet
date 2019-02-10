# Git Cheat Sheet


## Identificação

```sh
# configura usuário global
git config --global user.name "Joseph Climber"

# configura email global
git config --global user.email "joseph@climber.com"

# remova a opção --global para fazer configurações somente no repositório local
git config user.name "J. Climber" 
```

## Criação

```sh
# inicializa um repositório local vazio
git init

# clona um repositório remoto para o local
git clone git@github.com:wrpinheiro/git-cheatsheet.git
```

## Operações comuns

```sh
# adiciona um arquivo na área de stage
git add <file>

# adiciona todos os arquivos na área de stage
git add --all

# adicionar todos os arquivos no diretório corrente e subdiretórios na área de stage
git add .

# mostra o status atual dos arquivos no diretório de trabalho na área de stage
git status

# move um arquivo
git mv <source> <target>

# apaga um arquivo
git rm <arquivo>

# remove um arquivo do índice mas não remove do diretório de trabalho
git rm --cached <arquivo>
```

## Visualizando as alterações 

```sh
# mostra as diferenças entre os arquivos no diretório de trabalho e na área de stage
git diff

# diferenças entre o intervalo de commits sha1-inicial e sha1..final
git diff <sha1-inicial>..<sha1..final>

# mostra as diferenças entre os arquivos na área de stage e os que foram salvos no último commit
git diff --cached
git diff --staged

# mostra as alterações do último commit
git show

# mostra as alterações feitas no commit sha1
git show <sha1>

# mostra os commits efetuados no branch corrente
git log

# mostra o log de um branch específico
git log <branch>

# coisas legais:

# mostra o sha1 abreviado (utilizando 7 dígitos somente)
git log --abbrev-commit

# mostra cada commit em uma única linha
git log --oneline

# desenha um gráfico na forma de texto representando os commits
git log --graph

# adiciona ref names nos commits
git log --decorate
```

## Salvando o trampo

```sh
# faz commit mostrando o editor para informar mensagem
git commit

# faz commit com a mensagem informada
git commit -m "<message>"

# executa git add antes de fazer o commit com a mensagem informada
git commit -am  "<message>"

# executa commit interativo com patch selection
# ou seja, abre uma tela pra você escolher quais
# alterações deve fazer parte do commit!
git commit -p
```

## Outras configurações

```sh
# configura editor default (usado quando for executado um git commit, por exemplo)
git config --global core.editor emacs

# adicionar cor à sua vida! O default é false
git config --global color.ui auto

# mostra todas as configurações
git config -l
```

# Branching

```sh

# mostra os branches existentes
git branch

# mostra todos os branches, inclusive os remotes
git branch -a

# cria um branch
git branch <branch>

# muda para outro branch 
git checkout <branch>

# cria um branch e já o torna o branch atual
# é o mesmo que git branch + checkout
git checkout -b <branch>

# muda o nome do branch para novo-nome
git branch -m <novo-nome>

# apaga um branch
git branch -d <branch>

# apaga um branch mesmo que ainda não tenha sido feito o merge desse branch
git branch -D <branch>
```
