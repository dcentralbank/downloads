# downloads

Decentralbank.com and dcentralcoin:
Decentralization is the process of redistributing or dispersing functions, powers, people or things away from a central location or authority. By definition, it is to move power away from a central authority, like a bank or government. Decentralization means that no single organization or entity has absolute power over a certain aspect of society.
Dcentralbank has all the elements that are necessary to make a functional, decentralized banking system. With the rise of the internet, this is especially relevant. Be your own bank. A decentralized system doesn’t only bring the benefit of not having to trust a central bank to do the job, but you also get to avoid unnecessary fees. Because you are dealing with other people within the decentralized system, instead of going through a middleman. Decntralcoin offers total payment confidentiality, maintaining a decentralised network using a public blockchain.

Getting started
Use the following instructions to mine a block.
Open your wallet, and make sure your wallet is connected with a node. 
Your wallet is connected when you see the icon in the lower right corner of your wallet.
The message “Syncing Headers (0,0%)” will disappear once you mine your first block.
Open your wallet.
Create a .bat file named mine.bat in the same folder where you extracted dcentralcoin-cli.exe and paste the following text into mine.bat.
@echo off
set SCRIPT_PATH=%cd%
cd %SCRIPT_PATH%
echo Press [CTRL+C] to stop mining.
:begin
 dcentralcoin-cli.exe generate 1
goto begin 
Save the file.
Execute mine.bat to start mining your first block.
It will take about +/- 30 minutes to mine your first block, depending on your computer hardware.
