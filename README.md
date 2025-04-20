# ERC20 and ERC721 Token Deployment

## Project Overview

This repository contains Solidity smart contracts for deploying custom ERC20 and ERC721 tokens using Remix IDE. It provides:

- A customizable ERC20 token contract.
- A customizable ERC721 (NFT) contract.
- Deployment instructions for Remix.
- Basic usage examples.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Contracts](#contracts)
  - [ERC20 Token](#erc20-token)
  - [ERC721 Token](#erc721-token)
- [Deployment Guide](#deployment-guide)
  - [Using Remix](#using-remix)
- [Usage](#usage)
- [Folder Structure](#folder-structure)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v12 or later)
- Git (for version control)
- A web browser (Chrome, Firefox, or Brave)
- [MetaMask](https://metamask.io/) wallet extension
- Familiarity with Solidity and Ethereum basics

## Installation

1. **Clone this repository**
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```

2. **Open Remix IDE**
   - Navigate to [Remix Ethereum IDE](https://remix.ethereum.org).
   - Create a new workspace or open an existing one.

3. **Import Contracts**
   - In Remix’s File Explorer, click the “+” icon to create new Solidity files.
   - Copy `ERC20Token.sol` and `ERC721Token.sol` from this repository into your workspace.

## Contracts

### ERC20 Token

- **Filename:** `ERC20Token.sol`
- **Description:** Implements a standard ERC20 token with:
  - Custom name, symbol, and initial supply.
  - Minting capability for the owner.
  - Adjustable decimals.

```solidity
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(uint256 initialSupply) ERC20("MyToken", "MTK") {
        _mint(msg.sender, initialSupply);
    }

    function mint(address to, uint256 amount) external {
        _mint(to, amount);
    }
}
```

### ERC721 Token

- **Filename:** `ERC721Token.sol`
- **Description:** Implements a standard ERC721 non-fungible token (NFT) with:
  - Custom name and symbol.
  - Safe minting function.

```solidity
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract MyNFT is ERC721 {
    uint256 public nextTokenId;

    constructor() ERC721("MyNFT", "MNFT") {}

    function mintNFT(address to) external {
        _safeMint(to, nextTokenId);
        nextTokenId++;
    }
}
```

## Deployment Guide

### Using Remix

1. **Compile**
   - In the Solidity Compiler tab, select `0.8.x`.
   - Click **Compile** for each contract file.

2. **Deploy**
   - Switch to the **Deploy & Run Transactions** tab.
   - Select **Injected Web3** to connect MetaMask (ensure you're on the desired network: Ethereum Mainnet, Ropsten, etc.).
   - Choose the contract (`MyToken` or `MyNFT`).
   - For `MyToken`, enter the `initialSupply` (e.g., `1000000` for 1,000,000 tokens).
   - Click **Deploy** and confirm the transaction in MetaMask.

3. **Interact**
   - After deploying, your contract instance appears under **Deployed Contracts**.
   - Expand it to call `mint`, `balanceOf`, `mintNFT`, etc.

## Usage

- **ERC20**:
  ```js
  // Example: Check token balance
  const balance = await myToken.balanceOf("0xYourAddress");
  console.log(balance.toString());
  ```

- **ERC721**:
  ```js
  // Example: Mint an NFT
  await myNFT.mintNFT("0xRecipientAddress");
  ```

## Folder Structure

```
├── contracts
│   ├── ERC20Token.sol
│   └── ERC721Token.sol
├── README.md
└── .gitignore
```

## Testing

> *Note: Remix has limited testing support. For automated tests, consider migrating to Hardhat or Truffle.*

## Contributing

Contributions are welcome! Please open an issue or submit a pull request:

1. Fork the repository.
2. Create your feature branch: `git checkout -b feature/YourFeature`.
3. Commit your changes: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature/YourFeature`.
5. Open a Pull Request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

