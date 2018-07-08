# Aircrack-ng

[![Linux/Mac Build Status](https://travis-ci.org/aircrack-ng/aircrack-ng.svg?branch=master)](https://travis-ci.org/aircrack-ng/aircrack-ng)
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/aircrack-ng/aircrack-ng?branch=master&svg=true)](https://ci.appveyor.com/project/aircrack-ng/aircrack-ng)
[![Intel Compiler Build Status](https://buildbot.benden.us/badges/aircrack-ng.png?left_text=Intel%20Compiler%20Build)](https://buildbot.benden.us/)
[![Alpine Linux Build Status](https://buildbot.benden.us/badges/aircrack-ng-alpine.png?left_text=Alpine%20Linux%20Build)](https://buildbot.benden.us/)
[![Kali Linux Build Status](https://buildbot.benden.us/badges/aircrack-ng-kali.png?left_text=Kali%20Linux%20Build)](https://buildbot.benden.us/)
[![Armel Kali Linux Build Status](https://buildbot.benden.us/badges/aircrack-ng-armel.png?left_text=Armel%20Kali%20Linux%20Build)](https://buildbot.benden.us/)
[![Armhf Kali Linux Build Status](https://buildbot.benden.us/badges/aircrack-ng-armhf.png?left_text=Armhf%20Kali%20Linux%20Build)](https://buildbot.benden.us/)
[![FreeBSD Build Status](https://buildbot.benden.us/badges/aircrack-ng-bsd.png?left_text=FreeBSD%20Build)](https://buildbot.benden.us/)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/aircrack-ng/badge.svg)](https://scan.coverity.com/projects/aircrack-ng)
[![Coveralls Coverage Status](https://coveralls.io/repos/github/aircrack-ng/aircrack-ng/badge.svg?branch=master)](https://coveralls.io/github/aircrack-ng/aircrack-ng?branch=master)

Aircrack-ng is a complete suite of tools to assess WiFi network security.

It focuses on different areas of WiFi security:
 * Monitoring: Packet capture and export of data to text files for further processing by third party tools.
 * Attacking: Replay attacks, deauthentication, fake access points and others via packet injection.
 * Testing: Checking WiFi cards and driver capabilities (capture and injection).
 * Cracking: WEP and WPA PSK (WPA 1 and 2).

All tools are command line which allows for heavy scripting. A lot of GUIs have taken advantage of this feature. It works primarily Linux but also Windows, OS X, FreeBSD, OpenBSD, NetBSD, as well as Solaris and even eComStation 2. 

# Building

## Requirements

 * Autoconf
 * Automake
 * Libtool
 * shtool
 * OpenSSL development package or libgcrypt development package.
 * Airmon-ng (Linux) requires ethtool.
 * On windows, cygwin has to be used and it also requires w32api package.
 * On Windows, if using clang, libiconv and libiconv-devel
 * Linux: LibNetlink 1 or 3. It can be disabled by passing --disable-libnl to configure.
 * pkg-config (pkgconf on FreeBSD)
 * FreeBSD, OpenBSD, NetBSD, Solaris and OS X with macports: gmake
 * Linux/Cygwin: make and Standard C++ Library development package (Debian: libstdc++-dev)

## Optional stuff

 * If you want SSID filtering with regular expression in airodump-ng
   (-essid-regex) pcre development package is required.
 * If you want to use airolib-ng and '-r' option in aircrack-ng,
   SQLite development package >= 3.3.17 (3.6.X version or better is recommended)
 * If you want to use Airpcap, the 'developer' directory from the CD/ISO/SDK is required.
 * In order to build `besside-ng`, `besside-ng-crawler`, `easside-ng`, `tkiptun-ng` and `wesside-ng`,
   libpcap development package is required (on Cygwin, use the Aircap SDK instead; see above)
 * For best performance on FreeBSD (50-70% more), install gcc5 (or better) via: pkg install gcc7
 * rfkill

## Resolving the basic requirements

Below are instructions for installing the basic requirements to build
`aircrack-ng` for a number of operating systems.

### Cygwin (Windows)

Cygwin requires the full path to the `setup.exe` utility, in order to
automate the installation of the necessary packages. In addition, it
requires the location of your installation, a path to the cached
packages download location, and a mirror URL.

An example of automatically installing all the dependencies
is as follows:

    c:\cygwin\setup-x86.exe -qnNdO -R C:/cygwin -s http://cygwin.mirror.constant.com -l C:/cygwin/var/cache/setup -P autoconf -P automake -P bison -P gcc-core -P gcc-g++ -P mingw-runtime -P mingw-binutils -P mingw-gcc-core -P mingw-gcc-g++ -P mingw-pthreads -P mingw-w32api -P libtool -P make -P python -P gettext-devel -P gettext -P intltool -P libiconv -P pkg-config -P git -P wget -P curl -P libpcre-devel -P openssl-devel -P libsqlite3-devel

### Debian/Ubuntu

    sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev libsqlite3-dev libpcre3-dev ethtool shtool rfkill zlib1g-dev libpcap-dev

### Fedora/CentOS/RHEL

    sudo yum install libtool pkgconfig sqlite-devel autoconf automake openssl-devel libpcap-devel pcre-devel rfkill libnl3-devel gcc gcc-c++ ethtool

### FreeBSD using PKG

    pkg install pkgconf shtool libtool gcc7 automake autoconf pcre sqlite3 openssl gmake

### MSYS2 (Windows)

    pacman -Sy autoconf automake-wrapper libtool msys2-w32api-headers msys2-w32api-runtime gcc pkg-config git python openssl-devel openssl libopenssl msys2-runtime-devel gcc binutils make pcre-devel libsqlite-devel

### OSX

XCode, Xcode command line tools and HomeBrew are required.

    brew install autoconf automake libtool openssl shtool pkg-config

## Compiling

To build `aircrack-ng`, the Autotools build system is utilized. Autotools replaces
the older method of compilation.

**NOTE**: If utilizing a developer version, eg: one checked out from source control,
you will need to run a pre-`configure` script. The script to use is one of the
following: `autoreconf -i` or `env NOCONFIGURE=1 ./autogen.sh`.

First, `./configure` the project for building with the appropriate options specified
for your environment:

    ./configure <options>

**TIP**: If the above fails, please see above about developer source control versions.

Next, compile the project (respecting if `make` or `gmake` is needed):

 * Compilation:

    `make`

 * Compilation on *BSD or Solaris:

    `gmake`

Finally, the additional targets listed below may be of use in your environment:

 * Execute all unit testing:

    `make check`

 * Installing:

    `make install`

 * Uninstall:

    `make uninstall`


###  `./configure` flags

When configuring, the following flags can be used and combined to adjust the suite
to your choosing:

* **with-airpcap=DIR**:  needed for supporting airpcap devices on windows (cygwin or msys2 only)
                Replace DIR above with the absolute location to the root of the
                extracted source code from the Airpcap CD or downloaded SDK available
                online. Required on Windows to build `besside-ng`, `besside-ng-crawler`, 
                `easside-ng`, `tkiptun-ng` and `wesside-ng` when building experimental tools
                The developer pack (Compatible with version 4.1.1 and 4.1.3) can be downloaded at
                https://support.riverbed.com/content/support/software/steelcentral-npm/airpcap.html

* **with-experimental**: needed to compile `tkiptun-ng`, `easside-ng`, `buddy-ng`,
                    `buddy-ng-crawler`, `airventriloquist` and `wesside-ng`.
                    libpcap development package is also required to compile most of the tools.
                    If not present, not all experimental tools will be built.
                    On Cygwin, libpcap is not present and the Airpcap SDK replaces it.
                    See --with-airpcap option above.

* **with-ext-scripts**: needed to build `airoscript-ng`, `versuck-ng`, `airgraph-ng` and 
                   `airdrop-ng`. 
                   Note: Each script has its own dependencies.

* **with-gcrypt**:   Use libgcrypt crypto library instead of the default OpenSSL.
                And also use internal fast sha1 implementation (borrowed from GIT)
                Dependency (Debian): libgcrypt20-dev

* **with-duma**:	Compile with DUMA support. DUMA is a library to detect buffer overruns and under-runs.
            	Dependencies (debian): duma

* **with-xcode**:    Set this flag to true to compile on OS X with Xcode 7+.

* **disable-libnl**:  Set-up the project to be compiled without libnl (1 or 3). Linux option only.

* **without-opt**:  Do not enable stack protector (on GCC 4.9 and above).

* **enable-shared**:   Make OSdep a shared library.

* **disable-shared**: When combined with **enable-static**, it will statically compile Aircrack-ng.

* **with-avx512**:  On x86, add support for AVX512 instructions in aircrack-ng.

#### Examples:

  * Configure and compiling:

    ```
    ./configure --with-experimental
    make
    ```

  * Compiling with gcrypt:

    ```
    ./configure --with-gcrypt
    make
    ```

  * Installing:

    `make install`

  * Installing (strip binaries):
  
    `make install-strip`

  * Installing, with external scripts:

    ```
    ./configure --with-experimental --with-ext-scripts
    make
    make install
    ```

  * Testing (with sqlite, experimental and pcre)

    ```
    ./configure --with-experimental
    make
    make check
    ```

  * Compiling on OS X with macports (and all options):

    ```
    ./configure --with-experimental
    gmake
    ```

  * Compiling on OS X 10.10 with XCode 7.1 and Homebrew:

    ```
    env CC=gcc-4.9 CXX=g++-4.9 ./configure
    make
    make check
    ```

    *NOTE*: Older XCode ships with a version of LLVM that does not support CPU feature
    detection; which causes the `./configure` to fail. To work around this older LLVM,
    it is required that a different compile suite is used, such as GCC or a newer LLVM
    from Homebrew.

    If you wish to use OpenSSL from Homebrew, you may need to specify the location
    to its' installation. To figure out where OpenSSL lives, run:

    `brew --prefix openssl`

    Use the output above as the DIR for `--with-openssl=DIR` in the `./configure` line:

    ```
    env CC=gcc-4.9 CXX=g++-4.9 ./configure --with-openssl=DIR
    make
    make check
    ```

  * Compiling on FreeBSD with better performance

    ```
    env CC=gcc7 CXX=g++7 ./configure
    gmake
    ```

  * Compiling on Cygwin with Airpcap (assuming Airpcap devpack is unpacked in Aircrack-ng directory)

    ```
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-osdep
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-crypto
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-util
    dlltool -D Airpcap_Devpack/bin/x86/airpcap.dll -d build/airpcap.dll.def -l Airpcap_Devpack/bin/x86/libairpcap.dll.a
    autoreconf -i
    ./configure --with-experimental --with-airpcap=$(pwd)
    make
    ```

# Packaging

Automatic detection of CPU optimization is done at run time. This behavior
**is** desirable when packaging Aircrack-ng (for a Linux or other distribution.)

Also, in some cases it may be desired to provide your own flags completely and
not having the suite auto-detect a number of optimizations. To do this, add
the additional flag `--without-opt` to the `./configure` line:

`./configure --without-opt`

AVX512 compilation is disabled by default, very few CPUs support this instruction
set. To enable it, run configure with --with-avx512:

`./configure --with-avx512`


# Run-time location of SIMD binaries

Typically, the full path that is compiled in to the `aircrack-ng` binary is
`/usr/libexec/aircrack-ng`. However, during development and/or packaging, it
may be of use to specify a path that is dynamic in nature.

The environment variable `AIRCRACK_LIBEXEC_PATH` may be used to specify the
location of the SIMD-optimized binaries. An example of such use is as
follows:

`env AIRCRACK_LIBEXEC_PATH=/home/user/dev/aircrack-ng/src ./src/aircrack-ng`

The look up path can be set at compilation time. Append `pkglibexecdir`
parameter to `make` (or `gmake`). The following will set it to the
same/current directory:

`pkglibexecdir=.`

It is particularly useful for Windows, when all binaries are in
the same directory.

# Using precompiled binaries

## Linux/BSD
 * Use your package manager to download aircrack-ng
 * In most cases, they have an old version.

## Windows
 * Install the appropriate "monitor" driver for your card (standard drivers doesn't work for capturing data).
 * aircrack-ng suite is command line tools. So, you have to open a commandline
   `Start menu -> Run... -> cmd.exe` then use them
 * Run the executables without any parameters to have help

# Documentation


Documentation, tutorials, ... can be found on https://aircrack-ng.org

See also manpages and the forum.

For further information check the [README](README) file
