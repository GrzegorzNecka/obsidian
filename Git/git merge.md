
### merge 

git merge pozwala połączyć całe 2 gałęzie - jeśli jestem na master to pozwala połączyć gałąź lub commit o nazwie nazwa_brancha  masterem. Git sam znajdzie wspólny punkt w którym można połączyć się oraz commity które połączyć 


```bash

git merge nazwa_brancha

```


![[Pasted image 20240312085141.png]]

### konflikty

konflikty pojawiają się wtedy kiedy plik zostanie zmieniony równocześnie przez kilka osób a dokładniej mówiąc kiedy zmienią się te same linie w tym samym czasie powstaną 2 różne commity dla tego samego fragmentu:

```bash
<<< head - zmiany z mastera
===
>>> gałąź2 - zmiany z gałęzi
```


jeśli wszystkie konflikty zostały rozwiązane ale dalej jesteśmy w stanie merge to wtedy `git add` > `git commit`

przerywa bieżący merge

```
git merge --abort
```


### merge rekrusywny

jeśli przesunę się mergem do góry ale po drodze miałem brancha to teraz nie mogę się z nim zmergować. Dlatego git robi dodatkowego commita czołowego z tyłu przed branchem który chcę dodać. Przy takim mergeu pojawi się okno dodatkowe:


![[Pasted image 20240312085346.png]]

w tym oknie trzeba stworzyć dodatkowego commita dla brancha który jest z tyłu aby master mógł się z nim połączyć .... wychodzę `esc: wq`












