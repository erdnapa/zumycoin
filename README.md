﻿# **Zumy (ZMY) v1.2.0.0 INTIAL RELEASE VERSION**

![ZMY logo](https://github.com/zumy/zumycoin/blob/master/src/qt/res/images/light/splash.png)

**Copyright (c) 2018-2019 Zumy Developers**

Social:
Twitter: https://twitter.com/zumycoin
Discord: http://discord.zumy.xyz
Telegram: https://t.me/zumyco

Whitepaper: http://wp.zumy.xyz/ - BETA
Website: http://zumy.co

What is Zumy?
----------------
Coin Name: Zumy

Coin Ticker: ZMY

Consensus: MN/PoW

MN Collateral: 2,000 ZMY

Block reward: 2 ZUMY Fluctuating

MN reward: 0.8 ZMY
Masternode Collateral Confirmations: 16 Blocks 

Governance Developers Fund: 0.2 ZMY Begins at 250,000 Blocks

Miner Reward : Fluctuating 1.6 ZMY current

Block spacing: 128 Seconds

Total supply: 12,614,400 ZMY

Maturity: 10 Blocks

Minimum TX Fee: 0.0001 ZMY

PoW Mining Algorithm: Argon2d

RPC port: 31051

Port: 32000

A newly launching ecosystem with a decentralized, all in one financial exchange and development Services ecosystem. Ever evolving in creating a safe haven for all creators online and offline.

Zumy uses peer-to-peer technology to operate securly with no central authority (decentralisation): managing transactions and issuing currency (ZMY) are carried out collectively by the Zumy network. Zumy is the name of open source software which enables the use of the currency ZMY.

Zumy utilises Masternodes, Privatesend and InstantSend to provide anonymous and near instant transaction confirmations.

Zumy implements Gavin Andresens signature cache optimisation from Bitcoin for significantly faster transaction validation.


**Masternode/Privatesend Network Information**
Utilisation of InstantSend for near-instant transactions and PrivateSend for anonymous transactions.

**MainNet Parameters**
P2P Port = 32000
RPC Port = 31051
Masternodes = 32000


UNIX BUILD NOTES
====================
Some notes on how to build Zumy in Unix.

Note
---------------------
Always use absolute paths to configure and compile Zumy and the dependencies,
for example, when specifying the the path of the dependency:

    ../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB_PREFIX

Here BDB_PREFIX must absolute path - it is defined using $(pwd) which ensures
the usage of the absolute path.

To Build
---------------------

```bash
./autogen.sh
./configure
make
make install # optional
```

This will build zumy-qt as well if the dependencies are met.

Dependencies
---------------------

These dependencies are required:

 Library     | Purpose          | Description
 ------------|------------------|----------------------
 libssl      | SSL Support      | Secure communications
 libboost    | Boost            | C++ Library
 libevent    | Networking       | OS independent asynchronous networking

Optional dependencies:

 Library     | Purpose          | Description
 ------------|------------------|----------------------
 miniupnpc   | UPnP Support     | Firewall-jumping support
 libdb4.8    | Berkeley DB      | Wallet storage (only needed when wallet enabled)
 qt          | GUI              | GUI toolkit (only needed when GUI enabled)
 protobuf    | Payments in GUI  | Data interchange format used for payment protocol (only needed when GUI enabled)
 libqrencode | QR codes in GUI  | Optional for generating QR codes (only needed when GUI enabled)
 libzmq3     | ZMQ notification | Optional, allows generating ZMQ notifications (requires ZMQ version >= 4.x)

For the versions used in the release, see [release-process.md](release-process.md) under *Fetch and build inputs*.

System requirements
--------------------

C++ compilers are memory-hungry. It is recommended to have at least 3 GB of
memory available when compiling Zumy.

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
Build requirements:

    sudo apt-get install build-essential libtool automake autotools-dev autoconf pkg-config libssl-dev libcrypto++-dev libevent-dev git
	
	sudo apt-get autoconf-archive

for Ubuntu 12.04 and later or Debian 7 and later libboost-all-dev has to be installed:

    sudo apt-get install libboost-all-dev

 db4.8 packages are available [here](https://launchpad.net/~bitcoin/+archive/bitcoin).
 You can add the repository using the following command:

        sudo add-apt-repository ppa:bitcoin/bitcoin
        sudo apt-get update

 Ubuntu 12.04 and later have packages for libdb5.1-dev and libdb5.1++-dev,
 but using these will break binary wallet compatibility, and is not recommended.

for Debian 7 (Wheezy) and later:
 The oldstable repository contains db4.8 packages.
 Add the following line to /etc/apt/sources.list,
 replacing [mirror] with any official debian mirror.

    deb http://[mirror]/debian/ oldstable main

To enable the change run

    sudo apt-get update

for other Debian & Ubuntu (with ppa):

    sudo apt-get install libdb4.8-dev libdb4.8++-dev

Optional (see --with-miniupnpc and --enable-upnp-default):

    sudo apt-get install libminiupnpc-dev

ZMQ dependencies (provides ZMQ API 4.x):

        sudo apt-get install libzmq3-dev

Dependencies for the GUI: Ubuntu & Debian
-----------------------------------------

If you want to build Zumy-Qt, make sure that the required packages for Qt development
are installed. Qt 5 is necessary to build the GUI.
If both Qt 4 and Qt 5 are installed, Qt 5 will be used. Pass `--with-gui=qt5` to configure to choose Qt5.
To build without GUI pass `--without-gui`.

For Qt 5 you need the following:

    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libcrypto++-dev

libqrencode (optional) can be installed with:

    sudo apt-get install libqrencode-dev

Once these are installed, they will be found by configure and a zumy-qt executable will be
built by default.

Notes
-----
The release is built with GCC and then "strip zumyd" to strip the debug
symbols, which reduces the executable size by about 90%.

miniupnpc
---------

[miniupnpc](http://miniupnp.free.fr/) may be used for UPnP port mapping.  It can be downloaded from [here](
http://miniupnp.tuxfamily.org/files/).  UPnP support is compiled in and
turned off by default.  See the configure options for upnp behavior desired:

    --without-miniupnpc      No UPnP support miniupnp not required
    --disable-upnp-default   (the default) UPnP support turned off by default at runtime
    --enable-upnp-default    UPnP support turned on by default at runtime

To build:

    tar -xzvf miniupnpc-1.6.tar.gz
    cd miniupnpc-1.6
    make
    sudo su
    make install

Berkeley DB
-----------
It is recommended to use Berkeley DB 4.8. If you have to build it yourself:

```bash
ZUMY_ROOT=$(pwd)

# Pick some path to install BDB to, here we create a directory within the zumy directory
BDB_PREFIX="${ZUMY_ROOT}/db4"
mkdir -p $BDB_PREFIX

# Fetch the source and verify that it is not tampered with
wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef  db-4.8.30.NC.tar.gz' | sha256sum -c
# -> db-4.8.30.NC.tar.gz: OK
tar -xzvf db-4.8.30.NC.tar.gz

# Build the library and install to our prefix
cd db-4.8.30.NC/build_unix/
#  Note: Do a static build so that it can be embedded into the exectuable, instead of having to find a .so at runtime
../dist/configure --prefix=/usr/local --enable-cxx
make
sudo make install

# Configure Zumy to use our own-built instance of BDB
cd $ZUMY_ROOT
./configure (other args...) LDFLAGS="-L${BDB_PREFIX}/lib/" CPPFLAGS="-I${BDB_PREFIX}/include/"
```

**Note**: You only need Berkeley DB if the wallet is enabled (see the section *Disable-Wallet mode* below).

Boost
-----
If you need to build Boost yourself:

    sudo su
    ./bootstrap.sh
    ./bjam install


Security
--------
To help make your Zumy installation more secure by making certain attacks impossible to
exploit even if a vulnerability is found, binaries are hardened by default.
This can be disabled with:

Hardening Flags:

    ./configure --enable-hardening
    ./configure --disable-hardening


Hardening enables the following features:

* Position Independent Executable
    Build position independent code to take advantage of Address Space Layout Randomization
    offered by some kernels. An attacker who is able to cause execution of code at an arbitrary
    memory location is thwarted if he doesn't know where anything useful is located.
    The stack and heap are randomly located by default but this allows the code section to be
    randomly located as well.

    On an Amd64 processor where a library was not compiled with -fPIC, this will cause an error
    such as: "relocation R_X86_64_32 against `......' can not be used when making a shared object;"

    To test that you have built PIE executable, install scanelf, part of paxutils, and use:

        scanelf -e ./zumyd

    The output should contain:
     TYPE
    ET_DYN

* Non-executable Stack
    If the stack is executable then trivial stack based buffer overflow exploits are possible if
    vulnerable buffers are found. By default, zumy should be built with a non-executable stack
    but if one of the libraries it uses asks for an executable stack or someone makes a mistake
    and uses a compiler extension which requires an executable stack, it will silently build an
    executable without the non-executable stack protection.

    To verify that the stack is non-executable after compiling use:
    `scanelf -e ./zumyd`

    the output should contain:
    STK/REL/PTL
    RW- R-- RW-

    The STK RW- means that the stack is readable and writeable but not executable.

Disable-wallet mode
--------------------
When the intention is to run only a P2P node without a wallet, zumy may be compiled in
disable-wallet mode with:

    ./configure --disable-wallet

In this case there is no dependency on Berkeley DB 4.8.

Mining is also possible in disable-wallet mode, but only using the `getblocktemplate` RPC call.


Example Build Command
--------------------
Qt Wallet and Deamon, CLI version build:

    ./autogen.sh && ./configure --with-gui && make

CLI and Deamon Only Buld:

    ./autogen.sh && ./configure --without-gui && make
