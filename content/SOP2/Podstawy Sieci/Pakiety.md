Aby zerknąć co dzieje się w sieci można użyć narzędzia *tcpdump*:
![[tcpdump.png]]
 
 Wypisuje ono linie na pakiet i opisuje jego znaczenie:

![[tcpdump_logs.png]]

Wyjście programu można przykładowo zobarzować graficznie w **wireshark**.


Przykład: HTTP Request

```
echo -ne "GET / HTTP/1.1\r\nHost: mini.pw.edu.pl\r\n\r\n" \ | nc mini.pw.edu.pl 80
```
![[http_dump.png]]