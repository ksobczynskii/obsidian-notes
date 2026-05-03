Funkcja mapująca plik (jego pamięć) do przestrzeni adresowej procesu, aby proces mógł zmieniać i dobierać się do jego zawartości poprzez operacje na pamięci.
![[MemoryFileMappings.png]] Składnia mmap():
```
#include <sys/mman.h>
void* addr = mmap(
	NULL, // Address hint (NULL)
	length, // Length of the mapping
	PROT_READ | PROT_WRITE, // Memory Protection Flags
	MAP_SHARED, // Flags (SHared vs Private)
	fd, // descriptor
	offset // offset in file
);
if(addr == MAP_FAILED){ /* ERROR HANDLING*/}
```

[[Flagi Widoczności]] - służą do określenia jak inne procesy mogą obcować z mappingiem
[[Flagi Ochrony Pamięci]] - służą do określenia w jaki sposób możemy posługiwać się mappingiem (Nie może być konfilktu z trybem otwarcia pliku).
