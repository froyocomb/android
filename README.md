froyocomb: Honeycomb Restoration Project 
===========

This branch contains manifests for AOSP tool `repo`, that download source code of Android 3.0 ("Honeycomb") builds (including pre-release and final releases, which are hard to obtain in form of source code). 

Following pre-release builds were reconstructed:

| Build number                             | Status           |
| :---:                                    |   :---:          |
| [`HRF72`] (13 June 2010)                 | Done             |
| [`HRF91`] (30 June 2010)                 | Done             |
| [`HRG15`] (15 July 2010)                 | Done             |
| [`HRG30`] (30 July 2010)                 | Done             |
| [`HRG44B`] (13 August 2010)              | Done             |
| [`HRG61`] (30 August 2010)               | Done             |
| [`HRG71C`] (13 September 2010)           | Done             |
| [`HRG85C`] (27 September 2010)           | Done             |
| [`HRH27`] (27 October 2010)              | Done             |
| [`HRH54C`] (24 November 2010)            | Done             |
| [`HRH83D`] (27 December 2010)            | Done             |
| [`HRI34C`] (3 February 2011)             | Done             |

Following release builds were reconstructed:

| Build number                              | Status           |
| :---:                                     |   :---:          |
| [`android-3.0_r1`] (8 February 2011)      | Done             |
| android-3.0_r1.1 (10 March 2011)      | Abandoned        |

[`HRF72`]:  https://github.com/froyocomb/android/blob/froyocomb/HRF72.xml
[`HRF91`]:  https://github.com/froyocomb/android/blob/froyocomb/HRF91.xml
[`HRG15`]:  https://github.com/froyocomb/android/blob/froyocomb/HRG15.xml
[`HRG30`]:  https://github.com/froyocomb/android/blob/froyocomb/HRG30.xml
[`HRG44B`]: https://github.com/froyocomb/android/blob/froyocomb/HRG44B.xml
[`HRG61`]:  https://github.com/froyocomb/android/blob/froyocomb/HRG61.xml
[`HRG71C`]: https://github.com/froyocomb/android/blob/froyocomb/HRG71C.xml
[`HRG85C`]: https://github.com/froyocomb/android/blob/froyocomb/HRG85C.xml
[`HRH27`]:  https://github.com/froyocomb/android/blob/froyocomb/HRH27.xml
[`HRH54C`]: https://github.com/froyocomb/android/blob/froyocomb/HRH54C.xml
[`HRH83D`]: https://github.com/froyocomb/android/blob/froyocomb/HRH83D.xml
[`HRI34C`]: https://github.com/froyocomb/android/blob/froyocomb/HRI34C.xml
[`android-3.0_r1`]:  https://github.com/froyocomb/android/blob/froyocomb/android-3.0_r1.xml

Preparing a Build Environment
-----------------

For installing dependencies, refer to the article ["Initializing a Build Environment"](https://web.archive.org/web/20140208084633/http://source.android.com/source/initializing.html) from the AOSP documentation. 

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.5-desktop-amd64.iso). 

For the repositories to work, it is needed to replace any `archive.ubuntu.com` and `security.ubuntu.com` mentions in your repository list (which is under /etc/apt/sources.list) with `old-releases.ubuntu.com`. Then, it will be possible to install required dependencies.

Ubuntu 12.04 usually bundles newer GCC version, like 4.6. However, for those builds, GCC 4.4 is more recommended. To download older GCC, execute:

    sudo apt-get install gcc-4.4 g++-4.4 gcc-4.4-multilib g++-4.4-multilib  

Downloading Source
------------------

To get started with downloading the source code, it is needed to get familiar with Git and [`repo`](https://source.android.com/docs/setup/reference/repo).

To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the table above for available builds):

    repo init -u https://github.com/froyocomb/android.git -b froyocomb -m <build>.xml

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
	
If builds older than HRG85C are compiled, it is required to add additional parameter `BUILD_WITHOUT_PV=true` to the build command.

Usage
-----

To use the compiled build, run them in a emulator. To specify the resolution, use the `-skin` option.

    emulator -skin 1280x800

Useful Links
------------

* GitHub search filter for non-SVN (i.e. Android) commits from the LineageOS LLVM & Clang mirrors, ordered by commit date
  * [LLVM](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_llvm+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
  * [Clang](https://github.com/search?q=repo%3ALineageOS%2Fandroid_external_clang+NOT+%22git-svn-id%3A%22&type=commits&s=committer-date&o=asc)
* [Froyocomb Helper](https://gist.github.com/Dobby233Liu/c55c1e9c816facd153eeb19e386f53fd): userscript to assist finding commits before a certain time (cannot replace human labor)




	
	
