Na przykład na 32 bitowym x86 tak tłumaczona jest poniższa instrukcja:
```
#include <stdint.h>

  

uint64_t shared_val = 0;

  

void writer() {

shared_val = 0x0000000100000001ULL;

}

  

void reader() {

uint64_t val = shared_val;

}

// ML:

writer():

mov DWORD PTR shared_val, 1

mov DWORD PTR shared_val+4, 1

ret

reader():

ret

shared_val:

.zero 8
```

Jak można zauważyć wykonane są dwie operacje mov - nie jest ona atomowa.

Na szczęście większość zalignowanych 2,4,8 bajtowych typów na dzisiejszych komputerach jest atomowa. Ponadto software udostępnia odpowiednie biblioteki jak:

```
atomic_store_explicit(&x, 1, memory_order_relaxed);
int ry = atomic_load_explicit(&y, memory_order_relaxed);
```
