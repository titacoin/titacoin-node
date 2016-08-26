Installing Titacoin

Once you connect to the VPS, create and log into user tita.

$ useradd -m tita

$ su tita

$ cd ~

Now you can download Titacoin.


$ wget https://github.com/titacoin/titacoin-node/archive/master.zip

--2015-10-10 03:34:36--  https://github.com/titacoin/titacoin-node/archive/master.zip
Resolving github.com (github.com)... 192.30.252.32

Unarchive the downloaded file.

$ tar -zxvf Titacoin-linux.tar.gz 

Titacoin-linux/
Titacoin-linux/configs/
Titacoin-linux/Titacoind
Titacoin-linux/simplewallet
Titacoin-linux/walletd
...
Saving the configuration file

Log into the Titacoin directory

$ cd Titacoin-linux
Write your configuration file

$ cat >configs/titacoin.conf 

EMISSION_SPEED_FACTOR=18
DIFFICULTY_TARGET=60
CRYPTONOTE_DISPLAY_DECIMAL_POINT=8
MONEY_SUPPLY=10000000000000000
GENESIS_BLOCK_REWARD=10000000000000000
SYNC_FROM_ZERO=1
DEFAULT_DUST_THRESHOLD=1000


MAX_BLOCK_SIZE_INITIAL=25600
MINIMUM_FEE=1000
DEFAULT_FEE=1000
MAX_TRANSACTION_SIZE_LIMIT=19400

CRYPTONOTE_MINED_MONEY_UNLOCK_WINDOW=20
CRYPTONOTE_BLOCK_GRANTED_FULL_REWARD_ZONE=100000
CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX=19
p2p-bind-port=41041
rpc-bind-port=41042
BYTECOIN_NETWORK=ae6088f8-ca03-f042-5ab2-f1e611879d0b
CRYPTONOTE_NAME=titacoin
GENESIS_COINBASE_TX_HEX=011401ff0001808084fea6dee11102f2028c81c48059459414d3dd455177564f26ed12f610f205c685262ecd8921ab210124d1c8b0d62e30b4c6e9796a0f75fd4f768063c01c1756fc068383d47326beee
UPGRADE_HEIGHT_V2=1
UPGRADE_HEIGHT_V3=2

seed-node=104.236.10.81:41041


Starting in upstart

Log with root user and change the directory to /etc/init/.

$ cd /etc/init
Create the upstart config file.

$ cat >Titacoin-titacoin-daemon.conf 

description "titacoin daemon"

start on runlevel [23]
stop on shutdown

exec sudo -u tita /home/tita/Titacoin-linux/Titacoind --no-console --config-file /home/tita/Titacoin-linux/configs/titacoin.conf

post-stop exec sleep 30

respawn
respawn limit 5 30

Start the service.

$ start Titacoin-titacoin-daemon 
You now have your seed node up and running. It will automatically restart if something goes wrong.

Stopping the service.

$ stop Titacoin-titacoin-daemon 
