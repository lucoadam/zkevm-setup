 **L1 EVM chains compatible to run ZkEVM**

 1\. Ethereum\
 2. Binance Smart Chain\
 3. Gnosis Chain (xDai)\
 4. Fantom\
 5. Avalanche\
 6. EVMOS\
 7. RSK\
 8. TomoChain\
 9. OKXChain\
 10. Canto\
 11. Astar\
 12. Telos\
 13. Ubiq\
 14. ThunderCore\
 15. Go Chain\
 16. Wanchain\
 17. Meter\
 18. Moonriver\
 19. KCC\
 20. Klaytn Cypress\
 21. Huobi ECO Chain\
 22. Songbird Canary-Network\
 23. Fuse\
 24. Syscoin

 **Requirements to run ZkEVM**

 A machine to run the ZkEVM node with the following requirements:\
 Hardware: 32G RAM, 4 cores, 128G Disk with high IOPS (as the network
 is super young the current disk requirements are quite low, but they
 will increase overtime. Also note that this requirement is true if the
 DBs run on the same machine, but it\'s recommended to run Postgres on
 dedicated infra). Currently, ARM-based CPUs are not supported\
 Software: Ubuntu 22.04, Docker\
 **Run L1 RPC Node**

 Running L1 RPC node enables us to get rid of limitations in currently
 available rpc. And also enhances performance, security, better control
 and securities.\
 For running it, follow the documentation of the corresponding L1
 chain.\
 Note: The L1 Node to be runned must be an archive node.

 For checking compatibility
 
```bash
curl -X POST \
   'https://l1-rpc.com' \
   --header 'Accept: */*' \
   --header 'Content-Type: application/json' \
   --data-raw '{
   "jsonrpc": "2.0",
   "method": "eth_getCode",
   "params": [
       "<anyDeployedLatestContractAddress>",
       "<blockNumberOfContractInHex:0x1b831a5>"
   ],
   "id": 1
   }'

```

 The result of above CURL should not contain \`missing trie node
 error\` **Setup ZkEVM contracts on L1**

 1\. Clone ZkEVM contracts repository to deploy contracts in L1 from\
 2. Install dependencies\
 3. Configure\
 a. menonics in the .env file, as in .env.example\
 b. Chain information in hardhat.config.js\
 Deployment parameters (deploy_parameters.json) (ref. c.

 deploy_parameters.json.example)\
 Set value from "admin", "zkevmOwner",\
 "initialZkEVMDeployerOwner" as first address from mnemonics.

 Also generate keystore files for aggregator and sequencer and update
 their addresses accordingly.

Note: The depolyerAddress must contain certain L1 funds for fees.

 d\. Update package.json script for particular L1 (prepare, deploy
 deployer, deploy ZkEVM, saveDeployment).

 4\. Run the following script prepared serially.

  ```bash
  npm run prepare:ZkEVM:{L1} && npm run deploy:deployer:ZkEVM:{L1} && npm run deploy:ZkEVM:{L1} && npm run saveDeployment:{L1}              
  ```

 5\. Backup the deployment generated config from deployments/{L1}..timestamp which includes

    a\. genesis.json
    b\. deploy-output.json
    c\. deploy-parameters.json

 **ZkEVM L2 Setup**

 1\. Download the pre-configuration zip

 Link:

 2\. Extract the zip and update sequencer.keystore,
 aggregator.keystore, test.genesis.config.json\
 3\. Change the necessary configuration\
 
 Replace the values of following keys:\
 
 ```
 L1URL=\
 URL=\
 GenBlockNumber=\
 PoEAddr=\
 BridgeAddr=\
 GlobalExitRootManAddr=\
 MaticAddr=\
 L2BridgeAddrs=(same as BridgeAddr)\
 L1ChainID=\
 ZKEVM_NODE_SEQUENCER_SENDER_ADDRESS=
 ZKEVM_NODE_AGGREGATOR_SENDER_ADDRESS= 
 ```
 4. Run the node using docker-compose.yml file.
