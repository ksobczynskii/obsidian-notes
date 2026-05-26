Intencja:
Współdzielenie wielu małych, lekkich obiektów. Nie duplikować danych.

Struktura:
![[Zrzut ekranu 2026-05-25 o 18.22.25.png]]

Przykładowo:
- Zamiast Robić Klasę Enemy która zawiera położenia, wygląd, damage, health etc., Można w implementacji klasy Enemy rozdzielić to na zmienne (damage, health, położenie) oraz stałe (Nazwa, Wygląd). Wtedy Tworząc np new Rat(...), nie ma potrzeby przechowywać Nazwy czy wyglądu dla każdego Rat, tylko można podawać w konstruktorze Rat(x = 1, y = 1, type=EnemyType.Rat).