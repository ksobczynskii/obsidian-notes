
Załóżmy, że mamy zmienialną strukturę danych we współdzielonej pamięci.

**Reader** - proces, który chce przeczytać dane.
**Writer** - proces musi móc nadpisywać zmiany.

Możemy:
1. Faworyzować czytelników - dopóki czytelnik jest pozwalamy nowym wchodzić.
2. Faworyzować piszących - dopóki jakiś writer jest nowi cztelnicy są zablokowani.


Rozwiązanie z semaforem:
![[rw-sem.png]]

Rozwiązanie z CV:
![[cv_rdl_writer.png]]
![[cv_rdl_reader.png]]

Warto wspomnieć, że posix implementuje rozwiązanie strukturą RW_lock:
![[rw_lock.png]]
Defaultowo, ten faworyzuje czytelników.