i-cant-believe-its-not-android: Android 1.0 AOSP build (TC3)
=========================================================

This repository contains the manifest for the Android 1.0 AOSP build (TC3).

Preparing a Build Environment
-----------------

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 LTS ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.4-desktop-amd64.iso). 

To prepare a build environment, you can use our own Bash script, which you can obtain [here](https://raw.githubusercontent.com/froyocomb/tools/refs/heads/main/envsetup.sh). Download it in your compiling environment and use chmod (or GUI interface) to give it executing permissions. 

After you execute the script, select the first option by typing in 1 and pressing Enter. It should automatically update the system and install required dependencies, including the repo script. After the option is done, restart the computer.

After the machine restarts, run the script again to install Java - select the 2nd option in the main menu and then select option 1 (JDK 5). The script can also change the default Java version, which can be useful if compiling different Android versions.

After the script is finished, create a folder in which the build files will be kept in, such as "android", then move on to the next step.

Downloading Source
------------------
To initialize a repository tree run the following command:

    repo init -u https://github.com/froyocomb/android.git -b i-cant-believe-its-not-android --depth=1

Then to download the respective code, execute:

    repo sync --no-tags --no-clone-bundle -c

Compiling
---------

To initialize the build environment, execute the following command:

 ```
. build/envsetup.sh
 ```

Then pick from one of the available build targets by executing the command:

    lunch

To compile for the HTC Dream, visit our proprietary-vendor repository and extract the "proprietary" folder into the vendor/htc/dream directory.

To compile the build, run:

    make CC=gcc-4.2 CXX=g++-4.2 -j$(nproc)

If the compile fails during the middle of compiling, run the following command afterwards (do not run make clean):

    make CC=gcc-4.4 CXX=g++-4.4 -j$(nproc)

Running
-------

You can run the compiled build with the Android Emulator.

In the Ubuntu build environment, you may run the currently compiled build with the in-tree emulator by executing the command:

    emulator
