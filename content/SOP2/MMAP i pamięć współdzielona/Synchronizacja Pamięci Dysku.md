![[DISK SYNCHRONIZATION.png]]
Po nadpisaniu pamięci w mappingu jądro oznacza region pamięci jako DIRTY oraz cyklicznie co cykl CPU skanuje tak oznaczone regiony i modyfikuje odpowiednie części pliku na dysku/

Jeżeli chcemy mieć pewność, że w danym momencie kodu zmiany zostały zapisane, możemy użyć syscalla [[msync()]] 