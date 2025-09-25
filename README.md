## 0G Alignment Node Guide Remake by P2Pnodetop
Step-by-step guide to set up and run a 0G AI Alignment Node, including installation, configuration, and operation instructions with example commands and images. Designed for both beginners and experienced node operators.

## 1. System Requirements
![System Requirements](Images0G/Requirement.png)

## 2. Installation & Setup
Step 1: Install dependencies, if needed

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl git wget htop screen build-essential jq make lz4 gcc unzip -y
```
Install Go
```bash
wget https://go.dev/dl/go1.22.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
echo "export GOROOT=/usr/local/go" >> ~/.bash_profile
echo "export GOPATH=\$HOME/go" >> ~/.bash_profile
echo "export PATH=\$GOPATH/bin:\$GOROOT/bin:\$PATH" >> ~/.bash_profile
source ~/.bash_profile
```
Create a screen session to run in the background.
```bash
screen -S AI0G
```
Download the latest 0G alignment node binary from the official repository:
```bash
wget https://github.com/0gfoundation/alignment-node-release/releases/download/v1.0.0/alignment-node.tar.gz
tar -xzf alignment-node.tar.gz
cd alignment-node
chmod +x 0g-alignment-node
```
Step 2: Configure Environment
a. Copy the example environment file:
```bash
cp .env.example .env
```
b. Edit the .env file with your configuration:
```bash
nano .env
```
c. Configure the following parameters:
```bash
export ZG_ALIGNMENT_NODE_LOG_LEVEL=debug
export ZG_ALIGNMENT_NODE_SERVICE_IP="http://IP Public:34567"  # Example: http://36.50.176.xxx:34567
export ZG_ALIGNMENT_NODE_SERVICE_PRIVATEKEY= Enter the private key that holds the NFT here, omit the 0x
```
d. Open port on Firewall
```bash
sudo ufw allow 34567/tcp
sudo ufw reload
```
Step 3: Start Your Node
a. Load environment variables:
```bash
source .env
```
b. Register the operator: Before performing this step, you need to have some ETH on the ARB mainnet in your wallet to cover the fees.
```bash
./0g-alignment-node registerOperator --key <Privatekey> --token-id <ID NFT> --chain-id 42161 --rpc https://arbitrum-one-rpc.publicnode.com --contract 0xdD158B8A76566bC0c342893568e8fd3F08A9dAac
```
### Note:
```bash
--key <Privatekey>: Enter the private key that holds the NFT here, omit the 0x.
--token-id <ID NFT>: If your wallet has 5 NFTs, you only need to enter 1 NFT ID as a representative, no need to enter all 5.
```
c. Start your Node:
```bash
./0g-alignment-node start --mainnet > node.log 2>&1 &
```
View logs: /root/alignment-node/node.log

Result: 
![System Requirements](Images0G/Logsfile.png)
```bash
time="2025-09-24T12:36:20+02:00" level=info msg="Verified identity result" address=0xabcxyz
time="2025-09-24T12:36:20+02:00" level=info msg="Starting server on port 34567"
```
d. After finishing, you need to press Ctrl A + D to detach and return to the main screen.
 ### Note: 
 If you want to check the status of the screen, you need to type:
 ```bash
 screen -r AI0G
 ```
Step 3: Delegate the wallet holding the NFT to the Operator on the 0G dashboard
Website: https://claim.0gfoundation.ai/
![System Requirements](Images0G/Delegateondashboard.png)
### Note: After you select the NFT, click delegate, and sign the transaction, you need to reload the site and perform the delegate action once more to complete it. At this point, the NFT status will show as pending.
Step 4: After completing step 3, you need to return to the server's main screen to run the final command: Approve NFT delegation

```bash
./0g-alignment-node approve --mainnet \
  --key <Privatekey> \
  --chain-id 42161 \
  --rpc https://arbitrum-one-rpc.publicnode.com \
  --contract 0xdD158B8A76566bC0c342893568e8fd3F08A9dAac \
  --destNode <Address hold NFT> \
  --tokenIds <ID1,ID2,ID3,ID4,ID5>
```
### Note: 
```bash
--key <Privatekey>: Enter the private key of the regisOperator wallet.
--destNode <Address hold NFT>: The wallet address holding the NFT is required to delegate into the regisOperator wallet.
--tokenIds <ID1,ID2,ID3,ID4,ID5>: Enter the NFT ID of the destNode wallet
```
Result: After running it, please go back to the dashboard to check that the status has changed from pending to delegated.
![System Requirements](Images0G/Delegated.png)

### Node command help
```bash
./0g-alignment-node --help
./0g-alignment-node <command> --help
```

## 🚀 Connect with Me

Stay in touch and follow my updates:

- **X (Twitter)**: [@p2pnodetop](https://x.com/p2pnodetop)  
- **Discord**: `p2pnodetop`  
- **Telegram**: `P2Pnodetop`

Let's build and explore the 0G ecosystem together! 🌌

  































