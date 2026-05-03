Syscall odpowiada za zsynchronizowanie mapowanej pamięci i pamięci z dysku - czyli aktualizuje dysk. 

```
if(msync(addr, length, MS_SYNC) == -1)
{
	perror("msync");
}
```

**MS_SYNC** - Blokuje proces aż dane nie zostaną zapisane
**MS_ASYNC** - Scheduluje operacje write i przechodzi do kodu dalszego

