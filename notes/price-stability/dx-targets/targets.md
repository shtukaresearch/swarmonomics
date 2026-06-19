# Price stability DX targets

## Context

User expectations from cloud storage:

* Prices are quoted in advance and stay constant (denominated in some major fiat currency) from month to month, or occasionally go down.
* Price rises only occur in special extenuating circumstances which are usually widely known and telegraphed several months in advance (e.g. a global supply crunch).

Assumptions about the customer:

* Customers divide the timeline into epochs and make purchase decisions based the per-epoch cost of a service.
* It is very common for the epoch to be the calendar month.
* Accurate cost estimates need to be available a little in advance of when the customer commits to the purchase in order to allow time for decision-making.
* From the perspective of user cash flow, costs are incurred as soon as cash is swapped to the settlement asset (if not the same as the cash asset).

Constraints:

* **One price.** All users are charged the same per-byte price over any given time interval. No per-user pricing.
* **No credit.** Committing to pay == paying. Users pay up front for a given commitment epoch, at or before the start of that epoch.
* **Only way to lock in exchange rate is to pay.** Regardless of which asset is used to quote prices, using any other asset for payment suffers from FX uncertainty. The only way to get price certainty when paying in a non-native asset is to swap to an amount of the settlement asset that covers the period for which you want to lock in prices.

## Objectives

### Concepts

At a high level, the first objective we are interested in is:

1. *Short-term billing certainty.* A user may obtain an exact BZZ-denominated quote for storage for the entirety of the next calendar month a few days before the start of that month.

This objective can be adjusted by choosing the number of days and, of course, the calendar month can be replaced with some other division of the timeline into epochs.

We pause to point out that this objective can be achieved if:

1. The protocol adjusts the quote price once per day;
2. The quotes are fixed in a "lookahead" at least $31+N$ days in advance.

We now fix a set of major fiat currencies (which could just be USD to start with), and choose a limit $L$ on what we consider a "small" month-on-month price increase. For example, we could choose $L$ based on typical month-on-month FX rate drift between our designated fiat currencies. Any time the month-on-month increase in *fiat-denominated* prices exceeds $L$, we say the system is in a state of *price discovery* with respect to the chosen currency. 

Our second objective is about limiting the time the system spends in price discovery.

2. *Infrequent price discovery.* The union of time intervals in which the system enters price discovery with respect to a designated currency is an "acceptable" subset of the timeline.

We are free to define "acceptable," and that is where most of the flex in this family of objectives is to be found. Broadly speaking, I can identify three types of criteria for acceptance of a set $X$ that may be useful:

* As a proportion of each year, the total size of $X$ is not too large.
* $X$ does not consist of too many distinct intervals per year.
* We can associate to each interval component of $X$ an *attribution* that clearly explains to users why price discovery occurred and why that cause was exceptional.

### Attributions

Classes of exogenous circumstance:

* Global supply or demand shock linked to price rises on major cloud providers.
* Global supply or demand shock linked to price rises on minor cloud providers.
* Major FX move in the numéraire currency.

Price discovery without associated exogenous circumstance should be treated as a Swarm-specific incident with accompanying notice from the Foundation.

### Formal definition

Define the *timeline* $\mathcal{T}$ to be a copy of $\mathbb{R}_+=[0,\infty)$ labelled by calendar times starting at some arbitrary reference time. For example, the labelling could identify $\mathbb{N}\subset\mathbb{R}_+$ with Unix timestamps (ignoring upper bounds).

Fix the following parameters:

* A family $\mathcal{E}$ of *calendars* that partition the timeline into epochs. The maximum epoch length is denoted $|\mathcal{E}|$.
* An integer $N$.
* A settlement asset $T$.
* A set of stable assets $\{S_1,\ldots,S_k\}$.
* A price jump limit $L\geq 1$.
* An *acceptance predicate* $\mathcal{A}:2^{\mathcal{T}}\rightarrow \{\bot, \top\}$ defined on subsets of the timeline.

Introduce the following family of objectives:

1. For any $E_\bullet\in\mathcal{E}$, there is an interface $\mathcal{P}$ such that for any $t\in\mathbb{N}$, the user may query $\mathcal{P}$ up to $N$ days before the start of epoch $E_t$ to obtain a price quote $\mathcal{P}(E_t)$, denominated in the settlement asset, for storage for the full duration of $E_t$. The price quote is accurate in the sense that it is certain at the time of consuming $\mathcal{P}(E_t)$ that if the user pays this price at the start of epoch $E_t$, he will receive the storage service for the entirety of $E_t$.

   (Note that this implies the value of $\mathcal{P}(E_t)$ does not depend on when it is queried, as long as it is at most $N$ days before the start of $E_t$.)

2. For each $i=1,\ldots,k$, define $\mathcal{P}_{i,t}(E_{t'})$ as obtained by converting $\mathcal{P}(E_{t'})$ to be priced in $S_i$ using the exchange rate at time $t$. 

   For any $E_\bullet \in\mathcal{E}$, define $PD(E_\bullet,S_i)\subseteq \mathcal{T}$ to be the union of $E_t$ such that $\mathcal{P}_i(E_{t+1})/\mathcal{P}_i(E_t) > L$ (queried after the price for $E_{t+1}$ becomes available). We say that $\mathcal{P}_i$ was in *price discovery* during the intervals in $PD(E_\bullet,S_i)$. Then $\mathcal{A}(PD(E_\bullet,S_i))=\top$.

## Parameters

```python
billing_epoch: Iterable[timedelta] # epoch over which users commit by paying up front
billing_lookahead: timedelta # length of time in advance of the start of an epoch from which the price for that epoch is fixed
billing_currencies: set[Currency] # set of major fiat currencies against which objectives may be measured
tolerance: float # fraction by which price may rise from one billing period to the next in ordinary circumstances
exogenous_circumstances: set[str] # set of circumstances of exogenous origin that may explain the system going into price discovery
```

## Appendix

**Theorem.** *There is no way to stabilise the price in the lookahead for customers who have not yet paid and satisfy all the constraints.*

*Proof.* Let $\tilde{P}_t$ be the price series of the settlement asset against a stable numéraire. Let $\tilde{Q}_t$ be the storage price series. The total price over epoch $I$ is $\sum_{t\in I}\tilde{P}_{s_t}\tilde{Q}_t$ where $s_t\leq t$ is the time at which the customer swaps to the settlement asset for paying the bill at time $t$. One constraint is that if a customer swaps and pays at the start $t_0$ of the epoch, that is $\sum_{t\in I} P_{t_0} \tilde{Q}_t$, he should know exactly how much to pay for the full epoch; that is $\tilde{Q}_t$ must be known for all $t\in I$ at time $t_0$. If this is satisfied for all possible epochs of length at most $|I|$, then at any time $t$, $\tilde{Q}_{t+r}$ must be known for all $r\leq |I|$.

Suppose we want to give a stabilised price estimate $\hat{Q}^t_{t'}$ for time $t'$ at time $t$, for all $t'\in I$. Here "stabilised" means that $P_t\hat{Q}^t_{t'}$ does not vary too much for $t$ close to the start of $I$. Suppose this estimate is to be available $N$ time steps in advance of $I$. If $P_t$ ends up varying a lot before the start of $I$, $\hat{Q}^t_{t'}$ needs to be updated, possibly as little as one time step in advance of $I$. But since $Q_{t+1}$ is known at time $t$ by the previous constraint, $\hat{Q}^t_{t+1}$ can only be based on a forecast of $P_{t+1}$, which we don't want to do. Q.E.D.
