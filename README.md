have-a-key-lime-pie: KitKat Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 4.4 ("KitKat / Key Lime Pie") builds.

Following pre-release builds were reconstructed:

| Build number                              | Status           |
| :---:                                     |   :---:          |
| [`AAQ65`] (6 March 2013)                  | Done             |
| [`AAQ84`] (25 March 2013)                 | Done             |
| [`AAR15`] (15 April 2013)                 | Done             |
| [`AAR31`] (1 May 2013)                    | Done             |
| [`AAR50C`] (20 May 2013)                  | Done             |
| [`KRS30D`] (30 July 2013)                 | Done             |
| [`KRS39`] (8 August 2013)                 | Done             |
| [`KRS44B`] (13 August 2013)               | Done             |
| [`KRS53G`] (23 August 2013)               | Done             |
| [`KRS58B`] (27 August 2013)               | Done             |

[`AAQ65`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/AAQ65.xml
[`AAQ84`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/AAQ84.xml
[`AAR15`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/AAR15.xml
[`AAR31`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/AAR31.xml
[`AAR50C`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/AAR50C.xml
[`KRS30D`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/KRS30D.xml
[`KRS39`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/KRS39.xml
[`KRS44B`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/KRS44B.xml
[`KRS53G`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/KRS53G.xml
[`KRS58B`]:  https://github.com/froyocomb/android/blob/have-a-key-lime-pie/KRS58b.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation.

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso).

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Downloading Source
------------------

To get started with downloading the source code, experience with Git and [`repo`](https://source.android.com/docs/setup/reference/repo) is needed.

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b have-a-key-lime-pie -m <build>.xml

Then to download the respective code, execute:

    repo sync --no-tags --no-clone-bundle

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
* [Every IR-series build from before 4.0.1 r1 was tagged](https://android.googlesource.com/platform/build/+log/598288e321cc4cec399afb20ff6485bf3b8ac953)
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time (cannot replace human labor)
