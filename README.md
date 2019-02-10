# Solidity Web Automation Tool 

This tool is built on top of [truffle-suite](https://github.com/trufflesuite/ganache-cli) &
[express.js](https://github.com/expressjs/express) and is meant for deploying server-side code. The client-side is implemented using  [web3.js](https://github.com/ethereum/web3.js).
It automatically and dynamically generates client-side code for accessing your smart-contracts. This tool simplifies the implementation of distributed apps (dapp), by taking care of configurations and auto-generating client api's.

## How to get started:
**1. Initialize truffle**    
It will generate `contracts` and `migrations` folders.
```
truffle init
```   
**2. Uncomment network configurations in `truffle-config.js`**
```
networks: {
     development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
     },
...
}
```
**3. Run the Ethereum Node**    
```
ganache-cli
```
**4. Implement your solidity smart contracts in the `contracts` folder**   
The migration files are autogenerated. They can be customized after deployment (step 5) and be redeployed again to update changes.
    
**5. Deploy your contracts in another terminal**    
The command below will deploy contracts and use the default configurations as defined in `truffle-config.js` (step 2).   
```
solidity-web
```    
Custom port and host for the webserver can be set as follows:
```
solidity-web web-host=<host> web-port=<port-number>
```

This command calls truffle's `truffle migrate` command underneath, which compiles the `.sol` files and creates a `build` folder with json files.
On top of this, the `solidity-web` tool will generate an `app` folder, which contains the server- and client-side implementation. The `app.js` file is the server-side code, which launches the container. 
It can be changed to add rest functionality or or frontend code (HTML/Javascript/CSS). The `contracts.js` file creates a reference for each smart-contract.
For demonstration purposes, an `index.html` is already present and references all smart-contract instances defined in `contract.js`.

**6. Start the express webserver**   
```
node app/web/app.js
```     
The default url is http://localhost:8181