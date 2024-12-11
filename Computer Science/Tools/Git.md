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

- Example: create feature branch

- git checkout main
- git pull Pull the latest change fro main
- git checkout -b feature-1
- git merge man Merge any chnages from main with your branch
- ....write some code here....
- git add .
- git commit -m 'initial working version of my new feature'
- git push -u origin feature-1 Finally, push your chnages to the remote branch

- u’ option followed by the remote branch name are only needed the first time to create the remote branch

- The whole process has three key components: always start with the latest code from master, alaways create a new branch to work on, set up a remote branch and track it.

Git messages

Commit log


```bash
git log --since='01-january' --pretty=format:%h,%ad,%s,%an > gitlogs.csv
```

git reset --> tirar arquivos do staging area
git clean -df -->
git checkout -- . --> limpa as modificações

git remote -v --> verifica o remote
set the URL correctly for origin:
- `git remote set-url origin https://<USER>@github.com/<USER>/<REPO.git>` --> troca a referencia do origin

git push -u origin main --> registra a primeira vez o origin

git push -f --> subscreve historico do github

- https:://./.../[name].git --> A connection string is a URL that we can use in order to let Git know where the remote repository is located.
- git remote add --> to add the remote repository to a local project. We want to add a remote repository and give it the alias origin to make sure that we always know which remote repository we're pushing to.
    
    Ex: git remote add origin https:://./.../[name].git  
    
- git remote -v --> list all remote repositories on the local machine
- In order to work with this remote repository, we can fetch and push the necessary data from our local project to the hosted repo
- In order to keep our local and remote repo in sync, we have to push the data from our local repo to the remote repo
- git push [origin] [master] --> to push latest data to a remote repo

- [origin] --> alias of a remote repo
- [master] --> current branch
- git push origin dev

- git clone [ ssh link ] --> got clone a repo
- git fetch origin master --> update the local master branch to point to the latest changes made on Origin Master
- git pull origin master --> Instead of individually fetching and then merging

- Merging branches

- Git can perfform two types of merge: fast-foward and no-fast-forward.

- A fast forward merge can happen when the current branch has no extra commits compared to the branch that we're merging. This type of merge doesn't create a new commit, but rather merges the commits on the branch that we're merging right into the current branch.

- (feature/signup)$ git checkout master
- (master)$ git merge feature/signup

- `git fetch`, to fetch the most recent metadata of the remote repo, which describes all the version history and branch information, but it does not actually pull the newest code changes. It allows developers to check if there are any changes without actually pulling any changes. This is so developers can avoid any potential merge conflicts.
- To get the actual changes, and to download and merge their changes into their own workspace, they can run `git pull,` which will pull the most recent version metadata and any changes
- git checkout --> switch their workspace from one branch to anothe

- Git looks in the metadata and makes changes to your local repository to show you exactly that branch’s code.
- You can also use `git checkout` to get back to a previous commit.