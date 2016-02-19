# IntelliJ: Comment résoudre l'erreur du compilateur scala

- - -


Si vous développer avec IntelliJ et que le compilateur scala ne s'execute plus avec cette erreur

```
>>> scala compile server: java.net.bindexception: address already in use:
```

Cette commande permet de tuer le process qui empêche le serveur de compile de s'executer

````
$ kill -9 `lsof -i :3200 -t`
````
