# 2x2coin


https://2x2coin.com     Official Website<br>
https://explorer.2x2coin.com     ( Blockexplorer including API )<br>
<br>
Hashing algorithm: x11<br>
Proof type: Proof-of-Stake<br>
Block time: 90 seconds<br>
Coin maturity: 24 hours<br>
Staking period: minimum 24 hours<br>
Staking rewards:365% per year<br>
Transaction fee:min 1 coin<br>
Coinbase maturity: 40 confirmations<br>
Supply:unlimited<br>


## How to compile and use the Linux Deamon
Tested and working on Ubtunu 14 - 16.04 and 18.04 Version.<br>
Versions 20.04 and later do not currently compile due to changes in OpenSSL 1.1
and the Boost C++ library in that version.

### Swapfile

You can check if your server has a swap file already with the ```swapon``` command.  If your system has less than 1.5GB of memory, you'll want at least a 2GB swap area.  Add a new swapfile with:
```
sudo fallocate -l 2G /swapfile
sudo chown root:root /swapfile
sudo chmod 0600 /swapfile
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
sudo mkswap /swapfile
sudo swapon /swapfile
```
If fallocate doesn’t work, you can instead use:
```
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1024288
```
Initialize the swapfile to mount automatically on boot:
```
sudo echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

### Install all required dependencies

```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get -y install nano ntp unzip git build-essential libssl-dev
sudo apt-get -y installlibdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude
sudo aptitude -y install miniupnpc libminiupnpc-dev
```
ubuntu 18.04
```
sudo apt-get install libssl1.0-dev
sudo apt-get install libqt4-dev
```

If you get an error mentioning lock files, you probably have a desktop or background package update tool running that prevents other apt changes from happening.  You can use the ```lsof``` utility to figure out what program holds the lock and then pause it from running.

Pull the source code from github, or download it yourself:
```
git clone https://github.com/coinsdevcode/2X2coin.git
```

### Compiling the software

Now you compile the included leveldb:
```
chmod +x 2x2coin
cd 2x2coin/src/leveldb
chmod +x build_detect_platform
make clean
make libleveldb.a libmemenv.a
```
Return to the source directory, and compile the daemon:
```
cd ..
make -f makefile.unix RELEASE=1
```
To compile qt (wallet with GUI) for Ubuntu 16.04 or 18.04 LTS use:
```
sudo apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools
sudo apt-get install libboost-system-dev
sudo apt-get install libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev
```
Return to the source directory, and compile the qt:
```
cd ..
qmake RELEASE=1
make STATIC=1
```
Strip the file to make it smaller, then relocate it:
```
strip 2X2d
sudo cp 2X2d /usr/bin
```
Now run the daemon:
```
2X2d
```
It should return an error, telling you to set up config file in a directory. 

## Create a config file

Now we’ll set up the config file. Note that this is case sensitive.<br>
Linux
```
nano ~/.2X2/2X2.conf
```
Winodws
```
C:\Users\YourUserName\AppData\Roaming\InfiniteRicks 
```
Add the following, save and exit:
```
stake=1
listen=1
daemon=1
server=1
rpcuser=(username)
rpcpassword=(strong password)
addnode=176.222.52.79
addnode=75.119.137.26
addnode=138.122.48.56
addnode=177.204.190.11
addnode=180.243.121.24
addnode=176.102.50.180
addnode=187.85.18.230
addnode=37.215.47.242
addnode=108.28.194.197
addnode=110.137.74.239
addnode=91.239.42.50
addnode=213.149.30.41
addnode=110.14.37.167
addnode=47.87.225.88
addnode=31.41.100.192
addnode=213.87.130.162
addnode=95.217.78.169
addnode=142.44.196.232
addnode=51.81.102.224
addnode=45.80.152.40
addnode=173.82.19.160
addnode=92.119.123.221
addnode=144.217.174.80
addnode=37.4.226.76
addnode=138.122.50.99
addnode=189.58.19.160
addnode=173.82.19.160
addnode=92.119.123.221
addnode=200.236.198.27
addnode=176.63.26.169
addnode=37.20.243.17
addnode=91.239.42.100
addnode=51.81.102.224
addnode=180.245.58.60
addnode=85.96.177.253
```
Run 2X2d once more and if you did everything correctly, your daemon is now online! 
## Command summary
Type:
```
help
```
for a full list of commands available.
## Attention!!!<br>
Do not keep more than 90,000,000,000 2X2 coins in your wallet.<br>
More than 90,000,000,000 coins becomes a negative balance.<br>
If you are lucky enough to have that much start a second wallet on another computer.

