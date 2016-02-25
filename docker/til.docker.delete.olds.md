# Libérer de l'espace en supprimant les vieux conteneur non taggués / non utilisés

Depuis que je travaille avec docker (mais pas que, les VM aussi) je suis souvent confronté à un problème d'espace disque. Normal, chaque conteneur et image utilisée est conservée pour une prochaine utilisation. 

## Suppression des conteneurs

Qui datent de plus d'une semaine 

```
$ docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs  docker rm -v 
```

ou bien

```
$ docker rm -v $(docker ps -a -q -f status=exited)
```

Ici suppression des conteneurs qui ne sont plus exécutés. 

## Suppression des images

```
$ docker rmi $(docker images -f "dangling=true" -q)
```