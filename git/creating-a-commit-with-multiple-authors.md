# Commiter dans git à deux ou plusieurs

Plusieurs situation nous amènent à collaborer pour écrire du code: code review, on bording, debug, etc.

Github [supporte](https://blog.github.com/2018-01-29-commit-together-with-co-authors/) depuis peu la possibilité de commiter à plusieurs. Pour information, ils ont implémenté un des `trailers` utilisée par certains projets open source, et que vous pouvez découvrir [ici](https://git.wiki.kernel.org/index.php/CommitMessageConventions).

Il suffit pour cela de rajouter la balise `Co-authored-by:` suivi du `name` et du `<mail>` à la suite d'une ligne vide qui suit le message du commit.

```bash
git commit -m "Refactor usability tests.
>
>
Co-authored-by: name <name@example.com>
Co-authored-by: another-name <another-name@example.com>"
```

Malheureusement, cette fonctionalité n'est pas encore supporté par [Gitlab](https://gitlab.com/gitlab-org/gitlab-ce/issues/31640) ni par [Bitbucket](https://jira.atlassian.com/browse/BSERV-10529).
