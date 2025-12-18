i-scream-sandwich: Ice Cream Sandwich Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 4.0 ("Ice Cream Sandwich") builds.

As of now, the following builds have been reconstructed:

| Build ID & manifest branch               | Status              |
| :--------------------------------------: | :-----------------: |
| [`IRJ20`]  (April 20th, 2011)            | Done                |
| [`IRJ40`]  (May 10th, 2011)              | Done                |
| [`IRJ60`]  (May 30th, 2011)              | Done                |
| [`IRJ81`]  (June 20th, 2011)             | Done, has rendering issues[^1]|
| [`IRK04`]  (July 4th, 2011)              | Done, has rendering issues[^1]|
| [`IRK22`] (July 22th, 2011)              | Done, has rendering issues[^1]|
| [`IRK36B`] (August 6th, 2011)            | Done                |
| [`IRK40C`] (August 9th, 2011)            | Done                |  
| [`IRK48`] (August 17th, 2011)            | Done                |
| [`IRK62C`] (August 31st, 2011)           | Done                | 
| [`IRK77`] (September 15th, 2011)         | Done                |
| [`IRK88B`] (September 26th, 2011)        | Done                |
| [`IFL10`] (October 10th, 2011)           | Done                |
| [`ITL28B`] (October 28th, 2011)          | Done                |

[`IRJ20`]:  https://github.com/froyocomb/android/blob/i-scream-sandwich/IRJ20.xml
[`IRJ40`]:  https://github.com/froyocomb/android/blob/i-scream-sandwich/IRJ40.xml
[`IRJ60`]:  https://github.com/froyocomb/android/blob/i-scream-sandwich/IRJ60.xml
[`IRJ81`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRJ81.xml
[`IRJ91D`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRJ91D.xml
[`IRK04`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK04.xml
[`IRK22`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK22.xml
[`IRK36B`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK36B.xml
[`IRK40C`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK40C.xml
[`IRK48`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK48.xml
[`IRK62C`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK62C.xml
[`IRK77`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK77.xml
[`IRK88B`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IRK88B.xml
[`IFL10`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/IFL10.xml
[`ITL28B`]: https://github.com/froyocomb/android/blob/i-scream-sandwich/ITL28B.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso).

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Ubuntu 12.04 usually bundles newer GCC version, like 4.6. However, for those builds, GCC 4.4 is more recommended. To download older GCC, execute:

    sudo apt-get install gcc-4.4 g++-4.4 gcc-4.4-multilib g++-4.4-multilib  

Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b i-scream-sandwich -m <build>.xml

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

    make CC=gcc-4.4 CXX=g++-4.4

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
* [Every IR-series build from before 4.0.1 r1 was tagged](https://android.googlesource.com/platform/build/+log/598288e321cc4cec399afb20ff6485bf3b8ac953)
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time 

[^1]: The following builds have rendering issues as a result of several graphic-related changes done in their lifespan. These changes will not be fixed as the builds are meant to be as accurate as possible.
