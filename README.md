# Rust-Predict: Substrate Prediction Protocol (with Ink!)


## Overview

rust-predict is an open-source prediction protocol implemented in Rust using the Ink! smart contract framework. It is designed to work seamlessly with the AlephZero blockchain and is compatible with any Substrate blockchain supporting Ink!.

The repository includes the following components:

1. **Prediction Market Smart Contract**: A smart contract that facilitates prediction markets on a ubstrate blockchain. Users can create, participate in, and resolve prediction markets using this contract.

2. **Conditional PSP22 Token**: A conditional token standard based on PSP22, allowing the creation of tokens that represent binary predictions. Those tokens can be traded on a (decentralized) exchange.

3. **CPAMM (Constant Product Automated Market Maker)**: A typical mechanism for trading underlying conditional tokens. CPAMM provides automated market-making functionality, enabling users to trade conditional tokens in a decentralized manner as well as earn fees by providing liquidity.

4. **Frontend with UI**: A user interface for interacting with the smart contracts. The frontend provides a user-friendly experience for creating and participating in prediction markets, managing conditional tokens, and trading on the CPAMM.

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- Contracts: make, rustup, cargo (https://www.rust-lang.org/tools/install)
- Frontend: npm, vite

### Installation

1. Make necessary adjustments to the first three lines of the .env file

2. Install the 1.69 toolchain for Rust:

    ```bash
    rustup toolchain install 1.69.0
    ```

3. Clone the repository:

    ```bash
    git clone https://github.com/your-username/rust-predict.git
    ```

4. Change into the project directory:

    ```bash
    cd rust-predict
    ```

5. Build the smart contracts:

    ```bash
    make
    ```

6. Deploy the contracts to the blockchain. View `scripts` directory for deployment scripts.

### Usage

1. Deploy the Prediction Market Smart Contract, Conditional PSP22 Token, and CPAMM on the AlephZero blockchain.

2. Access the frontend on your local machine
```bash
cd frontend
pnpm install
pnpm dev
```

3. Use the UI to interact with the smart contracts. Create and participate in prediction markets, manage conditional tokens, and trade on the CPAMM.

## Contributing

We welcome contributions from the community! If you would like to contribute to rust-predict, please open an issue or submit a pull request.

## License

rust-predict is currently proprietary.
