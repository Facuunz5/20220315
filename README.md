# 20220315
## Ejercicio PreExamen 20220317
#
##	-DOCUMENTACIÓN-

## merge una feature con historial sucio.sh
```
mkdir 17
cd 17
touch f1
git add f1
git commit -m "c 1 en master"
touch f2
git add f2
git commit -m "c 2 en master"
git checkout -b feature
git checkout master
touch f3
git add f3
git commit -m "c 3 en master"
git --no-pager log --oneline --graph
git checkout feature
touch change1
git add change1
git commit -m "c 1 en feature"
touch change2
git add change2
git commit -m "c 2 en feature"
git --no-pager log --oneline --graph
git --no-pager log --oneline --graph --all
git checkout master
git merge feature
git --no-pager log --oneline --graph --all
```
## genramos-conflicto+no-auto-mergeamos.sh
## EXPLICACIÓN: Si solo una rama modifica un fichero, al
## mergear, esos cambios serán aceptados sin conflicto
```
rm -rf .git
rm f1
git init
echo "L1 en f1 en rama main" >> f1
git add f1
git commit -m "+f1:L1"
echo "L2 en f1 en rama main" >> f1
git add f1
git commit -m "+f1:L2"
git --no-pager log --oneline --all --graph
git checkout -b rama1
echo "L1 en f1 en rama1" >> f1
git add f1
git commit -m "+f1:L1"
echo "L2 en f1 en rama1" >> f1
git add f1
git commit -m "+f1:L2"
git checkout main
sed -i s/$/MOD/ f1
cat f1
git add f1
git commit -m "+f1:L1:L2:+MOD"
git merge --no-ff --no-edit rama1
git --no-pager log --oneline --all --graph
cat f1
```
## github-actions-demo.yml
```
name: GitHub Actions Demo
on: 
  push:
      branches: [ main ]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - name: Que ruta es
        run: pwd
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

## git_create_orphan.sh
```
cd repository
git checkout --orphan orphan_name
git rm -rf .
rm '.gitignore'
echo "#Title of Readme" > README.md
git add README.md
git commit -a -m "Initial Commit"
git push origin orphan_name
```

## pasos-previos-para-entender-rebase-para-eliminar-commits.sh
```
#!/usr/bin/env bash
git init
touch f1
git add f1
git commit -m "f1"
touch f2
git add f2
git commit -m "f2"
touch f3
git add f3
git commit -m "f3-este-commit-rompe"
touch f4
git add f4
git commit -m "f4-este-commit-rompe"
touch f5
git add f5
git commit -m "f5"
git --no-pager log --oneline --all 
## hasta aqui
git rebase --interactive <commit-antes-de-lo-que-queremos-borrar>
## cambiar 'pick' por 'drop'
```

## pasos-previos-para-entender-rebase.sh
```
#!/usr/bin/env bash
git init
touch f1
git add f1
git commit -m "c 1 en master"
touch f2
git add f2
git commit -m "c 2 en master"
git checkout -b feature
git checkout master
touch f3
git add f3
git commit -m "c 3 en master"
git --no-pager log --oneline --graph
git checkout feature
touch change1
git add change1
git commit -m "c 1 en feature"
touch change2
git add change2
git commit -m "c 2 en feature"
git --no-pager log --oneline --graph
## hasta aquí, con esta estructura del repo, ahora podremos entender el rebase y compararlo con el merge
```

## rebase_evita_historial_sucio.sh
```
mkdir 17
cd 17
touch f1
git add f1
git commit -m "c 1 en master"
touch f2
git add f2
git commit -m "c 2 en master"
git checkout -b feature
git checkout master
touch f3
git add f3
git commit -m "c 3 en master"
git --no-pager log --oneline --graph
git checkout feature
touch change1
git add change1
git commit -m "c 1 en feature"
touch change2
git add change2
git commit -m "c 2 en feature"
git rebase master #esto aplana el historial pero los dos commits de la rama feature pasarán a tener otro hash!
git checkout master
git merge feature
```
