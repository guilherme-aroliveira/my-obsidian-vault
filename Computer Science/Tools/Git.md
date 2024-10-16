Git configuration

git config --global user.name ""

git config --global user.emal ""

Lista todas a configurações do sistema:

- `git config --list`

para informar o nome do usuário definido:

- `git config user.name`

COndigurações adicionais que podem ser adicionadas

- `git config --global core.editor ""` --> defini um editor de texto padrão
- `git config --global color.ui true` --> define as cores a srrem exibidas nk inteface do usuário 

Git workflow

`git init ~/project/java-project` --> initilize a project
`git add file_test.txt` --> add the changes to the staging area
`git commit -m "add java file"` --> commit the chnages with a message

The basic workflow is: chnage files ---> stage ---> commit

Git messages

Commit log


```bash
git log --since='01-january' --pretty=format:%h,%ad,%s,%an > gitlogs.csv
```

git reset --> tirar arquivos do staging area
git clean -df -->
git checkout -- . --> limpa as modificações

git remote -v --> verifica o remote
git remote set-url origin git@github.com: --> troca a referencia do origin
git push -u origin main --> registra a primeira vez o origin

git push -f --> subscreve historico do github