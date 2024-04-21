# 0G-LABS
OG LABS repo node run
Go to : http://termius.com/download

➖ Download & install termius.

➖ Signup with email.

➖ Enter VPS, IP address.

➖ Username = root

➖ Enter VPS password.

➖ Click connect.
> sudo apt-get update && sudo apt-get upgrade -y
  >apt-get install git unzip wget snapd lz4 -y
> Set time zone & install GO language>>commands a) timedatectl set-timezone UTC b) wget https://golang.org/dl/go1.21.4.linux-amd64.tar.gz
> Extract folder & add GO to the environment ---- tar -C /usr/local -xzf go1.21.4.linux-amd64.tar.gz  /   export PATH=$PATH:/usr/local/go/bin
> Install 0G command terminal  commands a)  git clone -b testnet https://github.com/0glabs/0g-evmos.git b) ./0g-evmos/networks/testnet/install.sh   c) source .profile d) evmosd config chain-id zgtendermint_9000-1
>  Initialize node  a) evmosd init <NAME> --chain-id zgtendermint_9000-1  note - Replace <NAME> with your preferred name.
>  Install Genesis file a) wget -P ~/.evmosd/config https://github.com/0glabs/0g-evmos/releases/download/v1.0.0-testnet/genesis.json
> Accelerate synchronisation command without ()   (sed -i '/seeds =/c\seeds = "8c01665f88896bca44e8902a30e4278bed08033f@54.241.167.190:26656,b288e8b37f4b0dbd9a03e8ce926cd9c801aacf27@54.176.175.48:26656,8e20e8e88d504e67c7a3a58c2ea31d965aa2a890@54.193.250.204:26656,e50ac888b35175bfd4f999697bdeb5b7b52bfc06@54.215.187.94:26656"' $HOME/.evmosd/config/config.toml)
>  Install Screen a) apt install screen
> Download snapshots & back-up file a) wget https://rpc-zero-gravity-testnet.trusted-point.com/latest_snapshot.tar.lz4 b) cp $HOME/.evmosd/data/priv_validator_state.json $HOME/.evmosd/priv_validator_state.json.backup  c) evmosd tendermint unsafe-reset-all --home $HOME/.evmosd --keep-addr-book
> Extracting snapshot file a)  lz4 -d -c ./latest_snapshot.tar.lz4 | tar -xf - -C $HOME/.evmosd b) mv $HOME/.evmosd/priv_validator_state.json.backup $HOME/.evmosd/data/priv_validator_state.json
> Setup node using Systemd one command 27-41 without ()  ( sudo tee /etc/systemd/system/zerog.service > /dev/null <<EOF
[Unit]
Description=0G Node
After=network.target

[Service]
User=root
ExecStart=/root/go/bin/evmosd start
Restart=always
RestartSec=3
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
EOF)
Enter screen & start node a) screen b) systemctl daemon-reload
systemctl enable zerog
systemctl start zerog
> 
