## Avail Validator setup (systemd)
```
sudo apt update
```
```
sudo apt-get update
```
```
sudo apt-get upgrade
```
```
sudo apt install make clang pkg-config libssl-dev build-essential
```
```
curl https://sh.rustup.rs/ -sSf | sh
```
```
source $HOME/.cargo/env
```
```
rustup update nightly
```
```
rustup target add wasm32-unknown-unknown --toolchain nightly
```
```
cd ..
```
# Create file
```
sudo mkdir /root/avail-node/
```
```
cd /root/avail-node/
```
# Check correct version from this link and wget it!
'https://github.com/availproject/avail/releases'
```
wget https://github.com/availproject/avail/releases/download/v1.7.0/data-avail-linux-amd64.tar.gz
```
```
wget https://kate.avail.tools/chainspec.raw.json
```
# Extract the file
```
tar xvzf data-avail-linux-amd64.tar.gz
```
# Change ''XXXX'' section and add your validator name. For example: ''Peertodevs''
```
sudo tee /etc/systemd/system/availd.service > /dev/null <<'EOF'
[Unit]
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0

[Service]
User=root
Type=simple
Restart=always
RestartSec=120
ExecStart=/root/avail-node/data-avail-linux-amd64 --base-path /root/avail-node/data --chain /root/avail-node/chainspec.raw.json --port 30333 --validator --name "XXXX"

[Install]
WantedBy=multi-user.target
EOF
```

# Run your node
```
sudo systemctl daemon-reload
```
```
sudo systemctl enable availd.service
```
```
sudo systemctl restart availd.service
```
# Check the status and logs 
```
sudo systemctl status availd.service
```
```
journalctl -f -u availd.service
```
# Check your node on this monitoring site.
https://telemetry.avail.tools/

# After the synchronization you can participate to the network with your tokens.


```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

# Get ''0x.......................................'' code and save it.

# Restart the node
```
sudo systemctl restart availd.service
```
# Wait for the sync a little bit. After the sync you can bond your tokens from this site.  
https://kate.avail.tools
# Network-Staking-Account-Stash-Bond-Add session key and validate.

## Congraculations!
