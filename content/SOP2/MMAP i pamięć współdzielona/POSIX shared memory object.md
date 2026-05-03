Ten typ współdzielenia pamięci jest dostępny dla procesów niezależnych, niepowiązanych. Cykl jego życia wygląda następująco:

[[shm_open()]]  - Create/Open the object
ftruncate() -  set the size
mmap() -  map into memory
close() -  close fd (mapping remains)
shm_unlink() - remove object name
