Współczesne CPU udostępniają możliwości **Atomowych Instrukcji** do zapewnienia rozwiązania problemów atomowości, kolejności etc.

Przykładowo - [[Atomowa zamiana zmiennych]]. Za jej pomocą możemy zaimplementować już pierwszy system typu lock - Spinlock z atomowym swapem:
![[atomic_swap_spinlock.png]]


Spinlocka możemy zaimplementować za pomocą [[TAS - Test And Swap]]:
![[tas_spinlock.png]]

Możemy użyć jeszcze innego rozwiązania, czyli [[CAS - Compare And Swap]]. TAS jest wystarczający dla spinlocka, ale CAS pozwala na zaimplementowanie trudniejszych problemów programowania współbieżnego.


Spinlocki jednak mają wady:
- Nie oferują równego rozmieszczenia wejść procesu w blok kodu - Bounded Waiting może być niespełniony.
- Busy Waiting - zajmujemy CPU czekając na zwolnienie sekcji krytycznej.


Istnieją jeszcze inne sposoby - [[Schematy śpiące]] 