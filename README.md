# How to Run Bitcoin Core, Mempool, Electrum for $5/month

When you run your own node, you can verify transaction data, and get transaction data from a source you can trust completely.

You can run your own Bitcoin Node if you want to do anything that uses Bitcoin API / wallet access. 
If you need Bitcoin API access, it's probably cheaper to run your own node than to go to a service provider. 
You can easily run your own Bitcoin Node by getting a hosted "Storage VPS" since Bitcoin Core requires a lot of storage. 

## Minimum Requirements to run Bitcoin Core
https://bitcoin.org/en/bitcoin-core/features/requirements
<img width="739" alt="image" src="https://user-images.githubusercontent.com/1872138/184553857-2f73ce22-05ba-4c73-b102-7573a66559dc.png">


## Options for Cheap "Storage VPS" Service Providers:

#### Interserver

**Note: tested this and could not get an OS to install**
https://www.interserver.net/vps/storage.html
$6/month for 1TB / 1 CPU / 4GB RAM

#### Time4VPS
**Note: only supports older OS (example Debian 9, Ubuntu 16.04) - so you will need to run older versions of bitcoind**
https://time4vps.com
€4.49/month for 1TB / 1 CPU / 2GB RAM

Here is what my server usage looks like while synchronizing with the bitcoin chain:
<img width="680" alt="image" src="https://user-images.githubusercontent.com/1872138/184553692-9e5f64d3-8da7-46d7-8d70-d4e025b34948.png">

#### Contabo

**Note: seems like the best bang for your buck even though it's twice some of the others**
https://contabo.com/en/storage-vps
$10.99/month for 700GB / 4 CPU / 10GB RAM 

## Steps to Install Bitcoin Core (bitcoind)
* Purchase a server running Debian or Ubuntu using the links above
* SSH to the server
* Update apt `apt update && apt upgrade -y`
* Download bitcoind `wget https://bitcoin.org/bin/bitcoin-core-22.0/bitcoin-22.0-x86_64-linux-gnu.tar.gz`
* (if you are running debian9, then use an older version of bitcoind: `wget bitcoin-0.19.0.1-x86_64-linux-gnu.tar.gz`)
* Unpack `tar -zxvf bitcoin-22.0-x86_64-linux-gnu.tar.gz`
* Install `sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-22.0/bin/*`
* Run once to see if it works `bitcoind -daemon`
* Check log file `tail -f ~/.bitcoin/debug.log` 
* Stop bitcoind `bitcoin-cli stop`
* Set up your bitcoin.conf file `nano ~/.bitcoin/bitcoin.conf` file - recommend using the info below with own rpc user/pass here:
 ```
rpcuser=bitcoin 
rpcpassword=bitcoinpass 
rpcallowip=127.0.0.1
daemon=1 
minrelaytxfee=2500
maxconnections=20
maxuploadtarget=250
txindex=1
server=1
 ```
* Check the sync of your bitcoin node - I have written a little script here https://gist.github.com/bensig/4793be2327b1d535a70046a759a5e696

## Installing electrum and mempool
Follow the steps in the Github here:
Electrs v0.99 - https://github.com/romanz/electrs/blob/v0.8.0/doc/usage.md
Mempool v2.4.1 - https://github.com/mempool/mempool/tree/v2.4.1/backend#setup
