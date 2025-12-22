thou-shalt-take-the-L: Lollipop Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 5.0 ("Lollipop") builds.

Following pre-release builds were reconstructed:

| Build number         | Status           |
| :---:                |   :---:          |
| AAU36                |  Done            |
| AAU42                |  WIP             |
| LRW38                |  WIP             |

Preparing a Build Environment
-----------------
**All of this must only be done once! Once a proper installation is set up, builds can be switched using just `repo init`. Make sure to erase the previous build's folders and files (with the exception of the hidden `.repo` folder, do not remove it) before changing.**

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 14.04 ("Trusty Tahr"), which can be downloaded from [here](https://releases.ubuntu.com/14.04/ubuntu-14.04.6-desktop-amd64.iso). 

**Prerequisites**
------------------
First, install all the needed dependencies needed for building AOSP:

```sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils openjdk-7-jdk xsltproc unzip$```

Afterwards, install Sun Java 1.6.0. The package for this is named `jdk-6u45-linux-x64.bin` - mirrors or the official download can be found by searching it up.

After acquiring the package, run the following (this assumes the package is on the Desktop and the terminal is on the same path where the file is):
```
chmod +x jdk-6u45-linux-x64.bin
./jdk-6u45-linux-x64.bin
sudo mkdir -p /usr/lib/jvm/jdk1.6.0_45
sudo mv ~/jdk1.6.0_45/* -f /usr/lib/jvm/jdk1.6.0_45/
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.6.0_45/bin/java" 1
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.6.0_45/bin/javac" 1
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.6.0_45/bin/javaws" 1```
```

Once done, run `sudo update-alternatives --config java` and switch the system over to `jdk1.6.0_45`. Do the same for `javac` and `javaws`, by replacing `java` with `javac` or `javaws`. `javaws` will likely not have an alternative, if so, skip it.

If the build uses OpenJDK 7 instead, switch to it appropiately.

To get modern `repo` working, install Python 3.6 in place of the standard Python 3.4. The commands for this are:

```
sudo apt-get install build-essential checkinstallsudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
cd ~
sudo wget https://www.python.org/ftp/python/3.6.15/Python-3.6.15.tgz
sudo tar xzf Python-3.6.15.tgz

cd Python-3.6.15
sudo ./configure --enable-optimizations
sudo make altinstall

sudo ln -s /usr/local/bin/python3.6 /usr/bin/python3.6

sudo -H pip3.6 install --upgrade pip

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.4 10
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 20
sudo update-alternatives --config python3
```

On the last command, check if `python3.6` is already selected.  

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

Optionally, run the command with `--depth=1` to shorten the source code size and download time from ~500GB to ~40GB. After the source code is finished checking out, proceed with the guide.

Then to download the respective code, execute:

    repo sync --no-tags --no-clone-bundle

Compiling
---------

To initialize the build environment, execute the following command:

   `. build/envsetup.sh`

Then pick from one of the available build targets by executing the command:

    lunch

To compile for specific devices, download and extract their driver binaries from Google's official website (https://developers.google.com/android/drivers).

To compile Android, type:

    make -jX (replace X with the amount of cores in your VM/PC)

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
