# A proposal for a bitcoin non-coerced hard-fork

With the, what seems, constant attacks on bitcoin in the past year attempting to co-opt the consensus rules, and adopt changes that lead to centralization concerns, I've thought many times of whether it is possible to safely hard-fork.  Given the choice between an attacking miner, and forking away to a safer set of consensus rules, I don't believe that this would present too much of an issue.  However, the implementation of Segregated Witness (i.e. SegWit), when the consensus changes were overwhelmingly supported, were still contentious, and there was a concerted social media compaign to undermine the bitcoin core open source development group.

There have been many discussions and suggestions that core has agreed that there should need to be some hard-fork required at some point in the future to address scalability issues.  Given the adversarial nature of bitcoin and consensus, I can't see how 100% of the current nodes of bitcoin could ever migrate from one set of consensus rules to another.  This is not to be confused with a soft-fork, where existing users may still continue using their node client.  True, there are some safety issues with continuing to use older node client software, but there are other ways that these safety concerns can be alleviated.  

I'd like to start a dialogue on how this might be achieved, with a suggestion on how it might be implemented without forcing existing bitcoin users to migrate to a different set of consensus rules, but still allow node users that are interested in expanding the protocol to meet new use-cases, to safely do so.  Following is what I think might be the beginning of a framework that might allow bitcoin to be migrated to a different set of consensus rules, like the adoption of an alternate hashing algorithm, without disenfranchising any of the existing bitcoin users. 

If I'm completely mistaken, I'll be the first to admit it, and I have broad shoulders, so have at it!

# The Issues

It is my belief that any hard-fork in bitcoin that doesn't have 100% acceptance of the consensus enforcing nodes is the creation of an alt-coin.  Because it is effectively impossible to source the opinion of the node owners for a given change, any proposal for a hard-fork will never be able to source the desirability for a change until the mechanism for the hard-fork is activated, and then you learn what the support is.  Any voting mechanism will not accurately reflect support.

There are many users in bitcoin that continue to use very old node reference clients.  It should always be of great concern if even 1% of the users of bitcoin don't agree with any conensus change if it disenfranchises them the safety and security of the social contract they believe they have with the maintainers of the environment, by removing the infrastructure that is necessary for them to continue using their node.  There are many people that are not concerned with block sizes, nor transaction fees, nor even mining centralization.

Added onto that is the issue of mining infrastructure.  Whether miners are malicious or not, it has to be recognized that any attempt to change the mining hashing algorithm will be met with great resistance, and deservedly so.  Even if a change of this nature was arguably justifiable as a result of a 51% attack by a large miner or group of miners, the non-attacking miners will be negatively affected in the same way as the attacking mining interest is.  This is a long-term untenable position for both miners, and for the maintainers of the consensus rules.  It should also be recognized the amount of resources that have been invested into that part of bitcoin security.  They must be protected from disenfranchisement as well.


# The Proposal : Dual-Locked chains.

In a discussion on reddit with jonny1000 about the feasibilty of implementing a dual-locking chain mechanism, it would seem to be broadly possible.  The proposal is this :

Definitions : 

              Old Chain = The pre-fork bitcoin blockchain.

              New Chain = A post-fork blockchain.

A consensus rule change hard-fork (the new chain) is created and populated with locked coins that may only be unlocked utilizing the private keys of the chain prior the fork (the old chain).  The key to unlock the coins on the new chain must be the result of a scripted output of an X block-depth (100?) lock transaction script.  The output of this script becomes the key that unlocks value on the the new chain.  The new chain is locked, with coins available to anyone that is prepared to unlock them using the private keys sourced from in the old chain. So the same as a regular hard-fork. But the unlocking process on the new chain requires a transaction on the old chain detailing how the coins at that address have been spent on the old chain and are no longer redeemable.

The transaction to migrate to the new chain is the transaction output of the old chain proving that the coins have been permanently locked.  It is placed into the transaction pool of the nodes of the new chain.  As the transaction pool increases with more transactions, the value behind that increases.  The incentive to mine this chain is explained below in mining rewards.  


# Mining rewards and coin supply

The issue for the enablement of the new chain is the issue of block rewards, and how one can bootstrap the mining environment.  It is also critically important to recognize the effect of a split chain will have the bitcoin supply.  By establishing a new chain, you are in effect doubling the reward schedule for miners.  

The proposal is to have block rewards calculated as a function of the percentage of bitcoin that has been migrated to the new chain.  Because each node and each miner will have knowledge of the transactions that lead to bitcoin migration, the block reward that is awarded the miner is increased accordingly, and the transaction is added to the new blockchain.

  Example :
  
    12.5 old chain block reward * 1.567% = 1.9875 btc reward.

The other schedule to introduce is the transfer value between the chains.  Because the old chain is still going up in rewards, the migration value for each transaction should be a function of the amount of coins that have been transferred and the amount of coins that exist in the new chain.  At first block of coins being migrated the value returned to the holder in the new chain is 100% of the coin count of the migration count.  If the new chain has 25% of the coin count of the old chain already committed, the amount of coins offered in the new chain is 75% of the coins being migrated from the old chain.

(Hmm... I think I have to think about that a bit more.  That is not quite right.)

The coin supply situation is therefore resolved in the new chain, because while the schedule of coin creation on the new chain will always be lower than the coin creation on the old chain, the migration is gradually lowering the amount of coins awarded in the new chain during migration.  It puts the ceiling on the total number of coins created in the new chain, which is < the previous chain. Each chain aligns on a value that is a reflection of the   If the new chain maintains the same block creation schedule on the new chain, it becomes a choice which chain you use, one or the other, not about having value on both chains. Because of the lock on the old chain, gradually the old chain would have less and less value available to it as value is transferred to the new one. 

This will allow the transaction pool being maintained by the nodes to act as a futures market to miners.  It will also incentivize miners mining blocks that are formed from the migration between chains, because each of these transactions will lead to an increase of the block reward.


# Miscellaneous


The other thing you could do would be to increase the decimal count in the new chain. As Luke Dashrj was kind enough to explain to me once, it is actually the satoshi that is the base level of bitcoin. The bitcoin determination of eight decimal places is arbitrary. But with the new chain, it would be possibl to nominate the arbitrary count as 16 decimal places, and the transfer of value from the old chain could be redeemed in the new chain as 1x108 satoshis.  This provides an even greater granularity than is currently possible.  Given enough thought on any new mining algorithm, this could have quite positive ramifications with regard to scalability.


# Conclusion

The primary concern for any consensus rule change, the risk of the disenfranchising the users that do not want to adopt a consensus change.  This proposal should allow new mining algorithms to be introduced into a bitcoin blockchain, and for 


# References :

[1]  https://www.reddit.com/r/Bitcoin/comments/6u30sc/block_494784_segwit2x_developers_set_date_for/dlqfe00/
     Discusison with https://www.reddit.com/user/jonny1000 about dual-locking chain feasibility.


