Use the following instructions to setup a masternode on Ubuntu Server 18.04.
Make sure that you have the following requirements.
- Required amount of coins to setup the masternode. 
- A wallet to store your coins. 
- A server or VPS.
The instructions are split in three sections.

Setup the control wallet (1/2)
Open your wallet and wait until the wallet has downloaded the complete blockchain.
Go to “Tools”. 
Click “Debug console”. 
This is the console where you will execute all commands.
Create a masternode private key.
masternode genkey

Example output
75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo

Show your collateral address.
getaccountaddress "MN1"

Example output
Nad4xtgdwf7c5y45ruy5MWtVY43zYMCvva

Keep note of the masternode private key and the collateral address.

Setup the VPS

Install Ubuntu Server 18.04 on a VPS.
Update your Ubuntu machine.
sudo apt-get update
sudo apt-get upgrade

Install the required dependencies.
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev
sudo apt-get install libminiupnpc-dev libzmq3-dev libprotobuf-dev protobuf-compiler unzip software-properties-common

Install Berkeley DB.
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev

Note: replace “examplecoin” with the name of your coin. 
Note: replace “6gs39011kick8xmqutpkrvi92xx5kwev4ykanlv1ls0ouuae5x” with the coinID of your coin.
Download the daemon and tools from MyCoin. (Available for a paid coin)
wget "https://dl.walletbuilders.com/download?customer=6gs39011kick8xmqutpkrvi92xx5kwev4ykanlv1ls0ouuae5x&filename=examplecoin-daemon-linux.tar.gz" -O examplecoin-daemon-linux.tar.gz
wget "https://dl.walletbuilders.com/download?customer=6gs39011kick8xmqutpkrvi92xx5kwev4ykanlv1ls0ouuae5x&filename=examplecoin-qt-linux.tar.gz" -O examplecoin-qt-linux.tar.gz

Extract the tar files.
tar -xzvf examplecoin-daemon-linux.tar.gz
tar -xzvf examplecoin-qt-linux.tar.gz

Install the daemon and tools.
sudo mv examplecoind examplecoin-cli examplecoin-tx /usr/bin/

Create the config file.
mkdir $HOME/.examplecoin
nano $HOME/.examplecoin/examplecoin.conf

Paste the following lines in examplecoin.conf.

rpcuser=rpc_examplecoin
rpcpassword=kuw05sqio7bcm8z96o7redv17xws1lw6xpd1qf33
rpcallowip=127.0.0.1
rpcport=4887
listen=1
server=1
daemon=1
port=4888
maxconnections=64
addnode=mn1.dcentralbank.com
addnode=mn2.decentralbank.com
masternode=1
masternodeprivkey=REPLACE_WITH_MASTERNODE_PRIVATE_KEY
externalip=REPLACE_WITH_EXTERNAL_IP_OF_VPS


Replace the text “REPLACE_WITH_MASTERNODE_PRIVATE_KEY” with the “masternode private key” that you created using the command “masternode genkey”. 

E.G. masternodeprivkey=75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo
Replace the text “REPLACE_WITH_EXTERNAL_IP_OF_VPS” with the external IP address of your VPS. 

E.G. externalip=136.144.171.201
Start your node with the following command:
examplecoind

Setup the control wallet (2/2)
Transfer the required amount of coins to the “collateral address” that you created using the command “getaccountaddress "MN1"”.
Wait until the transaction has the required masternode confirmations.
Go to Tools. 
Click Debug console. 
Enter the following command.
masternode outputs

Example output
{ "06e38868bb8f9958e34d5155437d009b72dff33fc28874c87fd42e51c0f74fdb" : "0", } 

Go to “Tools”. 
Click “Open Masternode Configuration File”. 
Modify the following line and paste it into notepad.
MN1 136.144.171.201:4888 75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo 06e38868bb8f9958e34d5155437d009b72dff33fc28874c87fd42e51c0f74fdb 0

MN1 - Alias for your masternode.
136.144.171.201 - External IP of your VPS.
4888 - P2P port.
75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo - Masternode private key from the command “masternode genkey”.
06e38868bb8f9958e34d5155437d009b72dff33fc28874c87fd42e51c0f74fdb - Transaction hash from the command “masternode outputs”.
0 - Single digit from the command “masternode outputs”.
Save the file and close notepad.
Shutdown your wallet and re-open your wallet.
Go to “Settings”. 
Click “Unlock Wallet”. 
Enter your wallet passphrase and unlock your wallet.
Go to “Tools”. 
Click “Debug console”. 
Start your masternode using the command.
masternode start-alias MN1

It will take +/- 30 minutes to activate your masternode.
