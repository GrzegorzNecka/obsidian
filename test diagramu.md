

```mehrmaid
flowchart LR
A --> C
B --> D
C & D --> E
E --> F & G
F --> H
G --> J
subgraph X ["$X$"]
A(("$A$"))
end
subgraph id1 ["$Y$"]
G(("$G$"))
end
subgraph id3 ["$Z$"]
E(("$E$"))
end
C(("$C$"))
D(("$D$"))
F(("$F$"))
B(("$B$"))
H(("$H$"))
J(("$J$"))
```






```mermaid
flowchart LR
    Start((Start)) --> GetCartIdFromCookie[Pobierz ID koszyka\n z ciastka]
    GetCartIdFromCookie --> HasCartIdCookie{Czy ID było w ciastku?}

    HasCartIdCookie -->|Tak| GetCartById[Pobierz koszyk z API]
    HasCartIdCookie -->|Nie| CreateCart
    GetCartById--> DoesCartExist{Czy koszyk\n istnieje?}

    DoesCartExist-->|Tak| End
    DoesCartExist-->|Nie| CreateCart[Stwórz koszyk w API]

    CreateCart-->SetCartCookie[Ustaw ciastko\n z ID koszyka]-->End

    End((Zwróć koszyk))

```

