
This is a work in progress, spelling errors, grammar and all that.  If I'm completely mistaken, I'll be the first to admit it, and I have broad shoulders, so have at it!



# A proposal for a bitcoin non-coerced hard-fork (NCHF)

With the, what seems, constant attacks on bitcoin in the past year attempting to co-opt the consensus rules, and adopt changes that lead to centralization, I've thought many times of whether it is possible to safely hard-fork at all.  Given the choice between an attacking miner, and forking away to a safer set of consensus rules, I don't believe that this would present too much of an issue.  However, the implementation of Segregated Witness (i.e. SegWit) showed us that even when the consensus changes were overwhelmingly supported by the users of bitcoin, they were still contentious, and there was a concerted social media compaign to undermine the bitcoin core open source development group.

There have been many discussions and suggestions that core has agreed that there should need to be some hard-fork required at some point in the future to address scalability issues.  Given the adversarial nature of bitcoin and consensus, I can't see how 100% of the current nodes of bitcoin could ever migrate from one set of consensus rules to another.  This is not to be confused with a soft-fork, where existing users may still continue using their node client.  True, there are some safety issues with continuing to use older node client software, but there are other ways that these safety concerns can be alleviated.  

Of paramount importance is the protection of existing node owners from the loss of funds as a result of a consensus change.  Node owners should not require to upgrade their node for years at a time, or even at all.

I'd like to start a dialogue on how a non-coerced hard-fork (NCHF) might be achieved, with a suggestion on how it might be implemented without forcing existing bitcoin users to migrate to a different set of consensus rules, but still allow node users that are interested in expanding the protocol to meet new use-cases, to safely do so.  Following is what I think might be the beginning of a framework that might allow bitcoin to be migrated to a different set of consensus rules, like the adoption of an alternate hashing algorithm, without disenfranchising any of the existing bitcoin users. I would also suggest that the proposed solution may be a way to incrementally implement mining algorithm changes that don't needlessly punish miners for the perception of a risk of centralization.



# What is Coercion in the context of bitcoin?

Coercion in the NCHF relates to the requirement of a node owner to upgrade their node client to a version that recognizes a consensus rule change. If a node owner is forced to upgrade their node client in order to continue using bitcoin, they are being coerced to do so.

The premise of a hard-fork is that it has broad consensus, having a feature-set that is desirable, or it will not be proposed in the first place. The NCHF proposal makes no comment on the specifics of the hard-fork architecture or feature-set desirability of the new chain. The proposal demonstrates that even after the hard-fork, bitcoin may still be safely used without leading to a chain-split that requires a node owner to change their node client software. It is this lack of a requirement of users to change their node client that defines the lack of coercion. It makes no comment on whether the feature-set of the new chain or the old chain is more desirable. Having a more desirable feature-set is not to be confused with coercion to use that feature-set.


# The Issues

It is my belief that any hard-fork in bitcoin that doesn't have 100% acceptance of the consensus enforcing nodes in bitcoin is the creation of an alt-coin.  Because it is effectively impossible to source the opinion of the node owners for a given change, any proposal for a hard-fork will never be able to source the desirability for a change until the mechanism for the hard-fork is activated, and then you learn what the support is.  Any voting mechanism will not accurately reflect support.

There are many users in bitcoin that continue to use very old node reference clients.  It should always be of great concern if even 1% of the users of bitcoin don't agree with any conensus change if it disenfranchises them from the safety and security of the social contract they believe they have with the maintainers of the environment, by removing the infrastructure that is necessary for them to continue using their node.  There are many people that are not concerned with block sizes, nor transaction fees, nor even mining centralization.

Added onto that is the issue of mining infrastructure.  Whether miners are malicious or not, it has to be recognized that any attempt to change the mining hashing algorithm will be met with great resistance, and deservedly so.  Even if a change of this nature was arguably justifiable as a result of a 51% attack by a large miner or group of miners, the non-attacking miners will be negatively affected in the same way as the attacking mining interest is.  This is a long-term untenable position for both miners, and for the maintainers of the consensus rules.  It should also be recognized the amount of resources that have been invested in the integral part of bitcoin security that is mining.  They must be protected from disenfranchisement as well.


# The Proposal : Dual-Locked chains with aligned incentives.

In a discussion on reddit with jonny1000 about the feasibilty of implementing a dual-locking chain mechanism, it would seem to be broadly possible.  The proposal is this :

Definitions : 

              Old Chain = The pre-fork bitcoin blockchain.

              New Chain = A post-fork blockchain.

A consensus rule change hard-fork (the new chain) is created and populated with locked coins that may only be unlocked utilizing the private keys of the chain prior the fork (the old chain).  So the same as a regular hard-fork.  This proposal, however, generates this key to unlock the coins on the new chain as a function that is the result of a scripted output of an X block-depth (100?) lock transaction script.  The output of this script becomes the key that unlocks value on the the new chain.  

The new chain always has access to the current UTXO set (Not the entire blockchain) of the old chain but locked, with coins available to anyone that is prepared to unlock them using the private keys sourced from in the old chain. But the unlocking process on the new chain requires a transaction on the old chain detailing how the coins at that address have been spent on the old chain and are no longer redeemable.  Because the node maintains both the old chain and the new chain UTXO sets, it always 'knows' when funds are available for migration between the old chain and the new chain.

The transaction to migrate to the new chain is the transaction output of the old chain proving that the coins have been  permanently locked.  It is placed into the transaction pool of the nodes of the new chain when a user seeks to spend the coins on the new chain.  As the transaction pool increases with more transactions, the value behind that increases, incentivizing mining activity on the new chain.

The proposal is to modify the base unit of bitcoin to be 10^8 units for each existing satoshi.  For each unit in the old chain, new coins are available in the new chain to the tune of 10^8 multipled by a coin-count comparison between the old and the new chains.  It is explained in more detail the mining rewards and coin supply section.

Migration of value between chains shall be implemented such that the address space in the new chain is not linked to the address space in the old chain.  Because the act of migration to the new chain involves the output of a transaction on the old chain, that transaction is initiated on the new chain can happen at any time in the future.  It should therefore be possible to completely unlink the address space on the old chain with the new chain while at the same time ensure only coins that have been locked in the old chain are available for new chain transactions.  There are many proposals for confidential transactions that could be implemented in the new chain that would further this aim, but that is not the scope of this proposal.

The three model pictures demonstrate the propogation of nodes in the new chain through the network.  consensus-Model1, 2, and 3, as pdf and image.  Note how the 'available value' in the old chain gradually reduces as it is migrated to the new chain.

While the NCHF has many similarities to side-chains, it differs in a number of key areas.  First, transactions are one way.  They may only be migrated from the old chain to the new chain.  Two, it specifically aligns in its mining reward schedule in the new chain, and its value migration schedule from old chain to new chain, so that the the values of the old and new chains should broadly align.  A side-chain may have a completely arbitrary mining solution that devalues (or provides no mining rewards at all) the coins in relation to the old chain.  The NCHF proposal specifically aligns the release schedules to reflect the value that has been already transferred to the new chain.


# Mining rewards and coin supply

The issue for the enablement of the new chain is the issue of block rewards, and how one can bootstrap the mining environment.  It is also critically important to recognize the effect that a split chain will have on the total bitcoin coin supply.  By establishing a new chain, you are in effect doubling the reward schedule for miners.  

The proposal is to have block rewards calculated as a function of the percentage of bitcoin that has been migrated to the new chain.  Because each node and each miner will have knowledge of the transactions that lead to bitcoin migration, the block reward that is awarded the miner is increased accordingly, and the transaction is added to the new blockchain.

  Example :
  
    12.5 old chain block reward * 1.567% = 1.9875 btc reward.

The other schedule to introduce is the transfer value between the chains.  Because the old chain is still going up in rewards at the bitcoin release schedule, the migration amount of coins received for each transaction should be a reflection of the difference between the coin release schedules.  As more coins are available in the old chain by design, the ratio of coins redeemed in the new chain should be lower.  This can be done by multiplying the coins to be migrated by the ratio of the total number of coins in the new chain and the number of coins in the old chain. 

  Example :
    100 coins to transfer * (17M in the new chain / 20M in the old chain) = 85 coins in the new chain.
    
The first block of coins being migrated will have the value returned to the holder in the new chain at 100% of the coin count of the coins for migration, because no block in the new chain has been created, and the block counts align.  Any remaining 'dust' shall be discarded at the lowest granularity of the new chain.

The coin supply situation is therefore resolved in the new chain, because while the schedule of coin creation on the new chain will always be lower than the coin creation on the old chain, the migration is gradually lowering the amount of coins awarded in the new chain during migration.  It puts the ceiling on the total number of coins created in the new chain, which is < the previous chain.  Each chain aligns on a value that is a reflection of the ratio between the old chain and the new chain.  If the new chain maintains the same block creation schedule on the old chain, it becomes a choice which chain you use, one or the other, not about having value on both chains. Because of the lock on the old chain, gradually the old chain will have less and less value available to it as that value is transferred to the new one.  But the value of each coin on the old chain should be maintained, and aligned with the new coin.

At its inception, the pool of transactions to be mined on the new chain will allow the transaction pool being maintained by the nodes to act as a futures market to miners on the new chain.  It will also incentivize miners mining blocks that are formed from the migration between chains, because each of these transactions will lead to an increase of the block reward.  Very large transactions from the old chain to the new chain will lead to very large block rewards, of which the successful miner is the first to take advantage of.

It must be tested to determine what the most appropriate difficulty reset schedule should be given the staged migration.  The implementation of this schedule is not the scope of this proposal.


# Node behaviour

The memory pool for each chains would be maintained with by the new nodes, but old nodes would only manage the transactions that apply to the old chain.  As more value is migrated to the new chain, with the expectation of greater utility, the incentive will be to migrate coins to the new chain.  But because the values are tied on a set release and reward schedule, the values of the two chains should align.

New chain nodes should have read and write capability for peers that continue to want to transact on old chain consensus rules. Transactions should be coded to be backwards compatible with any existing format, and yet extend the functionality to cater for new chain requirements.  The transaction and integration of the node client should allow for the integration of both transaction formats, enabling the user to migrate to the new chain if signed appropriately.  It should also allow for the user to use entirely old node infrastructure without ever being exposed to the new chain, while ensuring that there isn't any rapid decrease in security by either abandoning existing mining infrastructure, nor existing mining infrastructure abandoning them. 

Users should still be able to choose which node client they run.  It should be possible to only run a node as an old chain node, or a new chain node.  The only restriction would be that migration transactions could not be validated on nodes that don't have the functionality of both node types.  But for users that only ever want to transact on one chain, they will not require validating any blocks or transactions that they will never have any interest in.


# Miscellaneous

To cater for the coin transferrance multiplication factors, an increase the decimal count in the new chain will alleviate issues with the application of these ratios. As Luke Dashjr was kind enough to explain to me once, it is actually the satoshi that is the base level of bitcoin. The bitcoin determination of eight decimal places is arbitrary. But with the new chain, it would be possible to nominate the arbitrary count as 16 decimal places, maintaining the bitcoin moniker, but for it to represented as 10^16 in the new chain.  The transfer of value from the old chain should be redeemed in the new chain as (10^8) satoshis.  This provides an even greater granularity than is currently possible.  Given enough thought on any new mining algorithm, this could have other positive ramifications with regard to scalability.  But that is not the scope of this proposal.



# Discussion

It must be studied what possible price effect might be generated on the new chain in the first blocks being migrated.

The mining algorithm might effect how blockchains are tied?

Given the the greater granularity in the new chain, it might be possible to use the increased transaction address space to develop an algorithm that will be able to use the deterministic public and private key allocation to store encrypted information in the deterministic space.

It would be broadly possible to disconnect the actual coin count in the new chain such that they always aligned with the coin count in the old chain.  This could conceivably incentivize migration to the new chain, because as the coin mining reward schedule between the old chain and the new chain will always be greater in the old chain, the ratio between old chain and new chain will always be positive.  In effect, this would provide a deflationary effect on the new chain such that the value of coins migrated to the new chain increase in value at a greater rate than the coins in the old chain, and this effect will increase the longer the time the coins are in the new chain.


# Conclusion

The primary concern for any consensus rule change is alleviating the risk of the disenfranchising the users that do not want to adopt a consensus change.  This proposal should allow new mining algorithms to be introduced into a bitcoin blockchain, and even provides a framework for multiple mining algorithms.

This also does not disenfranchise existing bitcoin holders, nor does it disenfranchise existing miners.


# References :

[1]  https://www.reddit.com/r/Bitcoin/comments/6u30sc/block_494784_segwit2x_developers_set_date_for/dlqfe00/
     Discusison with https://www.reddit.com/user/jonny1000 about dual-locking chain feasibility.


