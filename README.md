# testGitFlow


# Comment utiliser git flow ? 
Avec git flow comme workflow notre git répartit en 2 branches:
  
  - main
  - test
  - develop

Le principe est simple pour chaque nouvelle feature les étapes sont les suivantes : 

## Etape 1 : créer une feature

La création d'une feature consiste a créer une branche en partant de develop.  
Pour ce faire nous allons lancer la commande suivante depuis la branche develop :

> `git checkout -b "(type)/(branchID)/(branchName)"`
 Avec :
 - (type)
  - Feature
  - BugFix 

 - (branchID)
  - 3 digits exemple : 005
 - (branchName)
  - le sujet du développement lié à cette branche

