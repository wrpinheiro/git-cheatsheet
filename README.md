# Git Cheat Sheet

## Criação

```sh
# inicializa um repositório local vazio
git init

# clona um repositório remoto para o local
git clone git@github.com:wrpinheiro/git-cheatsheet.git
```

## Quem sou eu?

```sh
# configura usuário global
git config --global user.name "Joseph Climber"

# configura email global
git config --global user.email "joseph@climber.com"

# remova a opção --global para fazer configurações somente no repositório local
git config user.name "J. Climber" 
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

# mostra as diferenças entre os arquivos no diretório de trabalho e na área de stage
git diff

# mostra as diferenças entre os arquivos na área de stage e os que foram salvos no último commit
git diff --cached
git diff --staged

# move um arquivo
git mv <source> <target>

# apaga um arquivo
git rm <arquivo>

# remove um arquivo do índice mas não remove do diretório de trabalho
git rm --cached <arquivo>
```



