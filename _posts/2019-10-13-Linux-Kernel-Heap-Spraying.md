---
layout: post
title: "Linux kernel Heap Spraying Techniques"
author: "nonetype"
categories: pwn
tags: linux_kernel
---

# 목차

1. TOC
{:toc}

---

# Heap Spraying

Linux Kernel 취약점 중 UAF 혹은 Heap Overflow 취약점에 대한 Exploit code를 짜게 될 때 힙 스프레잉을 해야 하는 경우가 생기게 된다.
Linux Kernel Exploit은 userspace binary exploit과 다르게 '직접' `kmalloc`을 호출할 수 없으므로 `syscall` 호출을 통해 간접적으로 스프레잉을 진행해야 한다.
이 때 사용하는 `syscall`은 크게 3가지이다.

1. `add_key()`
2. `send[m]msg()`
3. `msgsnd()`


# add_key()


# send[m]msg()


# msgsnd()


# References
Linux Kernel universal heap spray | <https://duasynt.com/blog/linux-kernel-heap-spray>
twitter@Vitaly - add_key() | <https://twitter.com/vnik5287/status/806778450304319489>
Dissecting a 17-year-old kernel bug | <https://cdn2.hubspot.net/hubfs/2518562/beVX/bevx-Dissecting-a-17-year-old-Vitaly-Nikolenko.pdf>
CVE-2017-2636: exploit the race condition in the n_hdlc Linux kernel driver bypassing SMEP | <https://a13xp0p0v.github.io/2017/03/24/CVE-2017-2636.html>
