---
title: How to use Karton
---

*If you haven't installed Karton yet, do it following the [installation instructions](install.md).*


Create an image
---------------

Karton can run commands in several different Linux distributions with different sets of packages installed. A specific configured distro is called an **image**.
The first thing you need to do to use Karton is creating an image.

Let's imagine that, for work, you need to use the most recent (even if a bit unstable) version of Ubuntu to compile your project, but your computer runs another Linux distro or macOS.<br>
You then decide to create an image for your Ubuntu-based developent. Let's call this image `work`:

```sh
$ karton image create work ~/work-ubuntu-devel-image
```

This will generate a directory called `work-ubuntu-devel-image` inside your home directory. Inside this directory there's a Python source file called `definition.py`.

Open the `definition.py` file and take a look at the comments; they should explain everything you need to know about setting up an image.

The requirements for this image are quite simple:

* Use the latest development version of Ubuntu (called `ubuntu:devel`);
* Install compiler, headers and other basic development tools;
* Make the directory where we keep the source code (`~/src`) available to the image.

Modify the `definition.py` file (using your favourite editor) to look like this:

```python
def setup_image(props):
    # Name and version of the distro.
    props.distro = 'ubuntu:devel'

    # This is shared at the same relative path (relative to
    # your home directory) in the image as it is on your
    # machine, that is it will be accessible as "~/src" in
    # both home and image.
    props.share_path_in_home('src')

    # "build-essential" is name of the Ubuntu package which
    # installs gcc, make and similar tools.
    props.packages.append('build-essential')
```

Now that the image is defined you need to build it:

```sh
$ karton build work
```

This will take a couple of minutes, but you need to do it only when you modify the `definition.py` file.


Running commands
----------------

To run commands just use `karton run IMAGE-NAME COMMAND ARGUMENT1 ...`.

For instance, let's say you want to create a file called `~/src/my-project/test.c` and compile it using the newly created `work` image. You would do something like this:

```sh
$ # This all happens on your host machine:
$ cd ~/src/my-project/
$ # ... edit test.c ...

$ # Now compile (using the gcc inside the image, not the
$ # one on your system!):
$ karton run work gcc -o test test.c

$ # All the files are accessible both on the host and in
$ # the image.
$ ls -l
total 32
-rwxr-xr-x 1 user staff 8416 Feb 16 22:00 test
-rw-r--r-- 1 user staff   72 Feb 16 22:00 test.c

$ # Now you can run the program you just compiled!
$ karton run work ./test
[... output of the test program ...]

$ # The program is a Linux executable even if we are
$ # running on macOS.
$ file test
test: ELF 64-bit LSB shared object, x86-64,  [...]
```

If you want, you can even start a full shell inside the image:

```sh
$ karton shell work
$ # ... commands running on the Ubuntu image ...
```


Creating an alias
-----------------

After a while you will probably get bored of typing `karton run IMAGE-NAME` all the time. To make things simpler to type you can create an alias:

```sh
$ # Create a symbolic link "wk" which start Karton
$ # using the "work" image.
$ karton alias wk work
[...]

$ # This is equivalent to:
$ #     karton run work echo "Hello!"
$ wk run echo "Hello!"
Hello!
```

If you don't even want to have to type `run` every time, you can create an alias which includes a command as well:

```sh
$ # Create a "wr" alias (which stands for work and run):
$ karton alias --command run wr work

$ # Run the echo command in the image:
$ wr echo "Hello!"
Hello!
```

Directories inside the image
----------------------------

Images come with their own file system with all the files you would expect in a normal Linux system.

All the files and directories are reset when an image is restarted, with the exception of your home directory, and the directories and files you explicitly shared.

### Sharing directories and files

FIXME

### Home directory

FIXME (explain why non-transient but separate and how to configure it)


Managing images
---------------

FIXME: Document:

* Creating new ones
* Adding existing
* Removing


Image life cycle
----------------

FIXME
