## Trouver un .Class dans un groupe de .jar
Cette commande peut être utile pour vérifier si une Class Java existe en doublon dans notre class path
Supposons que les jars de l'application se trouvent dans un repertoire lib :

``` find lib/ -name "*.jar" | xargs grep ClassName.class ```
