# votechain-soc
This project aims to develop a blockchain based electronic voting system in Python.

Blockchain tutorial:

A blockchain is a growing list of records, called blocks, which are linked using cryptography. Each block contains a cryptographic hash of the previous block, a timestamp, and transaction data.

Double-spending: the sender spends the same money at more than one place for obtaining services or goods from multiple vendors.(for eg giving digital coin to one and its copy to another, where it being a copy cannot be verified). If every digital transaction is routed through a centralized authority that maintains a ledger book recording all the transactions, the problem of double-spending would be solved. 

Bitcoin: anonymity in the transactions; this ledger be public and maintained by the community;

Public Key Cryptography (PKI): asymmetric cryptography; It uses two pairs of keys(some long binary number) - public and private.

Hashing: A hash function maps the data of any arbitrary size to data of fixed size. If the message is modified, the hash value will change. Not only that given a hash value, it is impossible to reconstruct the original message.

Mining: Miners are machines which run a piece of software for mining the bitcoin message. A miner combines all messages received from various vendors in a single block and creates a hash on it with time-stamps that no third-party can modify without modifying the hash value. While creating the chain of blocks, hash of the previous block is added to the current block.

Nonce(proof of work): Nonce is a number such that the block’s hash meets a certain criterion.(like lets say that the generated hash must have its leading four digits to be zero) Generally, the miner starts with a Nonce value of 0 and keeps on incrementing it until the generated hash meets the specified criterion. The expected time for generating a block in bitcoin system is 10 minutes. 

Privacy: To achieve a higher degree of privacy, for every transaction, you may generate a new private/public key for each transaction so that multiple transactions made by you cannot be grouped together by a third party.

Merkle tree: The issue of disk space in a node is easily overcome because all transactions in a block are hashed in a Merkle Tree ![image](https://github.com/dhriti-13/votechain-soc/assets/157302650/9a428717-f52a-4862-a4be-e8e079474efb) 
The block header now contains the hash of the previous block, a Nonce, and the Root Hash of all the transactions in the current block in a Merkle Tree. As this Root Hash includes the hashes of all the transactions within the block, these transactions may be pruned to save the disk space.

Payment Verification: You can now search backwards in your copy of the blockchain until you find a block in which the desired transaction is timestamped in. Now, request the merkle tree of the selected block and you will have the transaction that you are looking for. Though you may not be able to see its contents, you know that this has been accepted by the block to which it belongs and all subsequent blocks in the chain. Thus, you can safely trust this transaction and proceed with your business.

In Bitcoin architecture, the longest branch always wins and the shorter ones are purged. Before purging this block, all transactions in this block will be returned to the transaction pool so that they are mined and added to some future block. This is how the conflicts are resolved and only one single chain of blocks is maintained by the system.

Race attack: Attacker may send the same coin to different vendors in rapid succession, probably by using two different machines. If the vendors do not wait for the block confirmation before delivering the goods, they will very soon realize that the transaction was rejected during the mining process.

Finney attack: The attacker is the miner. The miner mines a block with his transaction and does not release it in the system. He now uses the same coins in a second transaction and then releases the pre-mined block. Obviously, the second transaction would be rejected eventually by other miners, but this will take some time. To mitigate this risk, the seller should wait for at least six block confirmations before releasing the goods.

Bitcoin research paper:

A solution to the double-spending problem using a peer-to-peer distributed timestamp server to generate computational proof of the chronological order of transactions. The system is secure as long as honest nodes collectively control more CPU power than any cooperating group of attacker nodes.

We define an electronic coin as a chain of digital signatures. Each owner transfers the coin to the next by digitally signing a hash of the previous transaction and the public key of the next owner and adding these to the end of the coin.

In the mint based model, the mint was aware of all transactions and decided which arrived first. To accomplish this without a trusted party, transactions must be publicly announced, and we need a system for participants to agree on a single history of the order in which they were received. The payee needs proof that at the time of each transaction, the majority of nodes agreed it was the first receive.

Timestamp server: Each timestamp includes the previous timestamp in its hash, forming a chain, with each additional timestamp reinforcing the ones before it.

Proof-of-work: The proof-of-work is implemented by incrementing a nonce in the block until a value is found that gives the block's hash the required zero bits. Once the CPU effort has been expended to make it satisfy the proof-of-work, the block cannot be changed without redoing the work. Proof-of-work is essentially one-CPU-one-vote. The majority decision is represented by the longest chain, which has the greatest proof-of-work effort invested in it. If a majority of CPU power is controlled by honest nodes, the honest chain will grow the fastest and outpace any competing chains.

It adds an incentive for nodes to support the network, and provides a way to initially distribute coins into circulation, since there is no central authority to issue them. The incentive can also be funded with transaction fees. If the output value of a transaction is less than its input value, the difference is a transaction fee that is added to the incentive value of the block containing the transaction. Once a predetermined number of coins have entered circulation, the incentive can transition entirely to transaction fees and be completely inflation free.

 A user only needs to keep a copy of the block headers of the longest proof-of-work chain, which he can get by querying network nodes until he's convinced he has the longest chain, and obtain the Merkle branch linking the transaction to the block it's timestamped in.

 
