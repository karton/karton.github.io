Karton is a tool which can transparently run Linux programs:

* <i class="twa twa-penguin">🐧</i> on a different Linux distribution,
* <i class="twa twa-apple">🍎</i> on macOS,
* <i class="twa twa-laptop-computer">💻</i> on a different architecture (ARMv7 and ARMv8, on a x86-64 host).

To do this, you just need to tell Karton which distro <i class="twa twa-penguin">🐧</i> to use, which packages <i class="twa twa-package">📦</i> to install, and which directories <i class="twa twa-open-file-folder">📂</i> to make accessible. This is called an *image*.

Then you can run your commands inside the image just by adding <code>karton run <i>image-name</i></code> in front of your commands.


Example
-------

``` sh
$ uname -a # Show we are running on macOS.
Darwin my-hostname 16.4.0 Darwin Kernel Version 16.4.0 [...]

$ # Run the compiler in the Ubuntu image we use for work
$ # (which we called "ubuntu-work"):
$ karton run ubuntu-work gcc -o test_linux test.c

$ # Verify that the program is actually a Linux one.
$ # The files are shared and available both on your
$ # system and in the image:
$ file test_linux
test_linux: ELF 64-bit LSB executable, x86-64, [...]

$ # Same thing but on 32-bit ARMv7 (in the image we
$ # called "ubuntu-work-arm"):
$ karton run ubuntu-work-arm gcc -o test_arm test.c
$ file test_arm
test_arm: ELF 32-bit LSB executable, ARM, EABI5 [...]

$ # We can run the ARM program:
$ karton run ubuntu-work-arm ./test_arm
[... Output of our program ...]
```

<p class="extra-space-top">In another terminal you can attach to the running program and debug it.</p>

``` sh
$ # Find the PID of the test_arm program.
$ karton run ubuntu-work-arm ps aux | grep test_arm
test_arm    42  [...]  test_arm

$ # Debug it!
$ karton run ubuntu-work-arm gdb --pid 42
GNU gdb (Ubuntu 7.11.1-0ubuntu1~16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
[...]
Attaching to process 11
[...]
0x00007f53430e4740 in __nanosleep_nocancel () at ../sysdeps/unix/syscall-template.S:84
84	../sysdeps/unix/syscall-template.S: No such file or directory.
(gdb)
```

<p class="extra-space-top">Does typing every time <code>karton run <i>image-name</i></code> look boring? You can use the <code>alias</code> command, see <code>karton help alias</code>.</p>


Features
--------

* Fast <i class="twa twa-runner-type-4">🏃🏽</i>. Launching a program in an image takes fractions of a second.
* No need to start/stop a virtual machine or container, it's done transparently and quickly.
* Multiple terminals access the same running image. You can start a program in one terminal and attach to it with `gdb` from another.
* Automatic handling of shared directories and files. Your files are accessible both on your system and to programs running in an image.
* Except for directories you decide to share, the file system is transient. You can reset your changes to the system instantly.
* Can run Ubuntu, Debian, Fedora and CentOS images.
* Based on Docker <i class="twa twa-whale">🐳</i> containers.
