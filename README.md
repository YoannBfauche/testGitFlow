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
La branche est créer et nous sommes actuellement a la racine de cette branche . 

Il est donc temps d'aporter des modification au code...

## Etape 2 : Ajouter les modifications  

Une fois que des modifications on était réalisées, on vas tout dabord faire un premier commit :
### Git Add : 
> `git add .` 
> Commande qui permet d'ajouter toutes les modifications réalisé depuis le repertoire courant 

> `git add document.txt document2.txt document3.txt`  
> Ajoute précisement le ou les document selectioné.

> `git add /files/`
> Ajoute tous les documents présent dans le repertoire files.

❗ Noubliez pas d'utiliser la commande `git status` pour vous aider.

Une fois les modifications ajouter on vas pouvoir commit :
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
> Permet de lier le repertoire local avec le répertoir distant ( remote )  
> Cette liaison est necessaire pour réaliser plusieur push ou pull entre le remote et le repoLocal

Ton travail est ta branche sont maintenant ajouter au repo github

## Etape 3: Envoyer la Feature sur develop

Nous voulons maintenant terminer la Feature. 
Une protection à était mise en place pour réalisé les fusions de branches 

Il faut donc obligatoirement passé par une pullRequest qui nécessite une review d'une personne.

Les github Actions nous permettent de réaliser des pull Request automatique

### Git Push githubActions

Lorsque l'on push sur github les commits réalisé, si le format du nom de branche correspond à une nouvelle feature alors l'action github ce lance.
Cependant au lancement de l'actions pour créer la pull request, l'actions utilise le dernier commit pour savoir quoi faire.

les parametres : 
  1. "[draftPR]"  
  il permet de lancer la création de la pull request en mode draft. Ce mode permet d'afficher la pull request de la feature permettant a tout le monde de visualisé le développement en cours, cependant le mode draft indique que le travaille n'est pas tout a fait fini et qu'il faut attendre avant de faire la premiére review et de fusioné le code dans la branche develop.
  2 "[startPR]"  
  il permet de lancer la création de la pull request totalement. La pull request ce lance et envoie une notification au reviewers pour verifier le code. une fois aumoins 1 review a était validé le code peux être mergé. 

Comment utiliser ces parametres :
lors du dernier commit avant de push rajouter le parametre dans le commit
> ` git commit -m"[Feature/04] add parameters explication [prStart]"`

La github action gérant les PR automatiques est disponible [ici](.github/workflows/pullRequest.yml)

