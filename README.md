# Install-Avail-Full-Node
# This is a guide for installing Avail Node on Ubuntu 22.04.
 Video:
 https://youtu.be/HYBzK-jJIeQ

  *** 
X1.** Install Rust**

```
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

2.**After ensuring you have Rust installed, you can run the Avail Node using the following command:**

```
git clone https://github.com/availproject/avail.git
cd avail
mkdir -p output
git checkout v1.10.0.0
cargo run --locked --release -- --chain goldberg --validator -d /root/avail/output --reserved-nodes "/dns/bootnode-001.goldberg.avail.tools/tcp/30333/p2p/12D3KooWCVqFvrP3UJ1S338Gb8SHvEQ1xpENLb45Dbynk4hu1XGN" "/dns/bootnode-002.goldberg.avail.tools/tcp/30333/p2p/12D3KooWD6sWeWCG5Z1qhejhkPk9Rob5h75wYmPB6MUoPo7br58m" "/dns/bootnode-003.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMR9ZoAVWJv6ahraVzUCfacNbFKk7ABoWxVL3fJ3XXGDw" "/dns/bootnode-004.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMuyLE3aPQ82HTWuPUCjiP764ebQrZvGUzxrYGuXWZJZV" "/dns/bootnode-005.goldberg.avail.tools/tcp/30333/p2p/12D3KooWKJwbdcZ7QWcPLHy3EJ1UiffaLGnNBMffeK8AqRVWBZA1" "/dns/bootnode-006.goldberg.avail.tools/tcp/30333/p2p/12D3KooWM8AaHDH8SJvg6bq4CGQyHvW2LH7DCHbdv633dsrti7i5" --reserved-only
```
**This command complies and runs the Avail Node connected to the Kate Network.
**
```
2023-10-11 16:11:31 Avail Node    
2023-10-11 16:11:31 ✌️  version 1.7.0-ad024ff050e    
2023-10-11 16:11:31 ❤️  by Anonymous, 2017-2023    
2023-10-11 16:11:31 📋 Chain specification: Avail Kate Testnet    
2023-10-11 16:11:31 🏷  Node name: decorous-trade-0251    
2023-10-11 16:11:31 👤 Role: FULL    
2023-10-11 16:11:31 💾 Database: RocksDb at /tmp/substrateJwM8xd/chains/Avail Testnet_116d7474-0481-11ee-bc2a-7bfc086be54e/db/full    
2023-10-11 16:11:32 🔨 Initializing Genesis block/state (state: 0x6bc8…8ac6, header-hash: 0xd120…50c6)    
2023-10-11 16:11:32 👴 Loading GRANDPA authority set from genesis on what appears to be first startup.    
2023-10-11 16:11:33 👶 Creating empty BABE epoch changes on what appears to be first startup.    
2023-10-11 16:11:33 🏷  Local node identity is: 12D3KooWMmY2QLodvBGSiP1Cg9ysWrPSMN19qK3w35mRnUhq6pMX    
2023-10-11 16:11:33 Prometheus metrics extended with avail metrics    
2023-10-11 16:11:33 💻 Operating system: linux    
2023-10-11 16:11:33 💻 CPU architecture: x86_64    
2023-10-11 16:11:33 💻 Target environment: gnu    
2023-10-11 16:11:33 💻 CPU: 13th Gen Intel(R) Core(TM) i7-13700K    
2023-10-11 16:11:33 💻 CPU cores: 16    
2023-10-11 16:11:33 💻 Memory: 31863MB    
2023-10-11 16:11:33 💻 Kernel: 6.5.5-100.fc37.x86_64    
2023-10-11 16:11:33 💻 Linux distribution: Fedora Linux 37 (Workstation Edition)    
2023-10-11 16:11:33 💻 Virtual machine: no    
2023-10-11 16:11:33 📦 Highest known block at #0    
2023-10-11 16:11:33 〽️ Prometheus exporter started at 127.0.0.1:9615    
2023-10-11 16:11:33 Running JSON-RPC server: addr=127.0.0.1:9944, allowed origins=["http://localhost:*", "http://127.0.0.1:*", "https://localhost:*", "https://127.0.0.1:*", "https://polkadot.js.org"]    
2023-10-11 16:11:33 🏁 CPU score: 1.65 GiBs    
2023-10-11 16:11:33 🏁 Memory score: 19.49 GiBs    
2023-10-11 16:11:33 🏁 Disk score (seq. writes): 6.74 GiBs    
2023-10-11 16:11:33 🏁 Disk score (rand. writes): 2.65 GiBs    
2023-10-11 16:11:33 🔍 Discovered new external address for our node: /ip4/176.61.156.176/tcp/30333/ws/p2p/12D3KooWMmY2QLodvBGSiP1Cg9ysWrPSMN19qK3w35mRnUhq6pMX    
2023-10-11 16:11:34 [811] 💸 generated 9 npos targets    
2023-10-11 16:11:34 [811] 💸 generated 9 npos voters, 9 from validators and 0 nominators    
2023-10-11 16:11:34 [#811] 🗳  creating a snapshot with metadata SolutionOrSnapshotSize { voters: 9, targets: 9 }    
2023-10-11 16:11:34 [#811] 🗳  Starting phase Signed, round 1.
```
**
Press Ctrl + A + D to exit the screen
**

3. **Create Systemd**
```
sudo touch /etc/systemd/system/availd.service
sudo nano /etc/systemd/system/availd.service
```

**Change your Validator name and copy/paste it**

```
[Unit] 
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart= /root/avail/target/release/data-avail -d /root/avail/output --chain goldberg --validator --name "Dinhcongtac221" --reserved-nodes "/dns/bootnode-001.goldberg.avail.tools/tcp/30333/p2p/12D3KooWCVqFvrP3UJ1S338Gb8SHvEQ1xpENLb45Dbynk4hu1XGN" "/dns/bootnode-002.goldberg.avail.tools/tcp/30333/p2p/12D3KooWD6sWeWCG5Z1qhejhkPk9Rob5h75wYmPB6MUoPo7br58m" "/dns/bootnode-003.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMR9ZoAVWJv6ahraVzUCfacNbFKk7ABoWxVL3fJ3XXGDw" "/dns/bootnode-004.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMuyLE3aPQ82HTWuPUCjiP764ebQrZvGUzxrYGuXWZJZV" "/dns/bootnode-005.goldberg.avail.tools/tcp/30333/p2p/12D3KooWKJwbdcZ7QWcPLHy3EJ1UiffaLGnNBMffeK8AqRVWBZA1" "/dns/bootnode-006.goldberg.avail.tools/tcp/30333/p2p/12D3KooWM8AaHDH8SJvg6bq4CGQyHvW2LH7DCHbdv633dsrti7i5" --reserved-only
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target

```
**Save it: CTRL+X** .

P/s: My username is root what I used to login my Vps.

 data-avail file in this directory. 

![image](https://github.com/DinhCongTac221/Install-Avail-Full-Node/assets/27664184/1b1a15bb-edbf-44be-ba44-669a2cc90273)



**To enable this to autostart on bootup run:**

```systemctl enable availd.service```

Start it manually with:

```systemctl start availd.service```

You can check that it's working with:

```systemctl status availd.service```

You can tail the logs with journalctllike so:

```journalctl -f -u availd```

Check your node on https://telemetry.avail.tools
![image](https://github.com/DinhCongTac221/Install-Avail-Full-Node/assets/27664184/c70aaf66-ccbc-485e-ae9e-c09674425772)



# ** Guide Update to v1.10.0 by built from source**
**run commands**
 
```
systemctl stop availd.service
```
run the command to know **your data dir** and add more flags
```
sudo nano /etc/systemd/system/availd.service
```
![image](https://github.com/DinhCongTac221/Install-Avail-Full-Node/assets/27664184/e590ccc0-e5b3-4aec-8290-08da0ab81cd9)

in this picture, my data dir is '/root/avail/output '

copy and paste all to end of  ExecStart=  
```
--reserved-nodes "/dns/bootnode-001.goldberg.avail.tools/tcp/30333/p2p/12D3KooWCVqFvrP3UJ1S338Gb8SHvEQ1xpENLb45Dbynk4hu1XGN" "/dns/bootnode-002.goldberg.avail.tools/tcp/30333/p2p/12D3KooWD6sWeWCG5Z1qhejhkPk9Rob5h75wYmPB6MUoPo7br58m" "/dns/bootnode-003.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMR9ZoAVWJv6ahraVzUCfacNbFKk7ABoWxVL3fJ3XXGDw" "/dns/bootnode-004.goldberg.avail.tools/tcp/30333/p2p/12D3KooWMuyLE3aPQ82HTWuPUCjiP764ebQrZvGUzxrYGuXWZJZV" "/dns/bootnode-005.goldberg.avail.tools/tcp/30333/p2p/12D3KooWKJwbdcZ7QWcPLHy3EJ1UiffaLGnNBMffeK8AqRVWBZA1" "/dns/bootnode-006.goldberg.avail.tools/tcp/30333/p2p/12D3KooWM8AaHDH8SJvg6bq4CGQyHvW2LH7DCHbdv633dsrti7i5" --reserved-only
```
run commands to **delete db and network** folder. ( change your data dir)

```
rm -r /root/avail/output/chains/avail_goldberg_testnet/db/*
rm -r /root/avail/output/chains/avail_goldberg_testnet/network/*
```

install lz4
```
sudo apt-get -y install lz4
```

Run the command to download snapshot ( change your data dir )
```
curl -o - -L http://snapshots.staking4all.org/snapshots/avail/latest/avail.tar.lz4 | lz4 -c -d - | tar -x -C /root/avail/output/chains/avail_goldberg_testnet/
```
and run commands to restart it

```
sudo systemctl daemon-reload
sudo systemctl enable availd.service 
sudo service availd start 
systemctl status availd.service
```
