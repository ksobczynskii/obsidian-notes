
Kompilator nie tłumaczy kodu dosłownie. Przykładowo:

```
int data = 0;

int ready = 0;

  

void th1() {

data = 42; // Operacja A

ready = 1; // Operacja B

}

  

int th2() {

while (ready == 0) {

// Aktywne czekanie (busy-wait) - Operacja C

}

return data; // Operacja D

}
```

Jest tłumaczone na: 

```
th1():

mov DWORD PTR data[rip], 42

mov DWORD PTR ready[rip], 1

ret

th2():

mov eax, DWORD PTR data[rip]

ret

ready:

.zero 4

data:

.zero 4
```

Kompilator może w teorii zrobić z kodem co chce, dopóki obserwowalne efekty wykonania jednowątkowego programu pozostają takie same.

- Zmienne cache mogą zaburzyć kolejność
- Linijki kodu mogą zostać usunięte (dead code)
- agresywna optymalizacja pętli