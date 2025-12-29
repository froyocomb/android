thou-shalt-take-the-L: Lollipop Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 5.0 ("Lollipop") builds.

Following pre-release builds were reconstructed:

| Build number         | Status           |
| :---:                |   :---:          |
| AAU36                |  Done            |
| AAU42                |  Done            |
| AAU55D               |  Done            |
| AAU65                |  Done            |
| AAU65C               |  Done            |
| AAU70                |  Done            |
| AAU83                |  WIP             |
| LRW38                |  Done            |

Preparing a Build Environment
-----------------
**All of this must only be done once! Once a proper installation is set up, builds can be switched using just `repo init`. Make sure to erase the previous build's folders and files (with the exception of the hidden `.repo` folder, do not remove it) before changing.**

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.4-desktop-amd64.iso). Do not use anything newer, like Ubuntu 14.04.

Once Ubuntu 12.04 LTS is installed, as it is now a legacy edition of Ubuntu, the default repositories have to be changed to "old-releases.ubuntu.com". To do this, open Terminal and type in `sudo gedit /etc/apt/sources.list`. Change all references of the URLs from e.g. `http://archive.ubuntu.com` to `http://old-releases.ubuntu.com`. Do the same for `http://security.ubuntu.com`, but don't touch the two bottom-most URLs. Make sure to only change the beginning of the aforementioned URLs.

If running in a virtual machine, install VMware Tools now, or else its features won't work properly (press enter on all questions given by `./vmware-install.pl`), then reboot.

Update the machine:
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install duplicity linux-headers-generic-lts-saucy linux-image-generic-lts-saucy ubuntu-minimal
sudo reboot
```
You can now proceed with the rest of the guide.

**Prerequisites**
------------------
First, install all the needed dependencies needed for building AOSP:


```sudo apt-get install git gnupg flex bison gperf build-essential zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 libglapi-mesa libgl1-mesa-dev mingw32 openjdk-7-jdk tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386```

Additionally run:
```sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so```

Certain builds of Lollipop require Sun Java 1.6, while certain ones require OpenJDK 7. OpenJDK 7 is installed in the above command. For builds requiring Sun Java 1.6.0, do the following:

Afterwards, install Sun Java 1.6.0. The package for this is named `jdk-6u45-linux-x64.bin` - mirrors or the official download can be found by searching it up.

After acquiring the package, run the following (this assumes the package is on the Desktop and the terminal is on the same path where the file is):
```
chmod +x jdk-6u45-linux-x64.bin
./jdk-6u45-linux-x64.bin
sudo mkdir -p /usr/lib/jvm/jdk1.6.0_45
sudo mv jdk1.6.0_45/* -f /usr/lib/jvm/jdk1.6.0_45/
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.6.0_45/bin/java" 1
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.6.0_45/bin/javac" 1
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.6.0_45/bin/javaws" 1
```

Once done, run `sudo update-alternatives --config java` and switch the system over to `jdk1.6.0_45`. Do the same for `javac` and `javaws`, by replacing `java` with `javac` or `javaws`. `javaws` will likely not have an alternative, if so, skip it.

If the build uses OpenJDK 7 instead, switch to it appropiately.

Install newer `git`:
```
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get upgrade
```

To get modern `repo` working, install Python 3.6:

```
sudo apt-get build-dep python3.2
wget https://www.python.org/ftp/python/3.6.15/Python-3.6.15.tgz
tar -xvf Python-3.6.15.tgz && cd Python-3.6.15
sudo ./configure --enable-optimizations
sudo make -j6 && sudo make install
```
 
Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To set up repo, do the following:
```
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

Run `gedit ~/.bashrc`, navigate to the bottom and paste in the line `export PATH=${PATH}:~/bin`. Restart the terminal and then create the `android/system` folders in the directory you wish to download and compile Android in. Navigate to the `system` folder and then proceed with the rest of the guide.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b thou-shalt-take-the-L -m <build>.xml

If `git` asks you to set your email and username, do so appropiately. Your actual username and email don't have to be used of course, just anything. Optionally, run the command with `--depth=1` to shorten the source code size and download time from ~500GB to ~40GB. After the source code is finished checking out, proceed with the guide.

Then to download the respective code, execute:

    repo sync --no-tags --no-clone-bundle

Optionally optionally, run the above command with `-c` to shorten the size and download time even more.

Compiling
---------

To initialize the build environment, execute the following command:

   ```. build/envsetup.sh```

Then pick from one of the available build targets by executing the command:

    lunch

To compile for specific devices, download and extract their driver binaries from Google's official website (https://developers.google.com/android/drivers).

To compile Android, type:

    make -j$(nproc)

Please make sure to remember that certain builds may require exclusive patches that are mentioned on their respective BetaWiki page. If you face any issues during the compile, ask in the Discord server or on the "Issues" page on GitHub.

Running
-------

You can run the compiled build with the Android Emulator.

In the Ubuntu build environment, you may run the currently compiled build with the in-tree emulator by executing the command:

    emulator

To set a custom resolution, type `-skin 1920x1080`, replacing 1920x1080 with your desired resolution. Certain builds can also work with GPU acceleration, this can be enabled using `-gpu on`.

Useful Links
------------

* GitHub search filter for non-SVN (i.e. Android) commits from the LineageOS LLVM & Clang mirrors, ordered by commit date
  * [LLVM](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_llvm+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
  * [Clang](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_clang+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time 
