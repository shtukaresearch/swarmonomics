# Swarm alive-node forecast: document skeleton

## Top matter

Number cards:

* Active nodes during November, with $N$-day BOTD (specify $N$).

  Headline: 80% range.

* Active nodes today, with $N$-day BOTD.

  Headline: exact count.

* Change expected:

  Headline: 80% range.

Options: length of BOTD grace period, headline range (95%, 90%, 80%, 50%)

## 1 — What we count

Definitions:

* Audited node count ($M$-day window)
* $N$-day BOTD

## 2 — The network today

* Trailing 12 months node count chart, as is
* Stats:
  * Active nodes at data head
  * Max, min
  * Neighbourhoods not audited
* Link to Swarm State of the Network blog (for previous months, October blog won't be published by the time we deliver this)

Options: number of trailing months to plot in chart, length of BOTD

## 3 — Notable events

Just bullet points for October. Mention that we know who did the 2048 batch.

## 4 — Forecast models

We only need one plausible looking model this week! So pick one of these sections that looks best.

Boxout for each model or model component:

* How it works.
* How we validate it.
* Limitations.

### 4.1 — Direct fit

Target = node count series. Do not decompose into new registrations + previously audited nodes.

### 4.2 — Component model

Forget about the aggregation artefact. Fundamentally your model is trying to predict which nodes from the population are going to pass audit on day $T+N$. You are splitting the count into:

* Nodes that have previously passed an audit.

  Modelling P(pass next audit) based on length of strings of missed audits seems like a reasonable approach. Need to pin down the actual model being used.

* Nodes that have registered but not yet passed an audit.

  Much less important than the other two summands. Leaning towards using a guesstimate hardcoded figure for how long it takes to sync based on eyeballing the data (effectively a 1-parameter model). Or use BOTD and this summand just disappears.

* Nodes that have not yet registered. 

  For some reason this is treated in a different section in your report and its unclear if the charts actually use that model.

## 5 — The forecast

* Brief description of MC simulation process.
* Chart with raw audited node count forecast and with BOTD (possibly with option to adjust grace period).
* Statistics for 30 November. Quantile ranges