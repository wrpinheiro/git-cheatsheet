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

# remove um arquivo área de stage mas não remove do diretório de trabalho
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

## Branching

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

## Merging

```sh
# faz merge de um branch com o branch atual
git merge <branch>

# faz os merge e permite informar uma mensagem para o commit do merge
git merge -m <branch>

# faz merge sem fast forward. Isso sempre gera um commit de merge
git merge --no-ff <branch>

# aborta o merge após ocorrer algum conflito.
# volta tudo no estado anterior ao comando de merge.
git merge --abort

# prossegue com o merge após ocorrer algum conflito
git merge --continue
```

## Rebasing

```sh
# faz o rebase baseado em um branch
git rebase <branch>

# operações que podem ser executadas no meio do rebase 
# caso ocorra algum conflito
#
# - continue: permite seguir com o rebase e considerando
#             as alterações na área de stage
# - abort: aborta sem considerar qualquer alteração
#          feita pelo rebase
# - skip: permite pular um commit caso a aplicação desse
#         commit não gerar alteração alguma no código
git rebase --continue
git rebase --abort
git rebase --skip

# faz o rebase interativa baseado em um branc
git rebase -i <branch>

# é a sintaxe geral do rebase interativo. Permite
# fazer rebase utilizando os commits do próprio
# branch.
# 
# As seguintes operações podem ser executadas no rebase
# interativo (também pode ser usada a primeiro letra do comando):
#
# pick: aplica o commit
# rework: permite alterar a mensagem do commit
# edit: permite editar o commit
# squash: junta essa commit no alterior e permite alterar
#         a mensagem do commit
# fixup: semelhante ao squash mas descarta a mensagem do 
#        commit atual
# exec: permite executar um comando nesse commit
# drop: descarta o commit
git rebase -i <commit>
```

## Desfazendo cacas

```sh
# permite alterar o último commit, tanto mensagem
# quanto arquivos que estão na área de stage
git commit --amend

# retira a versão do arquivo da área de stage (é o oposto do git add)
git reset HEAD <arquivo>

# desfaz as alterações do arquivo no diretório de trabalho
git checkout -- <arquivo>
```

## Hostilizando com Reset

```sh
# faz com que o branch atual (branch apontado pelo HEAD) aponte 
# para um commit em questão, sem alterar o índice dos arquivos 
# que estão na área de stage e sem alterar o que está no diretório
# de trabalho. Essa operação não causa perda de dados!
#
# Dica: git reset --soft HEAD~ é a operação inversa ao git commit
git reset --soft <commit>

# faz com que o branch atual aponte para o commit em questão, altera
# o índice de arquivos na área de stage e não altera o diretório
# de trabalho. Essa operação também não causa perda de dados.
# O parâmetro `--mixed` é opcional.
git reset [--mixed] <commit>: move HEAD e também altera o índice

# faz com que o branch atual aponte para o commit em questão, altera
# o índice de arquivos na área de stage e altera os arquivos no
# diretório de trabalho. CUIDADO, essa operação pode causar perda de
# dados.
git reset --hard <commit>: altera HEAD, índice e o diretório de 

# DICA master: você pode juntar vários commits em um só utilizando
# o reset (essa operação se chama squash). Siga o exemplo abaixo.
#
# Suponha que tenhamos a seguinte sequência de commits:
#
#                meu_branch
#                     |
#                     v
# A <- B <- C <- D <- E
#
# e vamos juntar os commits C, D e E.
git checkout meu_branch
git reset --soft B
git commit -m "novo commit C+D+E"  #### 😎 nice!
```

