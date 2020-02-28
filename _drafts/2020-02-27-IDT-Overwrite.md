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
![55392467](https://i.imgur.com/XmpVSvW.jpg)

# IDT Overwrite
https://resources.infosecinstitute.com/hooking-idt/#gref

# Mitigation
https://kernsec.org/wiki/index.php/Exploit_Methods/Function_pointer_overwrite

# References