kraking-the-bread: Gingerbread Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 2.3 ("Gingerbread") builds.

Following pre-release builds were reconstructed:

| Build number and/or date                  | Status           |
| :---:                                     |   :---:          |
| [`15 April 2010`]                         | Done             |
| [`GRF70`] (June 11 2010)                  | Work in progress |

The following builds are uncompilable and have been unfortunately cancelled due to not possible way to compile them:
| Build number and/or date                  | Status           |
| :---:                                     |   :---:          |
| [`05 May 2010`]                           | Uncompilable due to major changes done during its tagged date|

[`15 April 2010`]:  https://github.com/froyocomb/android/blob/zombiebread/MASTER-20100415.xml
[`05 May 2010`]:  https://github.com/froyocomb/android/blob/zombiebread/MASTER-20100505.xml
[`GRF70`]:  https://github.com/froyocomb/android/blob/zombiebread/GRF70.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso).

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b zombiebread -m <build>.xml

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

    make 

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
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time 
