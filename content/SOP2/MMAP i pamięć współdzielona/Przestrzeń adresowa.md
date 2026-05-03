Kernel reprezentuje przestrzeń adresową każdego procesu jako array mappingów pamięci wewnątrz PCB (Process Control Block)

Każdy mapping ma powiązany zakres adresów (start + length), który definiuje:
- Czy writable, readable, executable?
- Widoczne dla innych procesów?
- Backupowane przez plik na dysku?
![[PROCESS MAPPINGS.png]]

[[procfs - Interfejs Debugowy]] 