<details>
<summary>Why was Karton created?</summary>
<p>At work I use Linux, while my personal computer is a Mac. I want to be able to work from home without having to always take my work laptop back home.</p>

<p>I also didn't want to put up with the limitations of using a virtual machine.<br>
Using Docker was clearly the best solution, but, being designed for something else, didn't provide the usability I wanted.<br>
See the next two questions for details.</p>

<p>Moreover, with Karton, I can also easily compile and run ARM executables on x86-64 without even noticing they are not native.</p>

</details>

<details>
<summary>Why not a virtual machine?</summary>
<p>Because I want the most transparent user experience possible. I don't want to notice I'm using a different operating system and I want to use the native tools of the platform I'm using.</p>

</details>

<details>
<summary>Why not using Docker directly?</summary>
<p>Docker was created to do something different. According to Docker's web site:</p>

<blockquote>
Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries – anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in.
</blockquote>

<p>I wanted something which is more similar to using a virtual machine, but more transparent to the user.<br>
Karton takes care of lots of small details to make this possible and gives the user what I think is the best experience possible.</p>

</details>

<details>
<summary>Why not using a chroot or schroot?</summary>

<p><ul>
<li>Chroots don't work on macOS.</li>
<li>Chroots offer only file system-level isolation while containers offer complete logical isolation from a container to the host and all other containers.</li>
<li>Docker containers are easier to deal with.</li>
<li>Docker containers have their own IP address, hostname, etc.</li>
</ul></p>

</details>

<details>
<summary>What about different architectures?</summary>
<p>Karton supports x86-64 plus ARM (ARMv7 and ARMv8 aarch64) with the help of Docker and QEMU. This can be set through the <code>props.architecture</code> property in a definition file.</p>

<p>Note that not all distros are supported. At the moment, I believe that only Ubuntu and Debian work reliably.</p>

</details>

<details>
<summary>Does Karton run on Windows?</summary>
<p>Not at the moment. I don't use Windows and I cannot port Karton to it. I'm happy to accept contributions to make Karton work on Windows if anybody is interested.</p>

</details>

<details>
<summary>Does Karton run on my Linux distro?</summary>
<p>Probably yes, as long as Docker supports it and you are using a recent version of Docker.<br>
At the moment, Karton is tested automatically on Ubuntu, Debian, Fedora and CentOS.</p>

</details>

<details>
<summary>Can I run graphical applications?</summary>
<p>Not at the moment, but I'm planning to support X in the future. I don't think it's possible to support Wayland.</p>

</details>

<details>
<summary>Can I use Karton for security reasons or to isolate programs?</summary>
<p>You shouldn't.</p>

<p><ul>
<li>Docker doesn't offer as much security as using virtual machines.</li>
<li>Karton was not created with this use case in mind so it's possible it contains bugs that could affect the security aspect of things.</li>
<li>Karton uses Docker in privileged mode, which gives containers access to “unsafe” features (this is required, for instance, to allow debuggers to work inside Karton).</li>
</ul></p>

</details>

<details>
<summary>What's the license of Karton?</summary>
<p><a href="https://raw.githubusercontent.com/karton/karton/master/COPYING.LGPL2" target="_blank">LGPL version 2.1 or later</a>.</p>

<p>In short, this means that you can use Karton freely and modify it, but, if you do any modification, you need to redistribute those under the same license.</p>

<p>If you find this license a limitation for any reason, feel free to contact me. I may be happy to relicense under an MIT-style license if there's a valid use case for it.</p>

</details>

<details>
<summary>Who are you? How can I contact you?</summary>
<p>See the footer at the end of this page for my details.</p>

</details>

<details>
<summary>Can I help?</summary>
<p>Yes please!</p>
<p>Read the <a href="contribute.html">contribute page</a> for details.</p>

</details>
