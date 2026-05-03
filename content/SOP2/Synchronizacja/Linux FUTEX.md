
Inaczej Fast userspace mutex.

Rozwiązanie hybrydowe:
- Szybkość atomowych rozwiązań spinlock gdy pusty CS.
- Możliwości spania jak w semaforze gdy zabrana CS.


Jak działa Futex?

Implementujemy go zwyczajnie jako 32-bitowy integer w dzielonej pamięci.
Kernel trzyma listę oczekujących.

![[implementacja futexa.png]]


Syscall może robić różne rzeczy w zależności od operatora op:
- dla op = FUTEX_WAIT - blokuje proces (dodaje do listy oczekujących)
- op = FUTEX_WAKE - budzi pierwszy z listy śpiących procesów.

implementacja kernela porównuje wartość futexa do tej, którą wskazuje proces. Syscall fast-failuje gdy się nie zgadzają.
![[futex_call.png]]

Korzystając z futexa możemy zaimplementować mutex w taki sposób (uproszczenie):
![[mutex_by_futex.png]]


W zaawansowanej implementacji, mutex ma stany: 0 - wolny, 1 - zajety, 2 - zajety z potencjalnymi oczekującymi.
