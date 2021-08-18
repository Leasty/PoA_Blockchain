# Proof of Authority Blockchain by Jay Richardson

---

# Creating a Proof of Authority Blockchain:

## Creating Nodes

* First, to create a PoA blockchain we will need to download Geth Tools from geth.ethereum.org. Download and extract to a folder called "Blockchain-Tools"

* Once downloaded, navigate to the Blockchain-Tools folder from Git Bash and we will generate two new nodes with account addresses.

* To create the two new nodes, run:
	- ./geth --datadir node1 account new
	- ./geth --datadir node2 account new

* copy the public address keys and store these for later use.

![node_image](./screenshots/node.jpg)

---

## Generate Genesis Block

* In Git Bash, navigate back to your Blockchain-Tools folder and run ./puppeth.exe

* Name your new network and 2.Configure new genesis -> Create new genesis -> Clique PoA -> all default options.

* When prompted to allow accounts to seal, provide the two addresses from the two nodes created previously and the same for pre-funding the accounts.

* Once the prompts are completed, you should be back at the main menu. Now choose "Manage existing genesis" and "Export genesis configurations". This will create new .json files in your folder in the name of your network.

---

## Initialise and Run Nodes

* In seperate Git Bash terminals, initialise each node using the new network.json (network is the name given to your new network) by running:
	- ./geth --datadir node1 init networkname.json
	- ./geth --datadir node2 init networkname.json

* In each terminal, we can begin to validate and mine blocks with the following code:
	- ./geth --datadir node1 --unlock "NODE_1_ADDRESS" --mine --rpc --allow-insecure-unlock
* The "Node_1_Address" is the public key of node1 that we copied down before. Once this node is running, search in the working terminal for "enode" and copy the full string. e.g. "enode://0xdaD099ee4a19c5D18a14076CBEE93399B60fccBb@127.0.0.1:30303". We will need this enode to validate with node2.

* You should be promted to enter your password that you have used when creating your PoA Blockchain.

* In the node2 terminal, run the following code:
	- ./geth --datadir node2 --unlock "NODE_2_ADDRESS" --mine --port 30304 --bootnodes "ENODE_STRING_FROM_NODE_1" --ipcdisable --allow-insecure-unlock.
* THe "Node_2_Address" and "Enode_String" were previously saved from the public key of the node2 account and the enode from initialising node1.

* You should be promted to enter your password that you have used when creating your PoA Blockchain.

* Keep both terminals up and running, you should be seeing block validations occuring.

---

## Connecting Your Wallet and Making a Transfer

* Download and install MyCrypto wallet from download.mycrypto.com

* Open MyCrypto and connect to your new PoA Blockchain network. Select "Change Network" on the screen and go to "Custom Node". The address is your local address 127.0.0.1:8545, Chain ID 999 (or any 3 digit number) and save.

* Now click on "Keystore File" to connect your wallet. Navigate through to your Blockchain-Tools folder and to your node1/keystore file. You will also need your password again.

![keystore_image](keystore.jpg)

* Once your wallet is connected to your node1 address, you will be able to send ETH from node1 to your node2 address and have the transaction validated on your blockchain!

* Alternatively, if MyCrypto is not responding well, export the private key of your node1 wallet from the drop down menu in wallet info and import to MetaMask.

![wallet_info](wallet_info.jpg)

* Sending and tracking transactions on MetaMask is easy, just send to the public address of node2

![send](send.jpg)

![where](where.jpg)

![sign](sign.jpg)



