Karton is a tool to transparently run Linux programs on macOS or on another Linux distro.

``` sh
$ # Run the compiler on the host machine (running macOS):
$ gcc -o test_mac test.c
$ file test_mac
test_mac: Mach-O 64-bit executable x86_64

$ # Run the compiler inside Ubuntu using Karton:
$ karton run ubuntu gcc -o test_linux test.c

$ # Verify that the program is actually a Linux executable:
$ file test_linux
test_linux: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=5d842663aa0478ba923ce230fe71fcfd07402dba, not stripped
```

In the example, by prefixing your commands with `karton run ubuntu`, you can run them on Ubuntu even if you are using macOS. Files are shared across the two operating systems and executing commands like this is very fast, making the whole experience smooth.

Underneath, Karton uses Docker to allow running programs, but Docker was not designed with this use case in mind, so Karton makes it work.


Why?
----

At work I use Linux, while my personal computer is a Mac. I want to be able to work from home without having to always take my work laptop back home.

Karton is not limited to running Linux programs on macOS but also allows running programs on a different Linux distro (for instance, if you use CentOS but you need to test something on Ubuntu) or running different architectures.
