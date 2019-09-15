---
layout: post
title: "Linux Kernel debugging with Qemu"
author: "nonetype"
---



리눅스 커널 디버깅!



#### Linux Kernel Build
https://mirrors.edge.kernel.org/pub/linux/kernel/v4.x/ 에서 원하는 버전의 커널을 다운로드 받고, 압축 해제한다.

`make defconfig`
`make kvmconfig`
`make menuconfig` 명령을 실행한다.

이후 나타나는 창에서 `Kernel Hacking - Compile-time checks and compiler options - compile the kernel with debug info` 체크, `Kernel Hacking - Choose kernel unwinder (Frame pointer unwinder) - Frame pointer unwinder` 체크, `Processor type and Features - Randomize the address of the kernel image (KASLR)` 체크 해제 후 나와서 `make` 명령을 실행한다.

#### Root FileSystem Build

`git clone git://git.buildroot.net/buildroot`
`cd buildroot`
`make menuconfig`
`Target options -> Target Architecture -> x86_64` 체크
`FileSystem images -> ext2/3/4 root filesystem (NEW)` 체크
`ext2/3/4 variant (ext4)` 에서 루트 파일 시스템으로 사용할 파일 시스템 선택 (나는 ext4를 선택했다.)
나와서 `make clean && make -j16`





#### References
https://tistory.0wn.kr/368

https://woodz.tistory.com/72

https://willow72.tistory.com/entry/qemu-gdb-%EC%97%B0%EB%8F%99

https://blog.naver.com/ultract2/221230988537

https://satanel001.tistory.com/183
