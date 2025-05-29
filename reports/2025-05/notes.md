# Shtuka Research

## Swarmonomics: May report

## Overview

Work this month was carried out in the context of two work streams from the project roadmap.

* *Stake transparency.* Surface information relevant to stakers. Make it easier to enter the NO market.
* *Node strategies.* Identify and evaluate aggressive staker strategies with negative externalities.

### Operations

* *Stake transparency.* Our objectives for May were to set up data pipelines and explore methods to publish data in the form of dashboard. Andrew worked with Pavel to set node data pipelines and spin up the first alpha version of Swarm-Dash.
* *Node strategies.* Continuing on our work from the staking analysis carried out over Winter 2024/25, investigate adversarial node strategies that aim to profit by undermining consensus over the reserve (part of the r8 sampling scheme needed to establish the storage index). Aata worked with the Swarm Foundation research team and created an article on node ghettoization.

## Findings

### Ghetto neighbourhoods

[@aata writes]

### Stake dashboard

What information do stakers need to enter the market?

The most obvious questions are:

1. Where (i.e. what neighbourhood) should I put my node?
2. How much should I put down?
3. How much expected revenue do I get per unit BZZ (for given investment size and node address)?

Answering these questions carefully requires forecasting various future events, which is hard. To zeroth order, one should consider what is happening in the staking market *now*.

1. To zeroth order, a rational NO will join the neighbourhood with the lowest cost per unit revenue — that is, the one with the lowest total effective stake.[^depth] }
   The neighbourhood recommender provided by swarmscan.io returns the neighbourhood with the smallest number of nodes. It is good for the health of the storage network if nodes always join these low node count neighbourhoods. 
   We will ship this endpoint in the next version of Swarm Dash.


   To first order, there are various other considerations an NO should take into account:

   * Are there likely to be a lot of faults in the neighbourhood that could cause my node to fall out of "quorum" and be frozen, leading to lost revenue? (See discussion of ghetto neighbourhoods.)
   * Are other nodes in the neighbourhood likely to top up stake in the future? Perhaps the incumbent nodes will react to my entry by topping up their own stake share?
   * How will system revenue behave in the future? Is my node reserve nearly full, indicating a bin subdivision is imminent?
   * If the unit price of storage goes up in the future, how much will the effective stake in that neighbourhood go up? Under SWIP-20, this is bounded above by the *potential* stake variable.

2. How much should I put down? The risk-discounted future revenue streams of the target bin give a capacity to the staking opportunity. 
   Since stake is not redeemable under normal circumstances, purchasing stake should be treated as a capital expense. The investment horizon substantially governs the perceived value of the opportunity — unlike for "typical" staking products like Etheruem, NOs must decide how long they are prepared to wait for revenue to pay off the expense. Therefore, to recommend an investment amount we should ask users to input this time.

3. How much expected revenue do I get per unit BZZ?
   Given a revenue forecast $\{\tilde{R}_n\}_{n\in\mathbb{N}}$ (where $n$ is the round number), the formula is
   $$
   \mathbb{E}\left[\sum_{n\in\mathbb{N}} w(\sigma_i,\tilde\sigma_{-i,n})\cdot\tilde{R}_n \mid \sigma_i\right] / \sigma_i
   $$
   where the summation and expectation is taken with regard to a suitable discount. So given models for $\tilde{R}_n$ and $\tilde{\sigma}_{-i,n}$ given $\sigma_i$ and a discount rate, we can produce a number. 
   The zeroth order approximation is to assume $R_n$ and $\sigma_{-i}$ are constant and independent of $\sigma_i$, with the constant estimated based on recent network state. We plan to ship an expected revenue endpoint in the next version of Swarm Dash.

Deployment:

* We deployed version 0.1 of the API at https://api.dash.swarm.shtuka.io. The stake data it serves is a snapshot taken on June 1st. Frontend coming soon! Please don't DOS it!

Fun facts from the data:

* We noticed 789 nodes staked at height 102 (under SWIP-21). We're informed that this was to test a bug where doing this allowed complete withdrawal of stake.
* There seem to be more nodes topping up stake past the minimum BZZ than when we last looked in the winter. We're still not sure if this represents competitive or simply testing activity.

[^depth]: For simplicity, we assume the neighbourhood depth is known and constant.