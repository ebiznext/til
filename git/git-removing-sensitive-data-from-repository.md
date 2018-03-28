# Supprimer du contenu sensible commité dans git

Au cas où on commit du contenu sensible par accident. Ici des étapes en mode click and past.


# Rappatrier  la totalité des références du repo

```bash
$ git clone --mirror git://example.com/some-big-repo.git
```

# Télécharger bfg repo cleaner au niveau de la working dir

```bash
$ wget http://repo1.maven.org/maven2/com/madgag/bfg/1.13.0/bfg-1.13.0.jar -O bfg.jar
```

# Supprimer le fichier

```bash
$ java -jar bfg.jar -D password.txt some-big-repo.git
```

# Supprimer les références locales orphelines

bfg supprimes toutes les références des commits et contenus indésirables. Cependant, les fichiers restent là.
Pour les supprimer physiquement, il faut demander à git de purger les références orphelines.

```bash
$ cd some-big-repo.git
$ git reflog expire --expire=now --all && git gc --prune=now --aggressive
```

# Pousser

```bash
$ git push
```

N.B: il faut par précaution demander à tout utilisateur de refaire un nouveau `git clone` afin de ne pas risquer de commiter accidentellement un contenu indésirable.

Plus de détails ici [bfg-repo-cleaner](https://rtyley.github.io/bfg-repo-cleaner/)
