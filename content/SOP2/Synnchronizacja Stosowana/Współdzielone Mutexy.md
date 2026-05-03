Inne prymitywy synchronizujące również mogą być używane przez wiele procesów na raz, jeżeli są w jednym mapping pamięci współdzielonej.

```
pthread_mutexattr_t attr;
pthread_mutexattr_init(&attr); // Tell the OS that the mutex will be shared pthread_mutexattr_setpshared(&attr, PTHREAD_PROCESS_SHARED);
pthread_mutex_init(&shm_ptr->mutex, &attr);
pthread_mutexattr_destroy(&attr);
```


#### Położenie mutexów.

Tak jak w semaforach, wartość mutexa, która chroni pamięci współdzielonej, zazwyczaj leży w tym samym segmencie pamięci co chronione dane.

```
struct shm_layout {
pthread_mutex_t mtx;// protects everything!
int active_processes; 
int pids[MAX_PROCESSES]; 
// ... 
}; 
struct shm_layout* shm = mmap(...);
```

Mutexa inicjalizujemy jednokrotnie, zazwyczaj robi to twórca pamięci współdzielonej.


#### Typy mutexów.
Jako że standardowy mutex jest dość głupi i podatny na deadlocki, istnieją typy inicjalizacji, które możemy nadać mutexowi (czy też barierom, cv, etc..). Przykładowo:
- Error Checking - chroni przed double - lockiem i zwraca EDEADLK
- Rekursywny - wewnątrz procesu ilość locków == ilość unlocków oraz można wywołać locka wielokrotnie pod rząd. Przydatny do struktów drzewowych, rekursywnych.


### Co Jeżeli owner mutexa umiera?

W takim wypadku ze standardowym mutexem, jeżeli owner zawołał lock i umarł -> mutex w shm pozostaje zablokowany na zawsze. Reszta procesów wisi i czeka w nieskończoność.

Rozwiązanie - **Robust Mutex**.

Kernel śledzi kto jest właścicielem mutexa. Gdy proces umrze trzymając mutexa - kernel wybudza następny czekający proces. lock() zwraca EOWNERDEAD. Wybudzony, może wywołać pthread_mutex_consistent() i przywrócić mutex do życia stając się jego nowym właścicielem.

Brak wykonania pthread_mutex_consistent() skutkuje tym, że mutex jest już permamentnie zepsuty i każdy następny lock() zwróci ENOTRECOVERABLE.