froyocomb: Honeycomb Restoration Project
=========================================================

This repository contains reconstructed `repo` manifests of pre-release Android 3.x ("Honeycomb") builds.

**See the list of manifests above for the total amount of reconstructed builds.**

Preparing a Build Environment
-----------------

It is recommended to use an older Linux distribution. All builds have been tested on Ubuntu 12.04 LTS ("Precise Pangolin"), which can be downloaded from [here](https://old-releases.ubuntu.com/releases/12.04/ubuntu-12.04.4-desktop-amd64.iso). 

To prepare a build environment, you can use our own Bash script, which you can obtain [here](https://raw.githubusercontent.com/froyocomb/tools/refs/heads/main/envsetup.sh). Download it in your compiling environment and use chmod (or GUI interface) to give it executing permissions. 

After you execute the script, select the first option by typing in 1 and pressing Enter. It should automatically update the system and install required dependencies, including the repo script. After the option is done, restart the computer.

After the machine restarts, run the script again to install Java - select the 2nd option in the main menu and then select option 2. The script can also change the default Java version, which can be useful if compiling different Android versions.

After the script is finished, create a folder in which the build files will be kept in, such as "android", then move on to the next step.

Downloading Source
------------------
To initialize a repository tree using one of the manifests provided by this project, execute a command like this (see the list of manifests above for available `<build>`s):

    repo init -u https://github.com/froyocomb/android.git -b froyocomb -m <build>.xml --depth=1

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

To compile for specific devices, download and extract their driver binaries from Google's official website (https://developers.google.com/android/drivers), or use our "proprietary-vendor" repository.

If compiling a build above and including HRG85C, run:

    make CC=gcc-4.4 CXX=g++-4.4 -j$(nproc)

If compiling a build below HRG85C, run:

    make CC=gcc-4.4 CXX=g++-4.4 -j$(nproc) BUILD_WITHOUT_PV=TRUE

Please make sure to remember that certain builds may require exclusive patches that are mentioned on their respective BetaWiki page. If you face any issues during the compile, ask in the Discord server or on the "Issues" page on GitHub.

Running
-------

You can run the compiled build with the Android Emulator.

In the Ubuntu build environment, you may run the currently compiled build with the in-tree emulator by executing the command:

    emulator -skin 1280x800
