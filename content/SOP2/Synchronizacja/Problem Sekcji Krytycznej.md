![[CS PROBLEM.png]]

Rozwiązanie problemu sekcji krytycznej łączy 3 wymogi:
- Mutual Exclusion - maksymalnie jeden process może być w critical section
- Progres - Jeśli CS jest wolne i procesy czekają w waiting section - jeden w końcu wejdzie (nie może być wiecznego czekania na sekcje krytyczną)
- Limit wejść w sekcje krytyczną - Proces nie może wchodzić w sekcje krytyczną w nieskończoność

Rozwiązanie teorytyczne - [[Algorytm Petersona]] 