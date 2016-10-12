La gestion des heures d'été (Daylight Saving Time) en Javascript
================================================================
Lorsque l'on travaille en javascript avec des dates, nous associons souvent un datepicker pour saisir une date que nous stockons en date pour que le serveur transforme désérialise notre date et le map dans notre objet. La date envoyé est au format iso-8601 et à l'heure Zulu (pas de décalage), un format que l'on peut obtenir aisément avec la méthode JSON.stringify() sur une date.

```
new Date(2012,7,1,0,0,0)
// Sat Sep 01 2012 00:00:00 GMT+0200 (Paris, Madrid (heure d’été))
JSON.stringify(new Date(2012,8,1,0,0,0))
// ""2012-08-31T22:00:00.000Z""
```

Le pattern de cette date est **yyyy-MM-dd'T'hh:mm:ss.SSSXXX**.

Appliquons maintenant le même code avec l'année 1970.

```
new Date(1970,8,1,0,0,0)
// Tue Sep 01 1970 00:00:00 GMT+0200 (Paris, Madrid (heure d’été))
JSON.stringify(new Date(1970,8,1,0,0,0))
// ""1970-08-31T22:00:00.000Z""
```

Si on imprime la date côté serveur, nous obtenons la date suivante :

```
Mon Aug 31 23:00:00 CET 1970
```

L'utilisation de l'objet Date en javascript fonctionne parfaitement bien de manière générale. Cependant, nous constatons que le serveur n'a pas récupéré la bonne date pour cette dernière.

Le problème vient du fait que la spécification Javascript applique la dernière règle concernant les heures d'été. Pour la France, la mise en place officielle des heures d'été débute en 1976.

Concernant notre date de 1970, le Javascript a reculé de deux heures et le serveur java a avancé d'une heure pour la mettre à l'heure locale. Nous nous retrouvons donc avec une date reculé d'un jour.

Pour plus d'information, un article a été rédigé et pointe vers les spécifications Javascript :
[http://codeofmatt.com/2013/06/07/javascript-date-type-is-horribly-broken/](http://codeofmatt.com/2013/06/07/javascript-date-type-is-horribly-broken/)

Il existe des librairies Javascript qui prennent en compte les dates d'applications de ces heures d'été et permettent d'avoir une gestion de date similaire à ceux côté serveur tel que [http://momentjs.com/timezone/](http://momentjs.com/timezone/).
