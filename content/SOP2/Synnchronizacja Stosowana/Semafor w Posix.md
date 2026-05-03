POSIX udostępnia API:
- sem_t - typ zawierający semafor.
- sem_open(path), sem_init(&s, val) - sposoby uzyskania semafora do użytku
- sem_wait(&s), sem_post(&s) - funkcje semafora.


Wartość sem_t może leżeć w:
- prywatnej pamięci procesu (stack, heap, global)
- współdzielonej pamięci
- namespace sameforów - szeroki na cały system

Do synchronizacji wątków wewnątrz jednego procesu używamy najczęściej **Semaforów Nienazwanych**. Te żyją w heapie/global/stacku maina i inicjalizuje się je:

```
sem_init(&sem, /*pshared*/0, initial_value)
```

Gdy proces umiera - semafor również.


Do synchronizacji procesów użyjemy już **Semaforów Nienazwanych w SHM**. Taki semafor **MUSI** żyć w regionie współdzielonej pamięci: 

```
sem_init(&sem, /*pshared*/1, initial_value)
```

Zależy kompletnie od współdzielonej pamięci -> po jej usunięciu semafor umiera.

Ostatnim sposobem synchronizacji procesów jest **Semafor Nazwany**. Przydaje się gdy chcemy zsynchronizować nasz program bez współdzielenia pamięci procesów.

```
sem_open("/name", O_CREAT, mode, initial_value)
```

Żyje aż do momentu wywołania *sem_unlink()* lub wyłączenia systemu.

Na Linux nazwane semafory leżą w */dev/shm*. 


### Jak pod spodem wygląda sem_t?

sem_t powinien być traktowany jako czarna skrzynka, ale typowa implementacja glibc wygląda tak:
```
struct internal_sem {
uint64_t data; // [ nwaiters (4b), value (4b) ] 
int private; // `pshared` flag 
int pad; };
```

data jest używany jak *futex word* - porównuje wartość w namespace usera i dopiero potem schodzi do kernel-mode.
#### Czemu pshared? 

Gdy pshared = 0, implementacja zaznacza flagę FUTEX_PRIVATE_FLAG, przez co kernel może zoptymalizować podejście wywoływań wait()/post() 


