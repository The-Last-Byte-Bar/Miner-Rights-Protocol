# Token-Quarry

# A Mining Rights NFT & Token Emission Protocol

A protocol enabling the sale of mining rights tokens that grant holders the ability to claim NFTs when they successfully mine blocks. This creates a mineral rights-like system where miners must first acquire rights before being eligible for NFT emissions.

## Stage ToC
1. [Rights Sale Stage](#Stage-Rights-Sale)
2. [Mining Rights Holding Stage](#Stage-Mining-Rights-Holding)
3. [Block Discovery Stage](#Stage-Block-Discovery)
4. [NFT Emission Stage](#Stage-NFT-Emission)

## Action ToC
1. [Bootstrap Rights Sale](#Action-Bootstrap-Rights-Sale)
2. [Purchase Rights](#Action-Purchase-Rights)
3. [Bootstrap NFT Emission](#Action-Bootstrap-NFT-Emission)
4. [Claim NFT](#Action-Claim-NFT)

---

## Stage: Rights Sale
This stage handles the sale of mining rights tokens to potential miners. Each rights token represents the ability to claim NFTs when successfully mining blocks.

### Registers
- R4: Price per mining right (in nanoERGs)
- R5: Service fee percentage
- R6: Protocol wallet address
- R7: Rights token ID

### Hard-coded Values
- Minimum purchase amount
- Maximum rights per address
- Protocol version

### Context Extension Values
1. Buyer's public key
2. Amount of rights to purchase

### Mandatory Stage Spending Conditions
- Payment must meet minimum purchase amount
- Cannot exceed maximum rights per address
- Service fee must be paid to protocol wallet

### Actions/Spending Paths
- [Purchase Rights](#Action-Purchase-Rights)

---

## Stage: Mining Rights Holding
Represents the state where miners hold rights tokens. This stage doesn't have a contract but defines the requirements for holding mining rights.

### Required Tokens
- Mining rights token with positive balance

### Hard-coded Values
- Rights token ID
- Token validity period (if applicable)

---

## Stage: Block Discovery
Activated when a rights-holding miner finds a block, enabling NFT emission.

### Registers
- R4: Block height of discovery
- R5: Miner's public key
- R6: Rights token ID used
- R7: Block hash

### Hard-coded Values
- Claim window duration
- Protocol version
- Minimum confirmations required

### Context Extension Values
1. Block header data
2. Mining rights proof

### Mandatory Stage Spending Conditions
- Block must be found by rights holder
- Must be within claim window
- Required confirmations must be met

### Actions/Spending Paths
- [Claim NFT](#Action-Claim-NFT)

---

## Stage: NFT Emission
Final stage where NFT is created and distributed to the successful miner.

### Registers
- R4: NFT properties derived from block
- R5: Original block height
- R6: Recipient address

### Hard-coded Values
- NFT issuance rules
- Protocol version

### Context Extension Values
1. NFT metadata

---

## Action: Bootstrap Rights Sale
Initializes the rights sale contract.

### Inputs
1. Initial funding box with ERGs for contract operation
2. Configuration box with protocol parameters

### Outputs
1. Rights sale contract box containing:
   - Sale price in R4
   - Fee percentage in R5
   - Protocol wallet in R6
   - Rights token ID in R7

---

## Action: Purchase Rights
Allows users to purchase mining rights tokens.

### Inputs
1. Payment box with sufficient ERGs
2. Rights sale contract box

### Outputs
1. Updated rights sale contract box
2. Buyer's box containing rights tokens
3. Protocol wallet box receiving fees

### Action Conditions
1. Payment must meet minimum purchase amount
2. Correct number of rights tokens must be minted
3. Protocol fee must be paid
4. Cannot exceed maximum rights per address

---

## Action: Bootstrap NFT Emission
Creates the NFT emission capability for the protocol.

### Inputs
1. Funding box for NFT minting
2. Protocol configuration box

### Outputs
1. NFT emission contract box with:
   - Initial funding for NFT minting
   - Protocol parameters
   - Rights token verification data

---

## Action: Claim NFT
Allows rights-holding miners to claim NFTs for blocks they've found.

### Data-Inputs
1. Block header data
2. Rights verification data

### Inputs
1. Miner's rights token box
2. Block discovery stage box

### Outputs
1. NFT transfer to miner
2. Updated rights token box
3. Protocol fee payment (if applicable)

### Action Conditions
1. Must prove block discovery
2. Must hold valid rights token
3. Must be within claim window
4. Must have sufficient confirmations

---

### Protocol Economics

#### Rights Token Sale
```
Price Structure:
- Base Price: X ERG per right
- Service Fee: Y% to protocol
- Mint Funding: Z% to emission contract
```

#### Funding Requirements
```
Initial Funding = (Expected_NFTs * Mint_Cost) + Protocol_Buffer
Rights Sale Price = (Mint_Cost + Service_Fee + Protocol_Fee)
```

#### Token Distribution
```
For each purchase of N rights:
1. N * Service_Fee -> Protocol Wallet
2. N * Mint_Cost -> Emission Contract
3. N Rights Tokens -> Buyer
```

Would you like me to expand on any part of the specification or add additional details about specific aspects of the protocol?
