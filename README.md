what-kind-of-dessert-is-eclair-anyway: Eclair Restoration Project 
===========================================

This repository contains reconstructed `repo` manifests of known notable builds of Android 2.0-2.1 ("Eclair") builds.

Following pre-release builds were reconstructed:

| Build number                              | Status           |
| :---:                                              |   :---:             |
| [`May 13 2009 build`]                  | Done            |

[`May 13 2009 build`]:  https://github.com/froyocomb/android/blob/what-kind-of-dessert-is-eclair-anyway/MASTER-20090513.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso), although for Cupcake especially, it is is recommended to install 10.04 instead. The repo script will however not work by default on 10.04.

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Ubuntu 12.04 usually bundles newer GCC version, like 4.6. However, for those builds, GCC 4.4 is more recommended. To download older GCC, execute:

    sudo apt-get install gcc-4.4 g++-4.4 gcc-4.4-multilib g++-4.4-multilib  

For 10.04:

    sudo apt-get install gcc-4.2 g++-4.2 gcc-4.2-multilib g++-4.2-multilib  

Android 2.0-2.1 Eclair also requires Java 1.5 for building. It is recommended to install it and run the update-alternatives command for both `java` and `javac` to set it as default.

Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b what-kind-of-dessert-is-eclair-anyway -m <build>.xml

Then to download the respective code, execute:

    repo sync

Compiling
---------

To initialize the build environment, execute the following command:

    source build/envsetup.sh

Then pick from one of the available build targets by executing the command:

    lunch

As appropriate device trees are not available in the source, the only targets that are possible to pick are the generic ones.

To compile Android, type:

    make CC=gcc-4.2 CXX=g++-4.2

The Eclair build will then likely fail half way through on 12.04. Re-type the script again, although replace 4.2 with 4.4.

Running
-------

You can run the compiled build with the Android Emulator.

In the Ubuntu build environment, you may run the currently compiled build with the in-tree emulator by executing the command:

    emulator

Useful Links
------------

* GitHub search filter for non-SVN (i.e. Android) commits from the LineageOS LLVM & Clang mirrors, ordered by commit date
  * [LLVM](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_llvm+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
  * [Clang](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_clang+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
* [Every build from before 2.0 r1 was tagged](https://android.googlesource.com/platform/build/+log/refs/tags/android-2.0_r1)
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time 

[^1]: The following builds have rendering issues as a result of several graphic-related changes done in their lifespan. These changes will not be fixed as the builds are meant to be as accurate as possible.
