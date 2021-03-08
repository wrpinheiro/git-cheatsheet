# Git Cheatsheet

## Identification

```sh
# global user's name
git config --global user.name "Joseph Climber"

# global user's email
git config --global user.email "joseph@climber.com"

# remove --global flag to set values for the local repository
git config user.name "J. Climber" 
```

## Clone & Initialization

```sh
# init an empty local repository
git init

# clone a remote repository into a local directory
git clone git@github.com:wrpinheiro/git-cheatsheet.git
```

## Frequently used operations

```sh
# add a file to the stage area (changes in the stage area will be persisted in the next commit)
git add <arquivo>

# add all changed files to the stage area
git add --all

# add all files in the currenty directory and its subdirectories to the stage area
git add .

# executa git add interativo com patch selection
# ou seja, abre uma tela para selecionar quais partes do arquivo farão parte do commit
git add -p <arquivo>
ou
git add --all -p 
ou
git add . -p

#descrição de cada opção do git add -p (abreviatura de --patch)

#y adiciona esse trecho para o próximo commit
#n não adiciona esse trecho para o próximo commit
#q quit; não adiciona esse trecho para o próximo commit e nenhum dos restantes
#a adiciona esse trecho e todos os demais desse arquivo
#d não adiciona esse trecho e nenhum dos demais desse arquivo
#g selecionar um trecho para ir
#/ pesquise um trecho utilizando regex
#j deixe esse trecho indeciso e vá para o próximo trecho indeciso
#J deixe esse trecho indeciso e veja o próximo trecho
#k deixa esse trecho indeciso e veja o trecho indeciso anterior
#K deixe esse trecho indeciso e veja o trecho anterior
#s divida esse trecho em trechos menores
#e editar manualmente esse trecho
#? help; mostrar todas essas descrições acima

# show the changes in the working directory and the stage area
git status

# move a file
git mv <source> <target>

# remove a file
git rm <arquivo>

# remove a file in the stage area but doesn't change the file in the working dir
git rm --cached <arquivo>
```

## Showing code changes

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

## Saving the work

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

## Other settings

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
git rebase -i <sha1>
```

## Undoing things

```sh
# permite alterar o último commit, tanto mensagem
# quanto arquivos que estão na área de stage
git commit --amend

# retira a versão do arquivo da área de stage (é o oposto do git add)
git reset HEAD <arquivo>

# desfaz as alterações do arquivo no diretório de trabalho
git checkout -- <arquivo>

# remove todos os arquivos que não estão sendo controlados pelo Git
# a opção -n executa um dry-run mostrando todos os arquivos que
# serão removidos. Para remover os arquivos utilize a opção -f
git clean -n
```

## Reseting

```sh
# faz com que o branch atual (branch apontado pelo HEAD) aponte 
# para um commit em questão, sem alterar o índice dos arquivos 
# que estão na área de stage e sem alterar o que está no diretório
# de trabalho. Essa operação não causa perda de dados!
#
# Dica: git reset --soft HEAD~ é a operação inversa ao git commit
git reset --soft <sha1>

# faz com que o branch atual aponte para o commit em questão, altera
# o índice de arquivos na área de stage e não altera o diretório
# de trabalho. Essa operação também não causa perda de dados.
# O parâmetro --mixed é opcional.
git reset [--mixed] <sha1>: move HEAD e também altera o índice

# faz com que o branch atual aponte para o commit em questão, altera
# o índice de arquivos na área de stage e altera os arquivos no
# diretório de trabalho. CUIDADO, essa operação pode causar perda de
# dados.
git reset --hard <sha1>: altera HEAD, índice e o diretório de 

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

## Working with remote repositories

```sh
# clona um repositório remoto para o local (você já viu isso antes 😊)
git clone git@github.com:wrpinheiro/git-cheatsheet.git

# baixa o conteúdo do repositório remoto remote-name. Os branches
# do repositório remoto podem ser referenciados pelos nomes:
#
# <remote-name>/<branch-name>
#
# Ex.: git log origin/master
git fetch <remote-name>

# baixa o conteúdo de branch-name do repositório remoto
# remote-name e faz merge no branch atual
git pull <remote-name> <branch-name>

# faz o mesmo que o anterior porém utiliza as informações
# de vínculo do branch corrente com o branch remoto. Esse
# comando causa um erro caso o branch atual não esteja 
# vinculado com um branch remoto.
# 
# Vide comandos: git push -u e git branch --set-upstream-to
# abaixo.
git pull

# faz push do branch atual no repositório remote-name
# e vincula com o branch branch-name
git push -u <remote-name> <branch-name>

# útil para a seguinte situação:
# você envia um branch local para o repositório remoto, exemplo: origin/feature1
# mas ai você atualiza sua branch local master e precisa fazer um rebase na feature1 local 
# quando fazer um push de novo para origin/feature1 dará erro, o git dirá
# que sua branch está atrás da branch remoto
# o comando abaixo verifica se há modificações no branch remoto que você não tenha
# e atualiza o branch

# se o dev usar o comando -f ou --force a branch origin/feature1 será substituida pela 
# local que está sendo enviada, apagando possiveis alterações que esse branch (origin/feature1) possa ter recebido

git push --force-with-lease <remote-name> <branch-name>

# mostra os remotes configurados. origin é o padrão
git remote -v

# adiciona um remote e usa remote-name para referenciá-lo
git remote add <remote-name> <url>

# remove o remote com nome remote-name
git remote remove <remote-name>

# altera a url do remote remote-name
git remote set-url <remote-name> <url>

# vincula o branch atual com o branch branch-name
# no repositório remoto remote-name
git branch --set-upstream-to=<remote-name>/<branch-name>
```