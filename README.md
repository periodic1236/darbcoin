Darbcoin (DEI)
===========

Darbcoin is this really, really... kind of cryptocoin. It uses scrypt as a proof-of-work algorithm. 3553 Darbcoins are generated approximately every minute, for all time (probably).

[Darbcoin Block Chain Explore](http://darbcoin.myanimelife.net:2750/)

How to Build (for Debian based Linux)
-------
First, get the dependencies:

    sudo apt-get install build-essential libboost-all-dev libcurl4-openssl-dev libdb5.1-dev libdb5.1++-dev qt-sdk libminiupnpc-dev

Download the source. We'll assume it's stored in ``~/darbcoin`.

To build the command-line client (darbcoind):

    cd ~/darbcoin/src
    make -f makefile.unix "USE_UPNP=-"
    
To build the graphical client (darbcoin-qt):

    cd ~/darbcoin`
    qmake "USE_UPNP=-"
    make

How to Build (Windows)
-------
Don't. It's too hard. Abandon all hope. Use this release compiled using devil voodoo black magic: [darbcoin-v1-Win.zip] (http://darbcoin.myanimelife.net/darbcoin-v1-Win.zip)

How to Connect
-------
Darbcoin is somewhat lacking in nodes, so you might have to run the client with `-addnode=darbcoin.myanimelife.net` to get it to work. You can do this with both the command-line and graphical clients. On Windows, just run the `darbcoin-connect.bat` file, and it'll automatically run Darbcoin with the correct arguments. Darbcoin uses TCP port 3553, so open that port if you want others to able to connect to you.

How to Mine
-------
You can mine using your CPU with miner built into the client either through the graphical client, or in the command-line client using the command `setgenerate true [# Threads]`.

If you're using the graphical client, you'll want to set Scantime to 1.

To mine with your GPU, create a file called `darbcoin.conf` in `%appdata%/Darbcoin` (Windows) or `~/.darbcoin` (Linux) containing:

    rpcuser=[USERNAME]
    rpcpassword=[PASSWORD]

Then run the Darbcoin client with -server (this is automatically done in `darbcoin-json-rpc.bat`), which will start a JSON-RPC server on port 3552. ~~Then, pick a Litecoin mining application of your choice ([GUIMiner-scrypt](https://bitcointalk.org/index.php?topic=150331.0) works, make sure to set 'Use stratum' to No), and point it to `localhost:3552` with the username and password you specified in `darbcoin.conf`. It should work, hopefully. Actually, I don't think this works at least at the moment. I have a feeling that cgminer doesn't like working with a network difficulty of 0.00024414. If you can get GPU mining to work, let me know.~~

GPU Mining on Nvidia GPUs with CUDA (thanks Greg!)

Set up the darbcoin wallet client to work with cudaminer by adding a file "darbcoin.conf" to %appdata%/darbcoin, with the contents:

    server=1
    daemon=1
    rpcuser=miner
    rpcpassword=password
    rpcallowip=127.0.0.1
    rpcallowip=192.168.*.*
    
And invoking cudaminer with: 
cudaminer -o 127.0.0.1:3552 -O miner:password
(or alternatively, whatever IP gets you to the host with the wallet running, but make sure the IP is allowed in the darbcoin.conf file)

If cudaminer gives you an error saying it doesn't detect a CUDA driver, install the [CUDA development kit](https://developer.nvidia.com/cuda-downloads).

License
-------

Darbcoin is released under the terms of the MIT license.
