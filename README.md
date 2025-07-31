 GitHub-Ready README.md
markdown
Copy
Edit
# 🚀 Quick Guide: Deploying Helios Smart Contracts with Hardhat & Chronos

This guide helps you deploy a smart contract to the **Helios Testnet** using **Hardhat** and automate tasks using **Chronos**. Optimized for Windows CMD users.

---

## 1. 🛠️ Environment Setup

- Install **Node.js v18+** and npm  
  👉 [Download Node.js](https://nodejs.org/)

- Install **MetaMask**, create a testnet wallet

- Get HLS testnet tokens from the [Helios Faucet](https://faucet.helioschainlabs.org) for deployment and gas fees

---

## 2. 📁 Clone the Project Repository

```bash
git clone https://github.com/azrim/helios-lottery.git
cd helios-lottery
3. 📦 Install Dependencies
bash
Copy
Edit
npm install
💡 Ignore deprecated warnings unless they stop the installation.

4. ⚙️ Setup .env File
Copy the example environment file (for Windows CMD):

bash
Copy
Edit
copy .env.example .env
Then open .env with a text editor (preferably VS Code) and add your private key:

env
Copy
Edit
PRIVATE_KEY=0xYOUR_FULL_PRIVATE_KEY_HERE
✅ Make sure it's a full 66-character private key including the 0x prefix, without quotes or extra spaces.

5. 🧾 Configure hardhat.config.js
Ensure the configuration file looks like this:

js
Copy
Edit
require("dotenv").config();
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.30", // or "0.8.20" for stability
  networks: {
    helios_testnet: {
      url: "https://testnet1.helioschainlabs.org",
      chainId: 42000,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};
6. 🔨 Compile the Smart Contract
Make sure you're in the project directory:

bash
Copy
Edit
npx hardhat compile
7. 🚀 Deploy to Helios Testnet
bash
Copy
Edit
npx hardhat run scripts/deploy.js --network helios_testnet
Wait for the message: Deployment Successful!

💾 Save the deployed contract address for later use.

8. ✅ Verify the Contract (Optional but Recommended)
Extract constructor input data for verification:

bash
Copy
Edit
npx hardhat run scripts/extract-input.js
Then follow the instructions in verify-smart-contracts.md.

9. ⏱️ Schedule Automated Task with Chronos
Open scripts/schedule.js and replace this line:

js
Copy
Edit
const contractAddress = "YOUR_DEPLOYED_CONTRACT_ADDRESS";
Then run:

bash
Copy
Edit
npx hardhat run scripts/schedule.js --network helios_testnet
This sets up an automatic task (e.g. drawWinner) every 24 hours using Chronos.

