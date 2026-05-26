![[Zrzut ekranu 2026-05-25 o 22.41.06.png]]

1) Kowariancja - ta sama strone zależności.
2) Kontrawariancja - przeciwna strona zależności
3) Inwariancja - równość klas (X' = X)



- T a T' -> Kontrawariancja i Inwariancja działają, kowariancja nie, bo okraja działanie klasy. (Uwaga może się wydawać, że danie klasy bazowej, okrojonej do metody która przyjmuje już poszerzoną nie powinno zadziałać, ale dobrze napisane klasy powinny to obsługiwać)
- S a S' -> Kowariancja i Inwariancja -> pasuje bo podklasa S' to też S (polimorfizm). Kontrawariancja nie, bo klient dostaje informacje, że operuje na innej klasie niż ma.
- U a U' -> tylko inwariancja
