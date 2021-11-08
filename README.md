# testGitFlow


# Comment utiliser git flow ? 
Avec git flow comme workflow notre git répartit en 3 branches:
  
  - main
  - test
  - develop

Le principe est simple pour chaque nouvelle feature les étapes sont les suivantes : 

## Etape 1 : Créer une feature

La création d'une feature consiste a créer une branche en partant de develop.  
Pour ce faire nous allons lancer la commande suivante depuis la branche develop :

> `git checkout -b "<type>/<branchID>/<branchName>"`

 Avec :
 1. type
    - Feature
    - BugFix 
 2. branchID
    - 3 digits exemple : 005
 3. branchName
    - le sujet du développement lié à cette branche
La branche est créer et nous sommes actuellement à la racine de cette branche . 

Il est donc temps d'apporter des modifications au code...

## Etape 2 : Ajouter les modifications  

Une fois que des modifications on était réalisées, on vas tout d'abord faire un premier commit :

### Git Add : 
> `git add .` 
> Commande qui permet d'ajouter toutes les modifications réalisé depuis le repertoire courant 

> `git add document.txt document2.txt document3.txt`  
> Ajoute précisement le ou les document selectioné.

> `git add /files/`
> Ajoute tous les documents présent dans le repertoire files.

❗ Noubliez pas d'utiliser la commande `git status` pour vous aider.

Une fois les modifications ajoutées on va pouvoir commit :
### Git Commit

> `git commit -m"[<type>/<branchID>]<commitMessage>"`
> Cette command créer le commit avec :  
> 1. type
>    - Feature
>    - BugFix 
> 2. branchID
>    - 3 digits exemple : 005
> 3. commitMessage
>    - Résumé des modification ‼️ éviter les noms de commit trop long 

### Git Push

> `git push --set-upstream remote <branchName>`
> Permet de lier le répertoire local avec le répertoire distant ( remote )  
> Cette liaison est nécessaire pour réaliser plusieurs push ou pull entre le remote et le repoLocal

Ton travail est ta branche sont maintenant ajouter au repo github

## Etape 3: Envoyer la Feature sur develop

Nous voulons maintenant terminer la Feature. 
Une protection à était mise en place pour réaliser les fusions de branches.  

Il faut donc obligatoirement passé par une pullRequest qui nécessite une review d'une personne. 

Les githubs Actions nous permettent de réaliser des pull Request automatique.

### Git Push githubActions

Lorsque l'on push les commits réalisé sur github, si le format du nom de branche correspond à une nouvelle feature alors l'action github ce lance. 
Cependant au lancement de l'actions pour créer la pull request, l'actions utilise le dernier commit pour savoir quoi faire il faut donc ajouter un paramètre dans le message de commit.

Les paramètres : 
  1. "[draftPR]"  
  il permet de lancer la création de la pull request en mode draft. Ce mode permet d'afficher la pull request de la feature permettant a tout le monde de visualisé le développement en cours, cependant le mode draft indique que le travaille n'est pas tout a fait fini et qu'il faut attendre avant de faire la première review et de fusionné le code dans la branche develop.
  2. "[startPR]"  
  il permet de lancer la création de la pull request totalement. La pull request ce lance et envoie une notification au reviewers pour verifier le code. une fois aumoins 1 review a était validé le code peux être fusionné. 

Comment utiliser ces parametres :
lors du dernier commit avant de push rajouter le paramètre dans le commit
> ` git commit -m"[Feature/04] add parameters explication [prStart]"`
> ❗ Si aucun paramètre n'a était fournit la Pr n'est pas créer 

La github action gérant les PR automatiques est accessible [ici](.github/workflows/pullRequest.yml)

## Etape 4 : Mettre a joure le Repo local .

Lorsque l'on travaille a plusieurs sur github il faut ce mettre a jour pour obtenir les modifications des collégues de travaille. 
Example :
> 2 personnes on créer des features différentes, aprés le premier push, une nouvelle branche pour chaque feature apparait sur github.  
> lorsque la feature est terminer et que l'on ajoute les modifications a la branche develop, la branche de cette feature est supprimé de github. cependant elle n'est pas supprimé du répertoire local. il faut aussi pouvoir récupérer les modifications ajouter dans develop.

Pour ce faire a chaque fois que l'on veux faire une nouvelle action depuis la branche develop il faudra faire les commandes suivantes: 

> Mettre à jour develop   
``` 
git checkout develop
git pull 
```
>  
>  Verifier l'existance des branches sur github  
`git remote show origin`  

> Supprimer les liens entre les brances local et les branches supprimé en remote   
`git remote prune origin `
 
> Supprimer une branche local qui n'est plus utilisé  
 `git branch -d <branchName> `  
 facultative, la supression n'est pas obligatoire on peut garder la branche si l'on veux pouvoir re travailler sur cette feature en particulier



# La gestion des releases 

Pour réaliser une realease nous allons partir de la branche develop.
La release consiste a lancer faire une nouvelle version en production avant cela nous devont réaliser des tests pour verifier que cette version sera fonctionelle en prod.
Pour cela nous utilison la branche de test.


