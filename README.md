# A proposal for a bitcoin non-coerced hard-fork

With the, what seems, constant attacks on bitcoin in the past year attempting to co-opt the consensus rules, and adopt changes that lead to centralization concerns, I've thought many times of whether it is possible to safely hard-fork.  Given the choice between an attacking miner, and forking away to a safer set of consensus rules, I don't believe that this would present too much of an issue.  However, the implementation of Segregated Witness (i.e. SegWit), when the consensus changes were overwhelmingly supported, were still contentious, and there was a concerted social media compaign to undermine the bitcoin core open source development group.

There have been many discussions and suggestions that core has agreed that there should need to be some hard-fork required at some point in the future to address scalability issues.  Given the adversarial nature of bitcoin and consensus, I can't see how 100% of the current nodes of bitcoin could ever migrate from one set of consensus rules to another.  This is not to be confused with a soft-fork, where existing users may still continue using their node client.  True, there are some safety issues with continuing to use older node client software, but there are other ways that these safety concerns can be alleviated.  

I'd like to start a dialogue on how this might be achieved, with a suggestion on how it might be implemented without forcing existing bitcoin users to migrate to a different set of consensus rules, but still allow node users that are interested in expanding the protocol to meet new use-cases, to safely do so.  Following is what I think might be the beginning of a framework that might allow bitcoin to be migrated to a different set of consensus rules, like the adoption of an alternate hashing algorithm, without disenfranchising any of the existing bitcoin users. 

If I'm completely mistaken, I'll be the first to admit it, and I have broad shoulders, so have at it!

# The Issues

It is my belief that any hard-fork in bitcoin that doesn't have 100% acceptance of the consensus enforcing nodes is the creation of an alt-coin.  Because it is effectively impossible to source the opinion of the node owners for a given change, any proposal for a hard-fork will never be able to source the desirability for a change until the mechanism for the hard-fork is activated, and then you learn what the support is.  Any voting mechanism will not accurately reflect support.

There are many users in bitcoin that continue to use very old node reference clients.  It should always be of great concern if even 1% of the users of bitcoin don't agree with any conensus change if it disenfranchises them the safety and security of the social contract they believe they have with the maintainers of the environment, by removing the infrastructure that is necessary for them to continue using their node.  There are many people that are not concerned with block sizes, nor transaction fees, nor even mining centralization.

Added onto that is the issue of mining infrastructure.  Whether miners are malicious or not, it has to be recognized that any attempt to change the mining hashing algorithm will be met with great resistance, and deservedly so.  Even if a change of this nature was arguably justifiable as a result of a 51% attack by a large miner or group of miners, the non-attacking miners will be negatively affected in the same way as the attacking mining interest is.  This is a long-term untenable position for both miners, and for the maintainers of the consensus rules.

# The Proposal : Dual-Locked chains.



# Mining Rewards

