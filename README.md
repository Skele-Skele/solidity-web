# Solidity Web Automation Tool 

This tool is built on top of [truffle-suite](https://github.com/trufflesuite/ganache-cli) and
[express.js](https://github.com/expressjs/express) for deploying server-side code. The client-side is implemented using  [web3.js](https://github.com/ethereum/web3.js).
It automatically and dynamically generates client-side code for accessing your smart-contracts. With this tool, you do not have to worry about configuration anymore, simply implement your smart-contracts, deploy and access them with the generated code. 

### Steps    
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
Keep in mind, that the migrations file will be autogenerated. If you want to customize them you can do so after performing step 5 and deploying again.   
    
**5. Deploy your contracts in another terminal**    
The command below will deploy your contracts and use the default configurations as defined in `truffle-config.js` (step 2).   
```
solidity-web
```    
This command calls truffle's `truffle migrate` command underneath, which compiles the `.sol` files and creates `build` folder with json files.
On top of this, the `solidity-web` tool will generate an `app` folder, which contains the client-side implementation. The `app.js` file is the server-side code, which launches the container. 
It can be changed to add rest functionality or html/javascript/css. The `contracts.js` file creates a reference for each smart-contract.
For demonstration purposes, an `index.html` is already present and references all smart-contract instances defined in `contract.js`.

**6. Start the express webserver**   
```
node app/web/app.js
```     
The default url is http://localhost:8181
