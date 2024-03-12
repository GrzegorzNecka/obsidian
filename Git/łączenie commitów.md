git **rebase** lokalnie po takim poleceniu git chce umieścić commity z repo lokalnego po commitach w zdalnym branchu

```bash
git rebase -i HEAD~3
```

zdejmij 3 ostatnie commity na bok i wstaw je po wykonaniu jakieś akcji

przechodzimy do kolejnego widoku - lista todo -tam zamieniamy w edytorze

- **p** - pick - zostawi commit tam gdzie jest
- **r** - reword - zmień nazwę commita
- **e** - edit -
- **s** - squash - łączy commit z poprzednimi commitami w taki sposób zę oba message zostaną połaąćzone i użyte jako message nowego commita
- **f** - fixup - łączy commit z poprzednimi commitami ale nazwa nazywa sięgo od nowa
- **x** - exec - pozwala uruchamiać polecenia za pomocą shella .. po kazym kroku sprawdzi czy aplikacja działa
- **d** - drop - usuwa committa

`esc :wq`

jeśli podczas rebase wywali mi błąd to jedną z opcji kontynuacji jest:

- git **rebase --continue**
- `git rebase --abort` cofa zmiany git rebase