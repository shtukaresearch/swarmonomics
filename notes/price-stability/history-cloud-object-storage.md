# History of cloud object storage pricing

The following history was reconstructed by trawling through blog posts, repricing announcements, and archived pricing pages from each year since cloud storage began in 2006.

## Summary

* The main fees of cloud object storage are capacity rent (priced in units of capacity-time, typically GiB-month) and egress (priced in units of capacity).
* Since AWS S3, the first object storage service, launched in 2006 the history of these prices has generally been **constant for many years** with occasional **reductions**. No service changes prices more often than once per year.
* Since 2022 there have been some **exceptional price rises**, especially among smaller or specialised providers, attributable to global supply and demand shocks and, perhaps, plateauing efficiency.
* Mostly no formal guarantees against price hikes. Services build trust through their track record.

### Communicating price hikes

Even on the rare occasions providers do have to hike prices, there are often ways to avoid communicating the price increase as a change in a `headline' GiB-month price.

Large providers with numerous services can move price increases into specialised services such as multi-region replication.

In cases where a provider is unable to do this and must post substantial price i

### Formal guarantees against price increases

As mentioned in the summary, rare. We found a couple of exceptions:

* *Reserved instances* with hyperscalers (AWS, Azure) allow large customers (at the scale of millions of USD per year) to commit to purchase a fixed amount of capacity for 1–3 years. They lock in the price at purchase time.

* *Price increase clauses* in the TOS of French providers guarantee that customers will be notified at least one month (30 days) in advance of any price hike. [Agent report](./tos-price-notice.md)

  Anecdotally, it may be common convention for price hikes to be notified at least 30 days in advance, even when there is no formal promise. For example, Hetzner's April 2026 price hike was notified to customers in early March.

## History

### Examples of market shocks

[Agent report](./claude.out/supply-chain-shocks.md)

1. 2021–2023. European energy crisis driven by post-pandemic inflation (2021) and Russo-Ukraine war (2022). Electricity prices **+70–200%**. French cloud companies (OVHCloud, Scaleway) hike prices ~10–20%.
2. 2021–2023. NAND shipping crunch. Smaller provider price hikes (Backblaze, Wasabi **+20%**).
3. 2025–present. AI driven demand shock on DRAM (**+200%**) and other memory cells. Hetzner +30%.

### Case study: OVHCloud

[Agent report](./claude.out/ovhcloud-pricing.md)

| Year | Standard (Swift) | Archive (Swift) | Standard S3 | High Performance S3 | Note                     |
| ---- | ---------------- | --------------- | ----------- | ------------------- | ------------------------ |
| 2015 | 10               |                 |             |                     | Prices are in €/TB-month |
| 2016 |                  |                 |             |                     |                          |
| 2017 |                  | 2               |             |                     |                          |
| 2018 |                  |                 |             |                     |                          |
| 2019 |                  |                 |             |                     |                          |
| 2020 |                  |                 |             |                     |                          |
| 2021 |                  |                 |             |                     | European energy crisis         |
| 2022 | 11 (**+10%**)    | 2.4 (**+20%**)  | 7           | 25                  | Elec. prices **up 70–200%**    |
| 2023 |                  |                 |             | 20 (-20%)           |                              |
| 2024 |                  |                 |             |                     |                                |
| 2025 |                  |                 |             |                     | Egress fees eliminated         |
| 2026 |                  |                 |             |                     | ~**+10%** excl. object storage |

### Case study: Storj

[Agent report](./claude.out/storj-pricing)

| Year | Tardigrade/DCS                | Archive | Regional | Global | Note                                              |
| ---- | ----------------------------- | ------- | -------- | ------ | ------------------------------------------------- |
| 2019 | 10                            |         |          |        | Prices in $/TB-month                              |
| 2020 |                               |         |          |        |                                                   |
| 2021 | 4 (-60%)                      |         |          |        | Rename: Tardigrade ⇒ DCS                          |
| 2022 |                               |         |          |        |                                                   |
| 2023 | Free tier reduced             |         |          |        |                                                   |
| 2024 | Free tier removed             |         |          |        |                                                   |
| 2025 | Grandfathered 1 year          | 6       | 10       | 15     | Acquisition by Inveniam<br />AI DRAM demand shock |
| 2026 | Migrate to Archive (**+50%**) |         |          |        | AI DRAM demand shock                              |

