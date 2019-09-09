---
layout: post
title: "Linux Kernel debugging with Vmware"
author: "nonetype"
---

## Stage 1 - vmx configure

Debugging 할 VM의 경로로 이동해서 .vmx 파일의 마지막 줄에 다음 라인을 추가한다.
```sh
debugStub.listen.guest32 = 1
```

.vmx 파일 저장 후 guest OS를 부팅한다.

## Stage 2 - guest OS Setting

`sudo apt-get update && sudo apt-get upgrade` 명령을 통해 패키지 업그레이드를 진행한다.

이후 다음 명령을 실행한다.
```sh
echo "deb http://ddebs.ubuntu.com $(lsb_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-proposed main restricted universe multiverse" | \
sudo tee -a /etc/apt/sources.list.d/ddebs.list
```

Ubuntu 18.04
```sh
sudo apt install ubuntu-dbgsym-keyring
```
Ubuntu 16.04
```sh
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F2EDC64DC5AEE1F6B9C621F0C8CAB6595FDFF622
```

심볼 설치!
```sh
sudo apt-get update
sudo apt-get install linux-image-`uname -r`-dbgsym
```

이후 `/usr/lib/debug/boot` 디렉토리를 확인해 보면 다음과 같이 나타난다.
```sh
debug@debug-virtual-machine:~$ ls /usr/lib/debug/boot/
vmlinux-4.15.0-45-generic
debug@debug-virtual-machine:~$
```

이 파일을 호스트(debugger를 실행할)로 옮겨주고, GDB를 또 컴파일하긴 귀찮으니 IDA로 깐다.




## References
http://jidanhunter.blogspot.com/2015/01/linux-kernel-debugging-with-vmware-and.html
https://wiki.ubuntu.com/Debug%20Symbol%20Packages