# anonsurf-hacked
dirty anonsurf hack to work with gentoo

this is a code adopted (dirty) from anonsurf repo to work with gentoo. this will need 'some love' in the future.

to use this hacked bit copy content to your system and start with: ``` /etc/init.d/anondaemon restart ```

please check firewall configuration with: ``` iptables -L ```
the output should look like this:

```

┌─[root@arrakis]─[/]
└──╼ #iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     all  --  anywhere             anywhere             state ESTABLISHED
ACCEPT     all  --  anywhere             anywhere            
DROP       all  --  anywhere             anywhere            
ACCEPT     all  --  anywhere             localhost           

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
DROP       all  --  anywhere             anywhere            

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     all  --  anywhere             192.168.0.0/16      
ACCEPT     all  --  anywhere             172.16.0.0/12       
ACCEPT     all  --  anywhere             10.0.0.0/8          
ACCEPT     all  --  anywhere             127.0.0.0/9         
ACCEPT     all  --  anywhere             127.128.0.0/10      
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     all  --  anywhere             anywhere             owner UID match tor
REJECT     all  --  anywhere             anywhere             reject-with icmp-port-unreachable
DROP       all  --  anywhere             anywhere             state INVALID
ACCEPT     all  --  anywhere             anywhere             state ESTABLISHED
ACCEPT     tcp  --  anywhere             anywhere             owner UID match tor tcp flags:FIN,SYN,RST,ACK/SYN state NEW
ACCEPT     all  --  anywhere             localhost           
ACCEPT     tcp  --  anywhere             localhost            tcp dpt:9040 flags:FIN,SYN,RST,ACK/SYN

```

you can also check connections with: ``` watch -n 0.1 netstat -tupano ```
it should look more/less like this:

```

┌─[root@arrakis]─[/]
└──╼ #netstat -tupano
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name     Timer
tcp        0      0 127.0.0.1:9040          0.0.0.0:*               LISTEN      149508/tor           off (0.00/0/0)
tcp        0      0 127.0.0.1:8118          0.0.0.0:*               LISTEN      4801/privoxy         off (0.00/0/0)
tcp        0      0 127.0.0.1:9050          0.0.0.0:*               LISTEN      149508/tor           off (0.00/0/0)
tcp        0      0 127.0.0.1:9051          0.0.0.0:*               LISTEN      149508/tor           off (0.00/0/0)
tcp        0      0 127.0.0.1:9054          0.0.0.0:*               LISTEN      149508/tor           off (0.00/0/0)
udp        0      0 127.0.0.1:53            0.0.0.0:*                           149508/tor           off (0.00/0/0)

```

portage will work without modifications so you can emerge without additional changes in make.conf
