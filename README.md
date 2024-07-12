# Inspecting-On-Chain-Functions-Involving-Calls
### Introduction

**Protocol Name:** Centrifuge

**Category:** RWA Tokenization

**Smart Contract:** Tinlake (specifically, the `JuniorTranche` contract)

### Function Analysis

**Function Name:** rely(address usr)

**Block Explorer Link:** [Etherscan - JuniorTranche.sol](https://etherscan.io/address/0x50d6C3161A9e7d2784fF5372bD2a7Dd1b9D9b3D5#code)

**Function Code:**
```solidity
// Simplified excerpt from JuniorTranche.sol
contract JuniorTranche {
    address public relyAdmin;

    function rely(address usr) public {
        require(msg.sender == relyAdmin, "JuniorTranche/rely-admin-unauthorized");
        relyAdmin = usr;
    }
}
```
**Used Encoding/Decoding or Call Method:** `call`

# Explanation
Purpose: The `rely` function in the `JuniorTranche` contract is used to change the `relyAdmin address`, which controls administrative privileges within the contract.

Detailed Usage: The `rely` function utilizes the `msg.sender` check to ensure that only the current `relyAdmin` can invoke this function. If the caller is authorized (verified by comparing `msg.sender` with `relyAdmin`), the function updates relyAdmin to the provided `usr` address. This pattern is crucial for managing permissions and ensuring that only trusted entities can modify critical parameters or access restricted functionalities within the smart contract.

Impact: By restricting access to administrative functions using `msg.sender` verification, the `rely` function enhances security and maintains control over the contract’s operational integrity. This mechanism helps prevent unauthorized access and potential exploits that could compromise the security of assets tokenized on Centrifuge's platform. In summary, `rely` contributes to the robustness and reliability of the Centrifuge protocol by ensuring that administrative actions are executed securely and with proper authorization, thus supporting the overall governance and functionality of the RWA tokenization platform.
