特定のIPアドレスへの通信に対して、自動でVPNを利用するようにする。
ex. IPアドレスで制限がかかっているSSHサーバーにVPN経由で接続するときとか

8.8.8.8が接続先のIPアドレス
ppp0は利用するVPN接続で、ifconfigから調べる

/etc/ppp/ip-up  
/etc/ppp/ip-down

```sh
#!/bin/sh
set -eu

if [ "$1" = "ppp0" ]; then
  /sbin/route add -net 8.8.8.8 -interface ppp0
fi
```

```sh
#!/bin/sh
set -eu

if [ "$1" = "ppp0" ]; then
  /sbin/route delete -net 8.8.8.8
fi
```
