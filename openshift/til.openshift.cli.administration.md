# Deployer une image docker sur openshift en utilisant la CLI


Actuellement chez AXA, je suis amené à deployer un poc sur leur plateforme openshift. En attendant un REX là dessus, voici les principales operations à effectuer afin de deployer une image docker. Ce n'est surement pas la meilleur façon de faire, mais pour le moment ça répond largement à mon besoin. Bien sur toute proposition ou amélioration est la bienvenue. 

## Installation de la CLI

`$ brew install openshift-cli`

## Connection à la plateforme

`$ oc login https://openshift-eu.admin.axaxx.nu:8443/`

## Création d'un projet

`$ oc new-project coho-alep --description="ALEP CEP service" --display-name="ALEP CEP service"`

à la création d'un projet, la cli se positionne automatiquement dessus. 

## Travailler sur un projet Existant

`$ oc project nodejs-test`

Je n'ai pas eu l'occasion de le tester sur un autre os, mais le fait est que sur MacOS l'auto completion en appuyant sur tab fonctionne. Ce qui fait qu'en appuyant sur Tab après project, nous avons la liste des projets disponibles. 

## Création d'une nouvelle application 

`$ oc new-app --docker-image=zedach/cep`

A ce stade si, même si le déploiement se passe bien, l'application n'est pas exposée. Il y aura uniquement creation de [pods](https://docs.openshift.com/enterprise/3.0/architecture/core_concepts/pods_and_services.html#pods) (cf. aussi la [documentation de kubernetes](https://www.digitalocean.com/community/tutorials/an-introduction-to-kubernetes))

## Exposition d'une application

`$ oc expose service cep-services`

## Supprimer une configuration de déploiement 

j'ai beau chercher, la seule manière que j'ai trouvé est de récupéré sous forme de json la configuration et de l'envoyer par pipe directement à la commande delete. Je trouve ça moyen, mais bon ça marche :)

`$ oc get service cep -o json > cep.json && oc delete -f cep.json`

`$ oc get imageStreams -o json > cep-imageStream.json && oc delete -f cep-imageStream.json`

`$ oc get deploymentConfig backend -o json > backend.json | oc delete -f  backend.json`

etc.





 