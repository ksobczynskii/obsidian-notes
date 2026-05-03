Tworzenie obiektu wygląda następująco:
![[SHM_OPEN.png]]

Warto zaznaczyć, że mimo że odwołujemy się do obiektu shm jak gdyby był plikiem na dysku, to "/my_data" nie istnieje rzeczywiscie w filesystemie. Mają osobny root i tworzą płaskie drzewo:![[SHM NAMESPACE.png]]


Używać obiektu shm poprzez mapping możemy w następujący sposób:

![[MMAP SHM.png]]

POSIX SHM ma tzw *kernel persistence* - istnieją do rebootu systemu lub do zawołania unlink. ![[SHM_UNLINK.png]]