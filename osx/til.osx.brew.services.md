# Gérer les services avec brew

Je viens de découvrir une manière assez simple de démarrer/arrêter/redémarrer un service sous mac osx: `brew services` 


```
$ brew services help
usage: [sudo] brew services [--help] <command> [<formula>|--all]

Small wrapper around 'launchctl' for supported formulae, commands available:
   cleanup Get rid of stale services and unused plists
   list    List all services managed by `brew services`
   restart Gracefully restart service(s)
   start   Start service(s)
   stop    Stop service(s)
  
```

L'installation se fait, en tappant directement une commande du module. Exemple avec list: 

```
$ brew services list
==> Tapping homebrew/services
Cloning into '/usr/local/Library/Taps/homebrew/homebrew-services'...
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 7 (delta 0), reused 4 (delta 0), pack-reused 0
Unpacking objects: 100% (7/7), done.
Checking connectivity... done.
Tapped 0 formulae (32 files, 42K)
...
```

Gérer un service devient nettement plus simple

```
$ brew services start nginx
==> Successfully started `nginx` (label: homebrew.mxcl.nginx)
```
 
## Source

[**Starting and Stopping Background Services with Homebrew**](https://robots.thoughtbot.com/starting-and-stopping-background-services-with-homebrew)
