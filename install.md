---
title: Install Karton
---

Linux
-----

1. Install Docker by using the packages available in your distro or by following the [official instructions](https://docs.docker.com/engine/installation/).
1. You should already have Python and the `pip` command installed. If not follow your normal distro procedures to install them:
   * On Debian or Ubuntu do: `sudo apt-get install python-pip`.
   * On Fedora or CentOS do: `yum install python-pip`.
1. Install Karton: `pip install karton`.
1. Try running `karton`. If it fails because the command was not found, add `~/.local/bin` to your `$PATH` environment variable.
   * Open the `~/.bashrc` file (assuming you use the bash shell, which is the default for most users).
   * Add `PATH="~/.local/bin:$PATH"` at the end of the file.


macOS
-----

1. Install Docker for Mac following the [official instructions](https://docs.docker.com/docker-for-mac/).
1. Install the `pip` command by copying this in a terminal: `which pip || sudo easy_install pip`.
1. Install Karton: `pip install karton`.
1. Try running `karton`. If it fails because the command was not found, add `~/Library/Python/2.7/bin/` to your `$PATH` environment variable:
   * Open the `~/.bashrc` file.
   * Add `PATH="~/Library/Python/2.7/bin:$PATH"` at the end of the file.



From source (all platforms)
---------------------------

You can also run Karton from source. This is recommended only if you want to modify it.

1. Close the repository from the [Karton GitHub page](https://github.com/karton/karton).
1. Create a symlink somewhere in your `$PATH` pointing to the `scripts/karton` file in your clone of the repository.
