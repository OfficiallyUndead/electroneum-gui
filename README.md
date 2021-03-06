# Electroneum GUI

Copyright (c) 2014-2017, The Monero Project
Special thanks to tperalta82 for his initial port which can be found [here](https://github.com/tperalta82/electroneum-core)

## About this Project

This is an unofficial GUI for [Electroneum](https://github.com/electroneum/electroneum). It is open source and completely free to use without restrictions, except for those specified in the license agreement below. There are no restrictions on anyone creating an alternative implementation of Monero that uses the protocol and network in a compatible manner.

As with many development projects, the repository on Github is considered to be the "staging" area for the latest changes. Before changes are merged into that branch on the main repository, they are tested by individual developers in their own branches, submitted as a pull request, and then subsequently tested by contributors who focus on testing and code reviews. That having been said, the repository should be carefully considered before using it in a production environment, unless there is a patch in the repository for a particular show-stopping issue you are experiencing. It is generally a better idea to use a tagged release for stability.

## Supporting the GUI Project

This GUI development can be supported directly through donations.

Electroneum Address is: `etnk15iRvCdXxgTghL2mpH4WTEUjyCCd2GSgVMLBQZPYGsTNudRw9pF5DX1d8LeMWkiUySg8f8yi6AE8PRc1uLNB6gYqmRY6Ts`
Monero Address is: `48VoiWRZ4ia7DUuC46xaKXdZpkgbshJBvGS7DMZ7HXDdUrJgKX6v8WeCkA1uePpwZihxAFWWzDQ1UUvqRsVqNyn5PPpL7SQ`

## License

See [LICENSE](LICENSE).

## Compiling Electroneum GUI Core from Source

### On Linux:

(Tested on Ubuntu 16.04 x64)

1. Install Electroneum dependencies

  - For Ubuntu and Mint

	`sudo apt install build-essential cmake libboost-all-dev miniupnpc libunbound-dev graphviz doxygen libunwind8-dev pkg-config libssl-dev`

  - For Gentoo

	`sudo emerge app-arch/xz-utils app-doc/doxygen dev-cpp/gtest dev-libs/boost dev-libs/expat dev-libs/openssl dev-util/cmake media-gfx/graphviz net-dns/unbound net-libs/ldns net-libs/miniupnpc sys-libs/libunwind`

2. Grab an up-to-date copy of the electroneum-core repository

	`git clone https://github.com/tperalta82/electroneum-core.git`

3. Go into the repository

	`cd electroneum-core`

4. Install the GUI dependencies

  - For Ubuntu 16.04+ x64

    `sudo apt-get install qtbase5-dev qt5-default qtdeclarative5-dev qml-module-qtquick-controls qml-module-qtquick-xmllistmodel qttools5-dev-tools qml-module-qtquick-dialogs qml-module-qt-labs-settings libqt5qml-graphicaleffects`

  - Optional : To build the flag `WITH_SCANNER`

    - For Ubuntu

      `sudo apt install qtmultimedia5-dev qml-module-qtmultimedia libzbar-dev`

5. Build the GUI

  - For Ubuntu and Mint
  
  `./get_libwallet_api.sh`
  `./build.sh`

The executable can be found in the build/release/bin folder.

### On OS X:

(Tested on macOS Sierra 10.12.6 - Running on a Late 2014 Mac Mini)

1. Install Xcode from AppStore
2. Install [homebrew](http://brew.sh/)
3. Install [electroneum](https://github.com/electroneum/electroneum) dependencies:

  `brew install boost --c++11`

  `brew install openssl` - to install openssl headers

  `brew install pkgconfig`

  `brew install cmake`

  `brew install qt5`  (or download QT 5.8+ from [qt.io](https://www.qt.io/download-open-source/))

  If you have an older version of Qt installed via homebrew, you can force it to use 5.x like so:
  
  `brew link --force --overwrite qt5`

5. Add the Qt bin directory to your path

    Example: `export PATH=$PATH:/usr/local/Cellar/qt/5.9.3/bin` (brew install qt5)
    Example: `export PATH=$PATH:$HOME/Qt/5.8/clang_64/bin` (install from website)

    This is the directory where Qt 5.x is installed on **your** system

6. Grab an up-to-date copy of the electroneum-core repository

  `git clone https://github.com/OfficiallyUndead/electroneum-gui.git`

7. Go into the repository

  `cd electroneum-gui`

8. Start the build

  `./get_libwallet_api.sh`
  `./build.sh`

The executable can be found in the `build/release/bin` folder.

**Note:** Workaround for "ERROR: Xcode not set up properly"

Edit `$HOME/Qt/5.8/clang_64/mkspecs/features/mac/default_pre.prf`

replace
`isEmpty($$list($$system("/usr/bin/xcrun -find xcrun 2>/dev/null")))`

with
`isEmpty($$list($$system("/usr/bin/xcrun -find xcodebuild 2>/dev/null")))`

More info: http://stackoverflow.com/a/35098040/1683164

### On Windows:

1. Install [msys2](http://msys2.github.io/), follow the instructions on that page on how to update packages to the latest versions

1.1. Specifically Use this version http://repo.msys2.org/distrib/i686/msys2-i686-20160205.exe

2. Install electroneum dependencies as described in [electroneum documentation](https://github.com/electroneum/electroneum) into msys2 environment
   **As we only build application for x86, install only dependencies for x86 architecture (i686 in package name)**
   ```
   pacman -S mingw-w64-i686-toolchain make mingw-w64-i686-cmake mingw-w64-i686-boost

   ```

3. Install git into msys2 environment

    ```
    pacman -S git
    ```

4. Install Qt5 from [official site](https://www.qt.io/download-open-source/)
   - download unified installer, run and select following options:
       - Qt > Qt 5.9 > MinGW 5.3.0 32 bit
       - Tools > MinGW 5.3.0
   - continue with installation

5. Open ```MinGW-w64 Win32 Shell``` shell 

   ```%MSYS_ROOT%\msys2_shell.cmd -mingw32```

   Where ```%MSYS_ROOT%``` will be ```c:\msys32``` if your host OS is x86-based or ```c:\msys64``` if your host OS
   is x64-based

6. Install the latest version of boost, specificly the required static libraries
    ```
    cd
    wget --no-check-certificate http://sourceforge.net/projects/boost/files/boost/1.63.0/boost_1_63_0.tar.bz2
    tar xjf boost_1_63_0.tar.bz2
    cd boost_1_63_0
    ./bootstrap.sh mingw
    ./b2 --prefix=/mingw32/boost --layout=tagged --without-mpi --without-python toolset=gcc address-model=32 variant=debug,release link=static threading=multi runtime-link=static -j$(nproc) install
    ```

7. Clone repository
    ```
    cd
    git clone https://github.com/OfficiallyUndead/electroneum-gui.git
    ```

8. Build the GUI
  Check which version of Qt you installed on point 4 and check the PATH below if it points to the correct location
    ```
    cd electroneum-core
    export PATH=$(ls -rd /c/Qt/5.[6,7,8,9].2/mingw53_32/bin | head -1):$PATH
    export CC=gcc
    git checkout windows-supportlink
    ./build.sh
    ./windows
    cd build
    make deploy
    ```

The executable can be found in the ```.\release\bin``` directory.

### Post Build (Important)

If when attempting to run the application you do not see a window, cd into the build directory and run `make deploy`.
This will copy the libraries and runtime files that are required for the app to work correctly.
