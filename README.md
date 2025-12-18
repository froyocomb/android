donut-bakery: Donut Restoration Project 
===========================================

This branch contains reconstructed `repo` manifests of known Android 1.6 ("Donut / Donut Burger") builds to be available via AOSP.

All of the planned builds have been reconstructed:

| Build ID & manifest branch               | Status              |
| :--------------------------------------: | :-----------------: |
| [`March 18 2009 build`]                  | Done                |
| [`March 24 2009 build`]                  | Done                |
| [`May 14 2009 build`]                    | Done                |
| [`June 17 2009 build`]                   | Done                |
| [`DRC06`]                                | Done                |
| [`DRC34`]                                | Done                |
| [`DRC52`]                                | Done                |

[`March 18 2009 build`]: https://github.com/froyocomb/android/blob/donut-bakery/MASTER-20090318.xml
[`March 24 2009 build`]: https://github.com/froyocomb/android/blob/donut-bakery/MASTER-20090324.xml
[`May 14 2009 build`]: https://github.com/froyocomb/android/blob/donut-bakery/MASTER-20090514.xml
[`June 17 2009 build`]: https://github.com/froyocomb/android/blob/donut-bakery/MASTER-20090617.xml
[`DRC06`]: https://github.com/froyocomb/android/blob/donut-bakery/DRC06.xml
[`DRC34`]: https://github.com/froyocomb/android/blob/donut-bakery/DRC34.xml
[`DRC52`]: https://github.com/froyocomb/android/blob/donut-bakery/DRC52.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso), although for Donut especially, it is is recommended to install 10.04 instead. The repo script will however not work by default on 10.04.

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Ubuntu 12.04 usually bundles newer GCC version, like 4.6. However, for those builds, GCC 4.4 is more recommended. To download older GCC, execute:

    sudo apt-get install gcc-4.4 g++-4.4 gcc-4.4-multilib g++-4.4-multilib  

For 10.04:

    sudo apt-get install gcc-4.2 g++-4.2 gcc-4.2-multilib g++-4.2-multilib  

Android 1.6 Donut also requires Java 1.5 for building. It is recommended to install it and run the update-alternatives command for both `java` and `javac` to set it as default.

Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>s):

    repo init -u https://github.com/froyocomb/android.git -b donut-bakery -m <build>.xml

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

The Donut build will then likely fail half way through on 12.04. Re-type the script again, although replace 4.2 with 4.4.

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
* [Every build from before 1.6 r1 was tagged]([https://android.googlesource.com/platform/build/+log/598288e321cc4cec399afb20ff6485bf3b8ac953](https://android.googlesource.com/platform/build/+log?s=cb6dae2336f976390031074ab80d4f29abc6268c))
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time 

[^1]: The following builds have rendering issues as a result of several graphic-related changes done in their lifespan. These changes will not be fixed as the builds are meant to be as accurate as possible.
