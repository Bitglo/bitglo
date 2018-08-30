![Bitglo Logo](src/qt/res/images/trad/bitglo_logo_horizontal.png)

Bitglo is GNU AGPLv3 licensed.

[![Build Status](https://travis-ci.org/Bitglo/bitglo.svg?branch=master)](https://travis-ci.org/Bitglo/bitglo)
<a href="https://discord.gg/FFzPAbY"><img src="https://discordapp.com/api/guilds/481272240130752513/embed.png" alt="Discord Server" /></a> <a href="https://twitter.com/intent/follow?screen_name=BitgloExchange"><img src="https://img.shields.io/twitter/follow/BitgloExchange.svg?style=social&logo=twitter" alt="follow on Twitter"></a>
                                                                                                                                                     
[![Build history](https://buildstats.info/travisci/chart/Bitglo/bitglo?branch=master)](https://travis-ci.org/Bitglo/bitglo?branch=master)

[Website](https://get.bitglo.io) — [Exchange](https://bitglo.io) - [Pool](https://mine.bitglo.io) — [Block Explorer](https://explorer.bitglo.io) — [Discord](https://discord.gg/FFzPAbY) — [Twitter](https://twitter.com/BitgloExchange)

Bitglo (BGL) is an innovative cryptocurrency. A form of digital currency secured by cryptography and issued through a decentralized and advanced mining market. Based on Dash, it's an enhanced and further developed version, featuring the masternode technology with 50% Reward, near-instant and secure payments as well as anonymous transactions. 
Bitglo has great potential for rapid growth and expansion. Based on a total Proof of Work and Masternode system, it is accesible to everyone, it ensures a fair and stable return of investment for the Graphics Processing Units (GPUs) miners and the Masternode holders.

Additional information, wallets, specifications & roadmap: https://bitcointalk.org/

## Coin Specifications

| Specification | Value |
|:-----------|:-----------|
| Total Blocks | `1,500,000` |
| Block Size | `4MB` |
| Block Time | `60s` |
| PoW Reward | `20 BGL` |
| Masternode Requirement | `10,000 BGL` |
| Masternode Reward | `50% PoW` |
| Port | `12755` |
| RPC Port | `12756` |
| Masternode Port | `12755` |


Build Bitglo wallet
----------

### Build on Ubuntu

Use

    sudo add-apt-repository ppa:bitcoin/bitcoin; git clone https://github.com/Bitglo/bitglo; cd bitglo; ./autogen.sh; ./configure --disable-tests; make clean; make -j$(nproc)


Add bitcoin repository for Berkeley DB 4.8

    sudo add-apt-repository ppa:bitcoin/bitcoin

Clone Bitglo repository

    git clone https://github.com/Bitglo/bitglo

Build Bitglo 

    cd bitglo
    ./autogen.sh
    ./configure --disable-tests
    make -j$(nproc)


Setup and Build: Arch Linux
-----------------------------------
This example lists the steps necessary to setup and build a command line only, non-wallet distribution of the latest changes on Arch Linux:

    pacman -S git base-devel boost libevent python
    git clone https://github.com/Bitglo/bitglo
    cd bitglo/
    ./autogen.sh
    ./configure --without-miniupnpc --disable-tests
    make -j$(nproc)

Note:
Enabling wallet support requires either compiling against a Berkeley DB newer than 4.8 (package `db`) using `--with-incompatible-bdb`,
or building and depending on a local version of Berkeley DB 4.8. The readily available Arch Linux packages are currently built using
`--with-incompatible-bdb` according to the
As mentioned above, when maintaining portability of the wallet between the standard Bitcoin Core distributions and independently built
node software is desired, Berkeley DB 4.8 must be used.


ARM Cross-compilation
-------------------
These steps can be performed on, for example, an Ubuntu VM. The depends system
will also work on other Linux distributions, however the commands for
installing the toolchain will be different.

Make sure you install the build requirements mentioned above.
Then, install the toolchain and curl:

    sudo apt-get install g++-arm-linux-gnueabihf curl

To build executables for ARM:

    cd depends
    make HOST=arm-linux-gnueabihf NO_QT=1
    cd ..
    ./configure --prefix=$PWD/depends/arm-linux-gnueabihf --enable-glibc-back-compat --enable-reduce-exports LDFLAGS=-static-libstdc++
    make -j$(nproc)

For further documentation on the depends system see [README.md](../depends/README.md) in the depends directory.

Building on FreeBSD
--------------------

Clang is installed by default as `cc` compiler, this makes it easier to get
started than on [OpenBSD](build-openbsd.md). Installing dependencies:

    pkg install autoconf automake libtool pkgconf
    pkg install boost-libs openssl libevent
    pkg install gmake

You need to use GNU make (`gmake`) instead of `make`.
(`libressl` instead of `openssl` will also work)

For the wallet (optional):

    ./contrib/install_db4.sh `pwd`
    setenv BDB_PREFIX $PWD/db4

Then build using:

    ./autogen.sh
    ./configure BDB_CFLAGS="-I${BDB_PREFIX}/include" BDB_LIBS="-L${BDB_PREFIX}/lib -ldb_cxx"
    gmake

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/Bitglo/bitglo/tags) are created
regularly to indicate new official, stable release versions of Bitglo.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).


Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.