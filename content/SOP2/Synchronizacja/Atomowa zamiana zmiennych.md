Mamy możliwość zamiany zmiennej z miejscem w pamięci w sposób atomowy. Ten kod:
```
int atomic_swap(int *mem, int new_value)
{
int old = *mem
*mem = new_value;
return old;
}
``` 

Tłumaczy się:

```
xchg eax, DWORD PTR mem[rip]
```

Jedna, atomowa instrukcja w języku maszynowym.