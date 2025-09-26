#Install Foundry
``curl -L https://foundry.paradigm.xyz | bas
foundryup
forge init``

#Create new project
``mkdir myproject``

``cd myproject
forge init``

#Compiling the smart contract

``// SPDX-License-Identifier: MIT
pragma solidity ^0.8.23;``

``import "openzeppelin-contracts/contracts/token/ERC721/ERC721.sol";``

``contract NFT is ERC721 {
    uint256 public currentTokenId;``

    constructor() ERC721("NFT Name", "NFT") {}

    function mint(address recipient) public payable returns (uint256) {
        uint256 newItemId = ++currentTokenId;
        _safeMint(recipient, newItemId);
        return newItemId;
    }
}``

And run command
``forge install openzeppelin/openzeppelin-contracts``

Note: In your project, add above code in a new file called src/NFT.sol

And run command
``forge build``

#Storing your privatekey
``cast wallet import deployer --interactive``


Note: Your private key is stored in ~/.foundry/keystores


#Adding Base as a network
``BASE_MAINNET_RPC="https://mainnet.base.org"
BASE_SEPOLIA_RPC="https://sepolia.base.org"
ETHERSCAN_API_KEY="<YOUR API KEY>"``

Note: you can gwt ApiKey here:
https://etherscan.io/apidashboard

And then use command
``source .env``

#Deploying the smart contract
``forge create ./src/NFT.sol:NFT --rpc-url $BASE_SEPOLIA_RPC --account deployer --broadcast``


#Verifying the Smart Contract
``forge verify-contract <DEPLOYED_ADDRESS> ./src/NFT.sol:NFT --chain 8453 --watch``


