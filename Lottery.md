### Lottery Smart Contract

#### 1. Introduction
   - **General Description**: This smart contract implements a monthly lottery based on NFTs, where users owning NFTs from different collections can participate to win tokens.
   - **Objective**: Provide a transparent and automated mechanism to randomly draw winners from multiple NFT collections and distribute the winnings in tokens.
   - **Prerequisites**:
     - One or more collections (modifiable after deployment)
     - Equal or different chances of winning among collections (e.g., Collection 1 has three times the chance of winning as Collection 2) (modifiable after deployment)
     - Free or paid tickets (modifiable after deployment)
     - Prizes can be tokens or NFTs

#### 2. Architecture and Components
   - **Main Components**:
     - Participation Management: Recording user participation (one ticket per NFT).
     - Random Draw: Mechanism for randomly selecting winners.
     - Prize Distribution: Transfer of tokens to the winners upon claiming.
     - State Storage: Keeping records of participations and winners, draw after draw.
   - **Interactions**:
     - Interaction with NFT collections to validate participations (paid or not).
     - Management of signature transactions for participations.
     - Execution of transactions for the draw and prize distribution.

#### 3. Functional Specifications
   - **Main Features**:
     - Recording monthly user participation.
     - Monthly random drawing of winners.
     - Distribution of winnings in tokens.
   - **Detailed Use Cases**:
     - **Use Case 1**: Recording a Participation
       - User signs a transaction to participate.
       - Alternatively, the user buys a ticket.
     - **Use Case 2**: Executing the Draw
       - Random selection of winners among the participants when a whitelisted address executes the draw transaction, simultaneously sending the tokens to be distributed.
       - Draws consider the number of tickets played and the probability of a collection winning.
     - **Use Case 3**: Claiming Prizes
       - Winner claims their tokens.
   - **User Workflow**:
     - User owning NFTs participates by signing a transaction.
     - Smart contract records the participation and validates the NFT.
     - At the end of the period, a draw is conducted and winners are updated.
     - Winners claim their prizes.

#### 5. Smart Contract Interface
   - **APIs and Entry Points**:
     - `register_participation(address, nft_id)`: Register a participation.
     - `execute_draw()`: Execute the draw.
     - `claim_prize(address)`: Claim a prize.
   - **Input and Output Parameters**:
     - Input: User's address, NFT ID.
     - Output: Participation confirmation, prize details.
   - **Events and Notifications**:
     - `ParticipationRegistered(address, nft_id)`: Notification of a registered participation.
     - `DrawExecuted(winner_list)`: Notification of the draw winners.
     - `PrizeClaimed(address, amount)`: Notification of a claimed prize.

#### 6. Technical Specifications
   - **Data Structures**:
     - `Participant`: Structure to store participant details.
     - `Winner`: Structure to record winners of each draw.
     - `Collection`: Structure to manage different NFT collections and their probabilities of winning.
   - **Algorithms and Processing Logic**:
     - Random draw algorithm based on collection weights.
     - Prize distribution management.
   - **State Management and Storage**:
     - States to record monthly participations.
     - States to record the results of the draws.
   - **Security Models**:
     - Validation of participant signatures.
     - Restricted access to critical functions to whitelisted addresses.