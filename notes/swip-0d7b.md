```yaml
---
title: Withdrawable stake
author: Andrew Macpherson (@awmacpherson)
discussions-to: https://discord.gg/Q6BvSkCv (Swarm Discord)
status: Draft
category: Core
created: 2024-08-07
---
```

# Pre-SWIP: Withdrawable stake

## Abstract

Make stake fully and ==instantly== withdrawable except while frozen or while participating in a round.

## Specification

* Introduce a new function `exit()` which withdraws the full stake balance as long as the address is not frozen, and clears the state.

* The functionality of `exit()` should be identical to calling `withdrawFromStake(amount)` with `amount` equal to the full stake balance, that is, the return value of `stakes()[msg.sender]`.

* The `withdrawFromStake` method gets a new parameter `uint256 amount` which is the amount to withdraw. The conditionals should be changed to the following:

  ```solidity
  if (addressNotFrozen(msg.sender) && !findCommit(msg.sender)) {
      // begin lock
      stakes[msg.sender] -= amount
      if !ERC20(bzzToken).transfer(msg.sender, amount)
          revert TransferFailed()
      // end lock
      emit StakeWithdrawn(msg.sender, amount);
  }
  ```

  Here `findCommit(owner)` is a function that finds a commit owned by `owner` in the `currentCommits` array in the Redistribution contract. It is similar to the internal method `findCommit(bytes32 _overlay, bytes32 _obfuscatedHash) internal view returns (uint256)`. For this function to be implementable, the stake registry would need a reference to the redistribution contract, which it currently does not have.

* Discontinue maintenance of the `CommittedStake` field of the stake registry. Stake weights are again provided by raw BZZ values.

## Rationale

* An option to fully withdraw stake under typical network conditions makes staking a much more attractive, low-risk investment opportunity. Because principal is not at risk, it improves the accessibility of staking to risk-averse operators such as those with worse acess to capital. It also makes the opportunity easier to compare on a like-for-like basis with other staking systems. For a more detailed analysis, see [here](https://mirror.xyz/shtuka.eth/qQnVGyNL7viiS5iLizSVL_0eTTMYGavl3Kb77XiaBxk).
* Since the main negative incentives active in Swarm Protocol today are based on freezing, exiting stake cannot be a method to evade freezing. That is, frozen nodes cannot be allowed to withdraw.
* Although additional frictions or conditions, such as a withdrawal delay, could be imposed on withdrawals, this proposal represents the simplest possible approach, could be deployed immediately, and doesn't make incentives to stay online any worse.

## Implementation notes

TODO

## Security implications

* We expect that this will result in more money being held in the stake registry contract, which accordingly scales the security concerns.

* *Instant unfreeze.* Frozen accounts cannot be allowed to withdraw. Otherwise, a depositor could evade freezing by simply withdrawing and opening a new account.

* *Consensus penalty evasion.* If withdrawals are allowed in the middle of a round, a depositor who commits but does not reveal, or one who reveals but considers the risk of being found in disagreement too high, can evade Non-revealed or Disagreement penalties by quickly withdrawing. To make these penalties effective, withdrawals in the middle of the round should therefore be restricted, at least until the end of that round.

  Either of the following restrictions would prevent penalty evasion:

  * Preventing withdrawal if the owner has already committed in the current round. This requires the withdraw function to carry a reference to the Redistribution contract.
  * A withdrawal delay of at least one round.

* *Shadow stake.* Withdrawals enable a strategy in which a large amount of stake is temporarily deposited in order to skew the leader election contest. Currently, the stake update cool-off period embedded in the `commit()` method prevents this strategy from being carried out after the round anchor is revealed. Upgrades should take care to preserve some thawing period after depositing (including topping up) stake.

## Economic implications

* Staking becomes substantially less risky because principal is not at risk, nor even particularly illiquid.
  * When slashing is introduced, principal is again at risk, but only in case of abnormal conduct.
  * When withdrawal delays are introduced, liquidity is impacted.
* The value of the principal gets added to the value of stake positions. This makes the value of staked BZZ comparable with other yield bearing assets such as treasuries. The market will likely accept a much lower yield per token ($r$ instead of $1+r$ ) and hence support a much larger deposit base ($Y/r$ instead of $Y/(1+r)$).
* Staking becomes accessible to a wider variety of economic actors.
* Currently, for a staked node sitting out of participation is disincentivised only by loss of revenue. Unstaking has the positive incentive of making capital immediately available, and implies sitting out of participation. So we have
  $$
  V(\neg \mathrm{P}) = O - R
  $$
  where $\mathrm{P}$ means "participate," $O$ is the variable operating cost of running the node, and $R$ is the revenue from participation. On the other hand,
  $$
  V(\mathrm{Unstake}) = LB(s) + O - R
  $$
   where $LB(s)$ is the liquidity bonus of having $s$ BZZ liquid instead of staked. Since instantly withdrawable stake is close to liquid, $LB(s)$ is likely to be pretty small here except in times of high trading activity when stakers may prefer to immediately trade their BZZ or post them as liquidity on an exchange.
  In times of high trading activity (high volatility, high volume), instantly withdrawable stake therefore entails a risk of higher node churn and potential network instability.

## Interactions with other proposals

* **SWIP-39.** Automatic address allocation is only binding if it is economically infeasible to reroll many times to achieve a desired prefix. Under the proposed scheme, withdrawals are instant and almost free, so they do not add any Sybil resistance to this scheme. Sybil-resistance could be introduced in a controlled manner by adding a tax or delay to withdrawals.
* **Non-custodial stake registry.** A non-custodial model for the stake registry separates the actions of *deregistering* stake, which disencumbers assets from their commitment to participation in the redistribution contest, and *withdrawing,* which actually transfers the assets out of the target account. In a non-custodial model, all references to "withdrawals" in the current proposal should apply specifically to deregistrations rather than moving assets, and its conditionals should be implemented within the redistributor contract which checks the conditions when the owner requests the lock be released.

## Alternative approaches

* **Withdrawal delay.** There are a few reasons that it may be desirable to enforce a delay on withdrawing assets after the intention to withdraw has been telegraphed. In this case, at least two actions would be required to withdraw: commit to withdraw, and execute withdrawal. For simplicity, this proposal specifies a single-action instant withdrawal.
* **Withdrawal queue.** In a system with a withdrawal delay, impose a hard limit on the number of nodes that can be waiting to exit at any one time. This is how Ethereum validator exits work. So far, we haven't established a need for this feature, which adds more complexity.
* **Address-based withdrawal restrictions.** Some discussions floated the idea of limiting withdrawals of nodes whose absence would cause the overlay address population to become "unbalanced" (for example, withdrawals from neighbourhoods that are already underpopulated).
* **Withdrawal tax.** Instead of being fully withdrawable, stake exits incur a fixed burn of some amount. The amount can be used to control the cost of exiting and re-entering, which in turn could be deployed as a mechanism to improve network stability.