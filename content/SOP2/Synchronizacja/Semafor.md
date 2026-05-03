Zawiera:
-  Counter (Integer)
-  Queue (managed by scheduler)
![[semafor.png]]
Zamiast czekania w pętli, procesy śpią i zwalniają CPU core.

Operacje semafora:
- wait() - dekrementuje counter i jeżeli counter <0 -> trafia do Queue.
- post()/signal() - inkrementuje counter. Jeżeli po inkrementacji negatywny -> budzi czekający proces.

Implementacja:

![[wait_post_sem.png]]

Zauważmy, że mamy tu sekcje krytyczną. Ten typ spinlocku tu jest uzasadniony, gdyż kod jest w pełni pod kontrolą OS oraz kod jest krótki.


Problemy Semafora:
- System Call Overhead - wait() i post() muszą być syscallami -> za każdym wywołaniem jednego z tych przez proces, musi on wejść w kernel mode nawet jeśli sekcja krytyczna jest wolna.