# IoT Cloud Stack Tutorial – EclipseCon Europe 2018

**Note:** This module uses Git submodules. Either clone with `--recursive` or run `git submodule update --init --recursive` after cloning.

## Getting started

Clone this repository:

    git clone https://github.com/ctron/iot-cloud-stack-ece2018 --recursive

**Git for Windows:** If you are using Git for Windows, then you need to execute the following
                     command __before__ cloning the Git repository.

    git config --global core.longpaths true 

Move on to: [steps](steps)

## Be prepared

Before you come to Ludwigsburg, you should prepare yourself. The following sub-sections help you
bring what you will need for this tutorial.

### GitHub Account

This tutorial requires a GitHub account, which you can use to fork repositories and
set webhooks to those forks. You can, of course, create a new GitHub account.

### A Linux machine

Yes, Linux is awesome. Bring your Linux notebook including:

  * A web browser
  * Either
    * Command line `git`
    * Or the Eclipse IDE with Git support
  * The classics
     * Like `bash`, `curl`, `sed`, … nothing fancy

### But I got a Mac!

It's actually less about the kernel, more about the command line tools. *sigh* ...

GNU/Mac OS X will work as well, as long as you still bring the tools mentioned above.
It might be helpful to install GNU Sed using `brew install gnu-sed`.

### And what about Windows?

Don't count on playing Minesweeper during the tutorial 😉

With Windows you need to prepare yourself. You will still need the basics already
mentioned: web browser, git, command line classics.

Windows doens't bring those out of the box, so you need to take care of that
yourself.

There are a few choices you have:

  * Run Linux virtual machine – That brings you back to [A Linux machine](#a-linux-machine), but you finally
    got a nice little Linux box on your machine.
  * Install [Git for Windows](https://git-scm.com/download/win) – Git for Windows allows you to install a "Git Bash", which
    has everything this tutorial needs. Might be a good alternative over a full blown virtual machine.
  * Run a docker container – `docker run -ti centos:7` and installing a few extras should work as well. But
    from what I know, this boils down to running Docker with a virtual machine again.
  * Go for the Windows 10 Linux subsystem – Yes, hell froze over once again. And now Windows acts like the Linux kernel.
