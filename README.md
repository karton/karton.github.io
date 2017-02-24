Karton is a tool which can transparently run Linux programs:

* 🐧 on a different Linux distribution,
* 🍎 on macOS,
* 💻 on a different architecture (ARMv7 and ARMv8 on x86-64).

To do this, you just need to tell Karton which distro 🐧 to use, which packages 📦 to install, and which directories 📂 to make accessible. This is called an *image*.

Then you can run your commands inside the image just by adding <code>karton run <i>image-name</i></code> in front of your commands.


Example
-------

You can compile a program written in C on macOS, Ubuntu and Ubuntu for ARMv7 on the same machine:

``` sh
$ # Run the compiler on your machine:
$ gcc -o test_mac test.c

$ # The executable is a Mac binary:
$ file test_mac
test_mac: Mach-O 64-bit executable x86_64

$ # Run the compiler inside Ubuntu using Karton:
$ karton run ubuntu gcc -o test_linux test.c

$ # Verify that the program is actually a Linux
$ # executable:
$ file test_linux
test_linux: ELF 64-bit LSB executable, x86-64, [...]

$ # Same thing but on 32-bit ARMv7:
$ karton run ubuntu-arm gcc -o test_arm test.c
$ file test_arm
test_arm: ELF 32-bit LSB executable, ARM, EABI5 [...]
```

In the example, by prefixing your commands with `karton run ubuntu`, you can run them on Ubuntu even if you are using macOS.<br>
Files are shared across the two operating systems and executing commands like this is very fast.


Features
--------

* Fast 🏃. Launching a program in an image takes fractions of a second.
* No need to start/stop a virtual machine or container, it's done transparently and quickly.
* Multiple terminals access the same running image. You can start a program in one terminal and attach to it with `gdb` from another.
* Automatic handling of shared directories and files. Your files are accessible both on your system and to programs running in an image.
* Except for directories you decide to share, the file system is transient. You can reset your changes to the system instantly.
* Can run Ubuntu, Debian, Fedora and CentOS images.
* Based on Docker 🐳 containers.
