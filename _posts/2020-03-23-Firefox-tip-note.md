---
layout: post
title: "Firefox tip note"
author: "nonetype"
categories: pwn
tags: browsers pwn_tips
---

Tip note for Firefox analysis & exploitation

# Index

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Index](#index)
- [Firefox note](#firefox-note)
  - [Build](#build)
- [Troubleshooting](#troubleshooting)
  - [TypeError: cannot create 'NoneType' instances while js/src/configure](#typeerror-cannot-create-nonetype-instances-while-jssrcconfigure)
    - [Solution](#solution)
  - [ERROR: Cannot find llvm-objdump](#error-cannot-find-llvm-objdump)
    - [Solution](#solution-1)
  - [ERROR: Could not find autoconf 2.13](#error-could-not-find-autoconf-213)
    - [Solution](#solution-2)
- [References](#references)

<!-- /code_chunk_output -->

# Firefox note

## Build

Firefox 소스 코드는 [여기](https://ftp.mozilla.org/pub/firefox/releases/72.0/source/)에서 받을 수 있다. (`ftp.mozilla.org/pub/firefox/releases/version to build/source`)

```bash
tar -xvf firefox-[version].source.tar.xz
sudo apt-get install python-pip gcc make g++ perl python autoconf -y
sudo apt install rustc cargo
sudo apt install llvm
sudo apt install autoconf2.13
mkdir build-[version]
cd build-[version]
../firefox-[version]/js/src/configure
make
./dist/bin/js
```

이후 `js> ` 형식의 인터프리터 쉘 창이 뜨면 성공!

# Troubleshooting

## TypeError: cannot create 'NoneType' instances while js/src/configure

```bash
 nonetype@box  ~/hack/browser/firefox/build  ../firefox-72.0/js/src/configure
Reexecuting in the virtualenv
checking for vcs source checkout... no
checking for a shell... /bin/sh
checking for host system type... x86_64-pc-linux-gnu
checking for target system type... x86_64-pc-linux-gnu
checking for Python 3... /usr/bin/python3 (3.6.9)
checking whether cross compiling... no
checking for yasm... not found
checking for the target C compiler... /usr/bin/gcc
checking whether the target C compiler can be used... yes
checking the target C compiler version... 7.5.0
checking the target C compiler works... yes
checking for the target C++ compiler... /usr/bin/g++
checking whether the target C++ compiler can be used... yes
checking the target C++ compiler version... 7.5.0
checking the target C++ compiler works... yes
checking for the host C compiler... /usr/bin/gcc
checking whether the host C compiler can be used... yes
checking the host C compiler version... 7.5.0
checking the host C compiler works... yes
checking for the host C++ compiler... /usr/bin/g++
checking whether the host C++ compiler can be used... yes
checking the host C++ compiler version... 7.5.0
checking the host C++ compiler works... yes
checking for 64-bit OS... yes
checking for nasm... not found
checking for linker... bfd
checking for the assembler... /usr/bin/gcc
checking for ar... /usr/bin/ar
checking for pkg_config... /usr/bin/pkg-config
checking for pkg-config version... 0.29.1
checking for stdint.h... yes
checking for inttypes.h... yes
checking for malloc.h... yes
checking for alloca.h... yes
checking for sys/byteorder.h... no
checking for getopt.h... yes
checking for unistd.h... yes
checking for nl_types.h... yes
checking for cpuid.h... yes
checking for sys/statvfs.h... yes
checking for sys/statfs.h... yes
checking for sys/vfs.h... yes
checking for sys/mount.h... yes
checking for sys/quota.h... yes
checking for linux/quota.h... yes
checking for linux/if_addr.h... yes
checking for linux/rtnetlink.h... yes
checking for sys/queue.h... yes
checking for sys/types.h... yes
checking for netinet/in.h... yes
checking for byteswap.h... yes
checking for linux/perf_event.h... yes
checking for perf_event_open system call... yes
checking whether the C compiler supports -Wbitfield-enum-conversion... no
checking whether the C++ compiler supports -Wbitfield-enum-conversion... no
checking whether the C compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C++ compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C compiler supports -Wunreachable-code-return... no
checking whether the C++ compiler supports -Wunreachable-code-return... no
checking whether the C compiler supports -Wclass-varargs... no
checking whether the C++ compiler supports -Wclass-varargs... no
checking whether the C compiler supports -Wfloat-overflow-conversion... no
checking whether the C++ compiler supports -Wfloat-overflow-conversion... no
checking whether the C compiler supports -Wfloat-zero-conversion... no
checking whether the C++ compiler supports -Wfloat-zero-conversion... no
checking whether the C compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wc++1z-compat... yes
checking whether the C++ compiler supports -Wc++2a-compat... no
checking whether the C++ compiler supports -Wcomma... no
checking whether the C compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wimplicit-fallthrough... yes
checking whether the C compiler supports -Wstring-conversion... no
checking whether the C++ compiler supports -Wstring-conversion... no
checking whether the C compiler supports -Wtautological-overlap-compare... no
checking whether the C++ compiler supports -Wtautological-overlap-compare... no
checking whether the C compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-inline-new-delete... no
checking whether the C compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C++ compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C++ compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C compiler supports -Wno-error=array-bounds... yes
checking whether the C++ compiler supports -Wno-error=array-bounds... yes
checking whether the C compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C++ compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C compiler supports -Wno-error=backend-plugin... no
checking whether the C++ compiler supports -Wno-error=backend-plugin... no
checking whether the C compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C++ compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C compiler supports -Wno-error=multistatement-macros... no
checking whether the C++ compiler supports -Wno-error=multistatement-macros... no
checking whether the C compiler supports -Wno-error=return-std-move... no
checking whether the C++ compiler supports -Wno-error=return-std-move... no
checking whether the C compiler supports -Wno-error=class-memaccess... no
checking whether the C++ compiler supports -Wno-error=class-memaccess... no
checking whether the C compiler supports -Wno-error=atomic-alignment... no
checking whether the C++ compiler supports -Wno-error=atomic-alignment... no
checking whether the C compiler supports -Wno-error=deprecated-copy... no
checking whether the C++ compiler supports -Wno-error=deprecated-copy... no
checking whether the C compiler supports -Wformat... yes
checking whether the C++ compiler supports -Wformat... yes
checking whether the C compiler supports -Wformat-security... yes
checking whether the C++ compiler supports -Wformat-security... yes
checking whether the C compiler supports -Wformat-overflow=2... yes
checking whether the C++ compiler supports -Wformat-overflow=2... yes
checking whether the C compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-noexcept-type... yes
checking whether the C++ compiler supports -fno-sized-deallocation... yes
checking whether the C++ compiler supports -fno-aligned-new... yes
checking for rustc... not found
checking for cargo... not found
Traceback (most recent call last):
  File "../firefox-72.0/js/src/../../configure.py", line 170, in <module>
    sys.exit(main(sys.argv))
  File "../firefox-72.0/js/src/../../configure.py", line 46, in main
    sandbox.run(os.path.join(os.path.dirname(__file__), 'moz.configure'))
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 499, in run
    func(*args)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 543, in _value_for
    return self._value_for_depends(obj)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/util.py", line 997, in method_call
    cache[args] = self.func(instance, *args)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 552, in _value_for_depends
    value = obj.result()
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/util.py", line 997, in method_call
    cache[args] = self.func(instance, *args)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 155, in result
    return self._func(*resolved_args)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 1152, in wrapped
    return new_func(*args, **kwargs)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/build/moz.configure/rust.configure", line 59, in unwrap
    (retcode, stdout, stderr) = get_cmd_output(prog, '+stable')
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/configure/__init__.py", line 1152, in wrapped
    return new_func(*args, **kwargs)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/build/moz.configure/util.configure", line 30, in get_cmd_output
    log.debug('Executing: `%s`', quote(*args))
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/shellutil.py", line 210, in quote
    return ' '.join(_quote(s) for s in strings)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/shellutil.py", line 210, in <genexpr>
    return ' '.join(_quote(s) for s in strings)
  File "/home/nonetype/hack/browser/firefox/firefox-72.0/python/mozbuild/mozbuild/shellutil.py", line 198, in _quote
    return t("'%s'") % s.replace(t("'"), t("'\\''"))
TypeError: cannot create 'NoneType' instances
```

[reference](https://bugzilla.mozilla.org/show_bug.cgi?id=1598642): rustc and cargo aren't installed

### Solution

```bash
sudo apt install rustc cargo
```

## ERROR: Cannot find llvm-objdump

```bash
 nonetype@box  ~/hack/browser/firefox/build  ../firefox-72.0/js/src/configure
Reexecuting in the virtualenv
checking for vcs source checkout... no
checking for a shell... /bin/sh
checking for host system type... x86_64-pc-linux-gnu
checking for target system type... x86_64-pc-linux-gnu
checking for Python 3... /usr/bin/python3 (3.6.9)
checking whether cross compiling... no
checking for yasm... not found
checking for the target C compiler... /usr/bin/gcc
checking whether the target C compiler can be used... yes
checking the target C compiler version... 7.5.0
checking the target C compiler works... yes
checking for the target C++ compiler... /usr/bin/g++
checking whether the target C++ compiler can be used... yes
checking the target C++ compiler version... 7.5.0
checking the target C++ compiler works... yes
checking for the host C compiler... /usr/bin/gcc
checking whether the host C compiler can be used... yes
checking the host C compiler version... 7.5.0
checking the host C compiler works... yes
checking for the host C++ compiler... /usr/bin/g++
checking whether the host C++ compiler can be used... yes
checking the host C++ compiler version... 7.5.0
checking the host C++ compiler works... yes
checking for 64-bit OS... yes
checking for nasm... not found
checking for linker... bfd
checking for the assembler... /usr/bin/gcc
checking for ar... /usr/bin/ar
checking for pkg_config... /usr/bin/pkg-config
checking for pkg-config version... 0.29.1
checking for stdint.h... yes
checking for inttypes.h... yes
checking for malloc.h... yes
checking for alloca.h... yes
checking for sys/byteorder.h... no
checking for getopt.h... yes
checking for unistd.h... yes
checking for nl_types.h... yes
checking for cpuid.h... yes
checking for sys/statvfs.h... yes
checking for sys/statfs.h... yes
checking for sys/vfs.h... yes
checking for sys/mount.h... yes
checking for sys/quota.h... yes
checking for linux/quota.h... yes
checking for linux/if_addr.h... yes
checking for linux/rtnetlink.h... yes
checking for sys/queue.h... yes
checking for sys/types.h... yes
checking for netinet/in.h... yes
checking for byteswap.h... yes
checking for linux/perf_event.h... yes
checking for perf_event_open system call... yes
checking whether the C compiler supports -Wbitfield-enum-conversion... no
checking whether the C++ compiler supports -Wbitfield-enum-conversion... no
checking whether the C compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C++ compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C compiler supports -Wunreachable-code-return... no
checking whether the C++ compiler supports -Wunreachable-code-return... no
checking whether the C compiler supports -Wclass-varargs... no
checking whether the C++ compiler supports -Wclass-varargs... no
checking whether the C compiler supports -Wfloat-overflow-conversion... no
checking whether the C++ compiler supports -Wfloat-overflow-conversion... no
checking whether the C compiler supports -Wfloat-zero-conversion... no
checking whether the C++ compiler supports -Wfloat-zero-conversion... no
checking whether the C compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wc++1z-compat... yes
checking whether the C++ compiler supports -Wc++2a-compat... no
checking whether the C++ compiler supports -Wcomma... no
checking whether the C compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wimplicit-fallthrough... yes
checking whether the C compiler supports -Wstring-conversion... no
checking whether the C++ compiler supports -Wstring-conversion... no
checking whether the C compiler supports -Wtautological-overlap-compare... no
checking whether the C++ compiler supports -Wtautological-overlap-compare... no
checking whether the C compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-inline-new-delete... no
checking whether the C compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C++ compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C++ compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C compiler supports -Wno-error=array-bounds... yes
checking whether the C++ compiler supports -Wno-error=array-bounds... yes
checking whether the C compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C++ compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C compiler supports -Wno-error=backend-plugin... no
checking whether the C++ compiler supports -Wno-error=backend-plugin... no
checking whether the C compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C++ compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C compiler supports -Wno-error=multistatement-macros... no
checking whether the C++ compiler supports -Wno-error=multistatement-macros... no
checking whether the C compiler supports -Wno-error=return-std-move... no
checking whether the C++ compiler supports -Wno-error=return-std-move... no
checking whether the C compiler supports -Wno-error=class-memaccess... no
checking whether the C++ compiler supports -Wno-error=class-memaccess... no
checking whether the C compiler supports -Wno-error=atomic-alignment... no
checking whether the C++ compiler supports -Wno-error=atomic-alignment... no
checking whether the C compiler supports -Wno-error=deprecated-copy... no
checking whether the C++ compiler supports -Wno-error=deprecated-copy... no
checking whether the C compiler supports -Wformat... yes
checking whether the C++ compiler supports -Wformat... yes
checking whether the C compiler supports -Wformat-security... yes
checking whether the C++ compiler supports -Wformat-security... yes
checking whether the C compiler supports -Wformat-overflow=2... yes
checking whether the C++ compiler supports -Wformat-overflow=2... yes
checking whether the C compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-noexcept-type... yes
checking whether the C++ compiler supports -fno-sized-deallocation... yes
checking whether the C++ compiler supports -fno-aligned-new... yes
checking for rustc... /usr/bin/rustc
checking for cargo... /usr/bin/cargo
checking rustc version... 1.39.0
checking cargo version... 1.39.0
checking for rust target triplet... x86_64-unknown-linux-gnu
checking for rust host triplet... x86_64-unknown-linux-gnu
checking for rustdoc... /usr/bin/rustdoc
checking for rustfmt... not found
checking for clang for bindgen... not found
checking for libclang for bindgen... not found
checking bindgen cflags... -x c++ -fno-sized-deallocation -fno-aligned-new -DTRACING=1 -DIMPL_LIBXUL -DMOZILLA_INTERNAL_API -DRUST_BINDGEN -DOS_POSIX=1 -DOS_LINUX=1
checking for llvm_profdata... not found
checking for awk... /usr/bin/gawk
checking for perl... /usr/bin/perl
checking for minimum required perl version >= 5.006... 5.026001
checking for full perl installation... yes
checking for gmake... /usr/bin/make
checking for watchman... not found
checking for xargs... /usr/bin/xargs
checking for rpmbuild... /usr/bin/rpmbuild
checking for llvm-objdump... not found
DEBUG: llvm_objdump: Trying llvm-objdump
ERROR: Cannot find llvm-objdump
```

### Solution

```bash
sudo apt install llvm
```

## ERROR: Could not find autoconf 2.13

```bash
 nonetype@box  ~/hack/browser/firefox/build  ../firefox-72.0/js/src/configure
Reexecuting in the virtualenv
checking for vcs source checkout... no
checking for a shell... /bin/sh
checking for host system type... x86_64-pc-linux-gnu
checking for target system type... x86_64-pc-linux-gnu
checking for Python 3... /usr/bin/python3 (3.6.9)
checking whether cross compiling... no
checking for yasm... not found
checking for the target C compiler... /usr/bin/gcc
checking whether the target C compiler can be used... yes
checking the target C compiler version... 7.5.0
checking the target C compiler works... yes
checking for the target C++ compiler... /usr/bin/g++
checking whether the target C++ compiler can be used... yes
checking the target C++ compiler version... 7.5.0
checking the target C++ compiler works... yes
checking for the host C compiler... /usr/bin/gcc
checking whether the host C compiler can be used... yes
checking the host C compiler version... 7.5.0
checking the host C compiler works... yes
checking for the host C++ compiler... /usr/bin/g++
checking whether the host C++ compiler can be used... yes
checking the host C++ compiler version... 7.5.0
checking the host C++ compiler works... yes
checking for 64-bit OS... yes
checking for nasm... not found
checking for linker... bfd
checking for the assembler... /usr/bin/gcc
checking for ar... /usr/bin/ar
checking for pkg_config... /usr/bin/pkg-config
checking for pkg-config version... 0.29.1
checking for stdint.h... yes
checking for inttypes.h... yes
checking for malloc.h... yes
checking for alloca.h... yes
checking for sys/byteorder.h... no
checking for getopt.h... yes
checking for unistd.h... yes
checking for nl_types.h... yes
checking for cpuid.h... yes
checking for sys/statvfs.h... yes
checking for sys/statfs.h... yes
checking for sys/vfs.h... yes
checking for sys/mount.h... yes
checking for sys/quota.h... yes
checking for linux/quota.h... yes
checking for linux/if_addr.h... yes
checking for linux/rtnetlink.h... yes
checking for sys/queue.h... yes
checking for sys/types.h... yes
checking for netinet/in.h... yes
checking for byteswap.h... yes
checking for linux/perf_event.h... yes
checking for perf_event_open system call... yes
checking whether the C compiler supports -Wbitfield-enum-conversion... no
checking whether the C++ compiler supports -Wbitfield-enum-conversion... no
checking whether the C compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C++ compiler supports -Wshadow-field-in-constructor-modified... no
checking whether the C compiler supports -Wunreachable-code-return... no
checking whether the C++ compiler supports -Wunreachable-code-return... no
checking whether the C compiler supports -Wclass-varargs... no
checking whether the C++ compiler supports -Wclass-varargs... no
checking whether the C compiler supports -Wfloat-overflow-conversion... no
checking whether the C++ compiler supports -Wfloat-overflow-conversion... no
checking whether the C compiler supports -Wfloat-zero-conversion... no
checking whether the C++ compiler supports -Wfloat-zero-conversion... no
checking whether the C compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wloop-analysis... no
checking whether the C++ compiler supports -Wc++1z-compat... yes
checking whether the C++ compiler supports -Wc++2a-compat... no
checking whether the C++ compiler supports -Wcomma... no
checking whether the C compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wduplicated-cond... yes
checking whether the C++ compiler supports -Wimplicit-fallthrough... yes
checking whether the C compiler supports -Wstring-conversion... no
checking whether the C++ compiler supports -Wstring-conversion... no
checking whether the C compiler supports -Wtautological-overlap-compare... no
checking whether the C++ compiler supports -Wtautological-overlap-compare... no
checking whether the C compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-enum-zero-compare... no
checking whether the C compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C++ compiler supports -Wtautological-unsigned-zero-compare... no
checking whether the C compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-error=tautological-type-limit-compare... no
checking whether the C++ compiler supports -Wno-inline-new-delete... no
checking whether the C compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C++ compiler supports -Wno-error=maybe-uninitialized... yes
checking whether the C compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C++ compiler supports -Wno-error=deprecated-declarations... yes
checking whether the C compiler supports -Wno-error=array-bounds... yes
checking whether the C++ compiler supports -Wno-error=array-bounds... yes
checking whether the C compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C++ compiler supports -Wno-error=coverage-mismatch... yes
checking whether the C compiler supports -Wno-error=backend-plugin... no
checking whether the C++ compiler supports -Wno-error=backend-plugin... no
checking whether the C compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C++ compiler supports -Wno-error=free-nonheap-object... yes
checking whether the C compiler supports -Wno-error=multistatement-macros... no
checking whether the C++ compiler supports -Wno-error=multistatement-macros... no
checking whether the C compiler supports -Wno-error=return-std-move... no
checking whether the C++ compiler supports -Wno-error=return-std-move... no
checking whether the C compiler supports -Wno-error=class-memaccess... no
checking whether the C++ compiler supports -Wno-error=class-memaccess... no
checking whether the C compiler supports -Wno-error=atomic-alignment... no
checking whether the C++ compiler supports -Wno-error=atomic-alignment... no
checking whether the C compiler supports -Wno-error=deprecated-copy... no
checking whether the C++ compiler supports -Wno-error=deprecated-copy... no
checking whether the C compiler supports -Wformat... yes
checking whether the C++ compiler supports -Wformat... yes
checking whether the C compiler supports -Wformat-security... yes
checking whether the C++ compiler supports -Wformat-security... yes
checking whether the C compiler supports -Wformat-overflow=2... yes
checking whether the C++ compiler supports -Wformat-overflow=2... yes
checking whether the C compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-gnu-zero-variadic-macro-arguments... no
checking whether the C++ compiler supports -Wno-noexcept-type... yes
checking whether the C++ compiler supports -fno-sized-deallocation... yes
checking whether the C++ compiler supports -fno-aligned-new... yes
checking for rustc... /usr/bin/rustc
checking for cargo... /usr/bin/cargo
checking rustc version... 1.39.0
checking cargo version... 1.39.0
checking for rust target triplet... x86_64-unknown-linux-gnu
checking for rust host triplet... x86_64-unknown-linux-gnu
checking for rustdoc... /usr/bin/rustdoc
checking for rustfmt... not found
checking for clang for bindgen... not found
checking for libclang for bindgen... not found
checking bindgen cflags... -x c++ -fno-sized-deallocation -fno-aligned-new -DTRACING=1 -DIMPL_LIBXUL -DMOZILLA_INTERNAL_API -DRUST_BINDGEN -DOS_POSIX=1 -DOS_LINUX=1
checking for llvm_profdata... /usr/bin/llvm-profdata
checking for awk... /usr/bin/gawk
checking for perl... /usr/bin/perl
checking for minimum required perl version >= 5.006... 5.026001
checking for full perl installation... yes
checking for gmake... /usr/bin/make
checking for watchman... not found
checking for xargs... /usr/bin/xargs
checking for rpmbuild... /usr/bin/rpmbuild
checking for llvm-objdump... /usr/bin/llvm-objdump
checking for autoconf...
ERROR: Could not find autoconf 2.13
```

### Solution

```bash
sudo apt install autoconf2.13
```

# References

| Title | url | tags |
|---|---|---|
| Javascript Engine(Spider Monkey) Array OOB Analyzing | [link](https://bpsecblog.wordpress.com/2017/04/27/javascript_engine_array_oob) | `pwn`, `JIT`, `ctf`, `OOB` |
