This has been a comprehensive project for me. If you appreciate the work done <br />
please consider donating(RVN) to: RD7yadeCvSDs4fCbEPuHstU3GHbiS7ao9q <br />

Ravencoin - an extended RPC version of Ravencoin  
=====================================

Major Changes Include:
----------------
Removing Full BIP173(Bech32) support <br />
Rebasing Ravencoin to the correct commit of bitcoin <br />
Adding address, spent and timestamp indexes and RPC calls <br />

Compiling Notes (linux):
----------------

Prerequisites: <br />

```
$sudo apt-get -y install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3
$sudo apt-get install libboost-all-dev
$sudo apt-get install software-properties-common
$sudo add-apt-repository ppa:bitcoin/bitcoin
$sudo apt-get update
$sudo apt-get install libdb4.8-dev libdb4.8++-dev
$sudo apt-get install libminiupnpc-dev
$sudo apt-get install libzmq3-dev
```

Compiling:

```
$sudo ./autogen.sh
$./configure --enable-cxx --disable-tests --enable-reduce-exports --disable-bench --disable-shared --with-pic --prefix=$BDB_PREFIX CXXFLAGS="-fPIC" CPPFLAGS="-fPIC"
$make
```

Helpful Commands
----------------
(start ravend) <br />
```
$ravend -daemon
```
(stop ravend) <br />
```
$raven-cli stop
```
Sample raven.conf
----------------
```
#server=1 tells Bitcoin-Qt and bitcoind to accept JSON-RPC commands
server=1

#Set rpcuser and rpcpassword to your own values for security
rpcuser=a-unique-username
rpcpassword=a-unique-password

#allow connections from localhost
rpcallowip=127.0.0.1
whitelist=127.0.0.1

#Listen for RPC connections on this TCP port:
rpcport=8766

#Miscellaneous options

txindex=1
addressindex=1
spentindex=1
timestampindex=1

mempoolexpiry=72 # Default 336
rpcworkqueue=1100
maxmempool=2000
dbcache=1000
maxtxfee=1.0
uacomment=bitcore-sl
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
dbmaxfilesize=64
```
Packaging Ravencoin for Ravencore:
----------------
```
$sudo ./autogen.sh
$./configure --enable-cxx --disable-tests --enable-reduce-exports --disable-bench --with-pic --prefix=$BDB_PREFIX CXXFLAGS="-fPIC" CPPFLAGS="-fPIC"
$make
$mkdir ~/package && mkdir ~/package/ravencoin-0.15.0
$sudo make install DESTDIR=~/package/ravencoin-0.15.0
$cd ~/package/
$sudo find . -name "lib*.la" -delete
$sudo find . -name "lib*.a" -delete
$sudo rm -rf ravencoin-0.15.0/lib/pkgconfig
$find ravencoin-0.15.0/ -not -name "*.dbg" | sort | tar --no-recursion --mode='u+rw,go+r-w,a+X' --owner=0 --group=0 -c -T - | gzip -9n > ~/ravencoin-0.15.0-linux64.tar.gz
$cd
$sha256sum ravencoin-0.15.0-linux64.tar.gz > SHA256SUMS
$gpg --digest-algo sha256 --clearsign SHA256SUMS # outputs SHA256SUMS.asc
##(enter password for gpg key)##
$rm SHA256SUMS
````
upload SHA256SUMS.asc and .tar.gz to github release page

Raven Core integration/staging tree
=====================================
https://ravencoin.org

What is Raven?
----------------

Raven is an experimental digital currency that enables instant payments to
anyone, anywhere in the world. Raven uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. Raven Core is the name of open source
software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of
the Raven Core software, see https://ravencoin.org

License
-------

Raven Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/RavenProject/Ravencoin/tags) are created
regularly to indicate new official, stable release versions of Raven Core.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

Developer IRC can be found on Freenode at #raven-core-dev.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

Testnet is now up and running and available to use during development. There is an issue when connecting to the testnet that requires the use of the -maxtipage parameter in order to connect to the test network initially. After the initial launch the -maxtipage parameter is not required.

Use this command to initially start ravend on the testnet. <code>./ravend -testnet -maxtipage=259200</code>

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/test), written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/test) are installed) with: `test/functional/test_runner.py`


### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.


About Ravencoin
----------------
A digital peer to peer network for the facilitation of asset transfer.



In the fictional world of Westeros, ravens are used as messengers who carry statements of truth. Ravencoin is a use case specific blockchain designed to carry statements of truth about who owns what assets.



Thank you to the Bitcoin developers.

The Ravencoin project is launched based on the hard work and continuous effort of over 400 Bitcoin developers who made over 14,000 commits over the life to date of the Bitcoin project. We are eternally grateful to you for your efforts and diligence in making a secure network and for their support of free and open source software development.  The Ravencoin experiment is made on the foundation you built.


Abstract
----------------
Ravencoin aims to implement a blockchain which is optimized specifically for the use case of transferring assets such as securities from one holder to another. Based on the extensive development and testing of Bitcoin, Ravencoin is built on a fork of the Bitcoin code. Key changes include a faster block reward time and a change in the number, but not weighed distribution schedule, of coins. Ravencoin is free and open source and will be issued and mined transparently with no pre-mine, developer allocation or any other similar set aside. Ravencoin is intended to prioritize user control, privacy and censorship resistance and be jurisdiction agnostic while allowing simple optional additional features for users based on need.



A blockchain is a ledger showing the value of something and allowing it to be transferred to someone else. Of all the possible uses for blockchains, the reporting of who owns what is one of the core uses of the technology.  This is why the first and most successful use case for blockchain technology to date has been Bitcoin.

The success of the Ethereum ERC 20 token shows the demand for tokenized assets that use another blockchain.  Tokens offer many advantages to traditional shares or other participation mechanisms such as faster transfer, possibly increased user control and censorship resistance and reduction or elimination of the need for trusted third parties.

Bitcoin also has the capability of serving as the rails for tokens by using projects such as Omnilayer, RSK or Counterparty. However, neither Bitcoin nor Ethereum was specifically designed for facilitating ownership of other assets.

Ravencoin is designed to be a use case specific blockchain designed to efficiently handle one specific function: the transfer of assets from one party to another.

Bitcoin is and always should be focused on its goals of being a better form of money. Bitcoin developers will unlikely prioritize improvements or features which are specifically beneficial to the facilitation of token transfers.  One goal of the Ravencoin project is to see if a use case specific blockchain and development effort can create code which can either improve existing structures like Bitcoin or provide advantages for specific use cases.

In the new global economy, borders and jurisdictions will be less relevant as more assets are tradable and trade across borders is increasingly frictionless. In an age where people can move significant amounts of wealth instantly using Bitcoin, global consumers will likely demand the same efficiency for their securities and similar asset holdings.

For such a global system to work it will need to be independent of regulatory jurisdictions.  This is not due to ideological belief but practicality: if the rails for blockchain asset transfer are not censorship resistance and jurisdiction agnostic, any given jurisdiction may be in conflict with another.  In legacy systems, wealth was generally confined in the jurisdiction of the holder and therefor easy to control based on the policies of that jurisdiction. Because of the global nature of blockchain technology any protocol level ability to control wealth would potentially place jurisdictions in conflict and will not be able to operate fairly.  
