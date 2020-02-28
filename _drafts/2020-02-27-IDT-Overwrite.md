---
layout: post
title: "IDT Overwrite in Linux kernel"
author: "nonetype"
categories: pwn
tags: linux_kernel
---

IDT Overwrite and mitigations in Linux Kernel

# 목차


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [목차](#목차)
- [Abstract](#abstract)
- [The IDT](#the-idt)
- [IDT Overwrite](#idt-overwrite)
- [Mitigation](#mitigation)
- [References](#references)

<!-- /code_chunk_output -->


# Abstract
커널에는 다양한 인터럽트가 존재한다. '3 / 0'같은 연산을 수행할 때 발생하는 `Zero-Division Error`, User-mode에서 Kernel-mode로 진입하는 `System call` 등이 대표적인 인터럽트의 예다.

이런 인터럽트가 발생하면, 이를 핸들링 하기 위한 함수를 호출하는데, 이 때 해당 인터럽트의 핸들링 함수를 찾기 위해 사용하는 것이 IDT, 'Interrupt Descriptor Table' 이다.

KASLR이 적용되고 있기 때문에, IDT의 Base Address 또한 가변적이다. 따라서 IDT Base Address는 IDTR(Interrupt Descriptor Table Register)의 값으로 존재하게 된다.
간단하게 다음과 같이 나타낼 수 있다.

{% gist 3015348ffef969a9531c05f333072ac9 %}

http://coffeenix.net/doc/develop/ia-interrupt/ch1-1.html
https://itguava.tistory.com/16
https://wiki.kldp.org/KoreanDoc/html/EmbeddedKernel-KLDP/idt.html
https://flslg.tistory.com/entry/IDT-Interrupt-Descriptor-Table
https://m.blog.naver.com/PostView.nhn?blogId=il0veu2&logNo=56772995&proxyReferer=https%3A%2F%2Fwww.google.com%2F (bookmarked)



# The IDT
https://github.com/NJhyo/bobfuzzer/blob/master/Exploit/NoneType/2019-09-23-Linux-Kernel-Exploit-Development-lab4.md#idt-overwrite

```
(gdb) x/32gx 0xffffffff81dd6000
0xffffffff81dd6000:	0x816a8e0000108120	0x00000000ffffffff
0xffffffff81dd6010:	0x81698e040010edb0	0x00000000ffffffff
0xffffffff81dd6020:	0x81698e030010f1c0	0x00000000ffffffff
0xffffffff81dd6030:	0x8169ee040010edf0	0x00000000ffffffff
0xffffffff81dd6040:	0x816aee0000108140	0x00000000ffffffff
0xffffffff81dd6050:	0x816a8e0000108160	0x00000000ffffffff
0xffffffff81dd6060:	0x816a8e0000108180	0x00000000ffffffff
0xffffffff81dd6070:	0x816a8e00001081a0	0x00000000ffffffff
0xffffffff81dd6080:	0x816a8e02001081c0	0x00000000ffffffff
0xffffffff81dd6090:	0x816a8e00001081f0	0x00000000ffffffff
0xffffffff81dd60a0:	0x816a8e0000108210	0x00000000ffffffff
0xffffffff81dd60b0:	0x816a8e0000108240	0x00000000ffffffff
0xffffffff81dd60c0:	0x81698e010010ee30	0x00000000ffffffff
0xffffffff81dd60d0:	0x81698e000010eed0	0x00000000ffffffff
0xffffffff81dd60e0:	0x81698e000010ef00	0x00000000ffffffff
0xffffffff81dd60f0:	0x816a8e0000108270	0x00000000ffffffff
(gdb)
```
<!--![55392467](https://i.imgur.com/XmpVSvW.jpg)-->

# IDT Overwrite
https://resources.infosecinstitute.com/hooking-idt/#gref

# Mitigation
https://kernsec.org/wiki/index.php/Exploit_Methods/Function_pointer_overwrite

# References