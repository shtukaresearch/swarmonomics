# Storj object storage — pricing history

Wayback-Machine-verified history of Storj's object storage pricing from launch (Nov 2019, branded Tardigrade) to May 2026. Note: this is pricing for the *service* (USD per TB-month and per TB egress, with credit-card or STORJ-token settlement). It is *not* the STORJ token's market price, which moves independently and is irrelevant to what customers pay.

## Background

- Storj operates a decentralized object-storage network: Storj Labs (the company) sells service to customers; **Storage Node Operators (SNOs)** supply disk and bandwidth and are paid per GB-month stored and per GB egressed.
- Customer prices are denominated in USD. The STORJ token is used purely as an optional payment rail — deposits are credited as USD balance at spot at deposit time, with a flat +10% bonus on deposits ≥$10. So the customer's headline $/TB rate doesn't move with token price.
- Customer pricing and SNO payouts are decoupled — Storj Labs sets both administratively; this is not a market. (Contrast Filecoin and Sia, which have real bid/ask markets.)

## Timeline of products

| Date | Event |
|---|---|
| **2018–2019** | Storj V3 network development |
| **19 Nov 2019** | **Tardigrade pricing announced** alongside Pioneer 2 beta release |
| **19 Mar 2020** | **Tardigrade GA** (commercial production launch) |
| **20 Apr 2021** | **Rebrand to Storj DCS** (Decentralized Cloud Storage), with major price cut |
| **3 Apr 2023** | Free tier reduced from 150 GB to **25 GB** storage + egress (new accounts) |
| **2023** | **Storj Select** enterprise SKU launched (curated SOC2-certified node groups; sales-quoted) |
| **1 Dec 2023** | SNO payout rates cut (supply side, not customer-facing) |
| **Feb 2024** | **Free tier discontinued**; 31 Mar 2024 deadline to convert to Pro |
| **2024–25** | **Object Mount** launched (file-system-style mount over object storage, separate SKU) |
| **22 Oct 2025** | **Acquisition**: Inveniam Capital Partners signs definitive agreement to acquire Storj Labs |
| **1 Nov 2025** | **Tiered pricing restructuring** — replaces single $4/$7 plan with three tiers (Global Collaboration, Active Archive, Object Mount Production Cloud Regional). Existing accounts grandfathered as "Legacy Global" for one year. Comes 9 days after the Inveniam acquisition |

## Per-product price trajectory (Wayback-verified)

### Tardigrade (Nov 2019 – Apr 2021)
- **Storage**: $10/TB-month ($0.01/GB)
- **Download bandwidth (egress)**: $45/TB ($0.045/GB)
- **Upload bandwidth**: free
- **Pricing rationale (from launch blog)**: "Storage is half the price of centralized cloud providers (we are $10 per terabyte versus their $22 per terabyte) and bandwidth (we are $45 per terabyte versus their $99 per terabyte)."
- Bulk discounts available
- https://web.archive.org/web/20200808161339/https://tardigrade.io/blog/post/business/announcing-pioneer-2-and-tardigrade-io-pricing-1/

### Storj DCS (Apr 2021 – Nov 2025) — the "$4/$7 era"
- **Storage**: $4/TB-month — a **60% cut** from Tardigrade's $10
- **Bandwidth**: $7/TB — an **~84% cut** from Tardigrade's $45
- **Segment fee**: $0.0000088 per segment-month (introduced with this pricing)
- **Free tier (Apr 2021 – Apr 2023)**: 150 GB storage + 150 GB bandwidth across 3 projects (50 GB/project per month)
- Marketing claim at launch: "80% Less" than incumbents
- $5/month minimum (waived for STORJ-token-paying accounts)
- Verified at multiple snapshots — held for 4.5 years:
  - 2021-04: https://web.archive.org/web/20210424041154/https://www.storj.io/pricing
  - 2023-02: https://web.archive.org/web/20230208223126/https://www.storj.io/pricing
  - 2025-01: https://web.archive.org/web/20250108153145/https://www.storj.io/pricing

### Free tier reductions (Apr 2023 → Feb 2024)
- **3 Apr 2023**: free tier cut from 150 GB → **25 GB storage + 25 GB egress** for new accounts. Existing accounts grandfathered, though some were unintentionally downgraded. Pro pricing held at $4/$7.
- https://web.archive.org/web/20230406062712/https://www.storj.io/pricing
- **Feb 2024**: free tier discontinued entirely. Existing free-tier users had until 31 March 2024 to convert to Pro accounts.

### November 2025 tier restructuring (the big event)

The single $4/$7 plan was replaced by three customer-facing tiers, effective 1 Nov 2025. Existing customers grandfathered as "Legacy Global" pricing for one year.

**Acquisition context.** Nine days before the restructuring took effect, on 22 Oct 2025, Inveniam Capital Partners (a private-markets data infrastructure firm) signed a definitive agreement to acquire Storj Labs. Storj remains a legal entity as an Inveniam subsidiary, with existing customer, supplier, and SNO relationships preserved. Storj's own announcement framed the deal as positioning Storj to "accelerate innovation"; coverage from Blocks & Files and Channel Insider framed it as a strategic infrastructure play around decentralized AI/data. The temporal coincidence with the tier restructuring is suggestive — large customer-pricing changes are commonly synchronized with M&A events because new owners want to reset commercial expectations from day one — but Storj's own communications attribute the pricing change to its product strategy rather than the acquisition. So: correlation is clear, causal attribution is not made public.

**As confirmed by the 2025-10 snapshot before the change (https://web.archive.org/web/20251025082803/https://www.storj.io/pricing):**

| Tier | Storage | Egress | Notes |
|---|---|---|---|
| **Global Collaboration** | $15/TB-mo | Included (1× storage-equivalent; $0.02/GB over) | Globally distributed, consistently fast |
| **Regional Workflows** | $10/TB-mo | Included (1× storage-equivalent; $0.01/GB over) | US first, EU/other regions coming; confirmed in storj.dev/dcs/pricing/tiered though not surfaced on the public storj.io/pricing marketing page |
| **Active Archive** | $6/TB-mo | $0.02/GB ($20/TB) | Strategically distributed, 30-day min retention |
| **Object Mount Production Cloud Regional** | $40/TB-mo paid annually | No egress or API fees | US-only at launch; 10 user licenses included, $75/license additional; 20 TB minimum footprint |
| **Legacy Global** (pre-Nov-2025 accounts) | $0.004/GB-mo ($4/TB) | $0.007/GB ($7/TB) | + $0.0000088/segment-month; preserved for one year |

After the one-year grandfather period (~Nov 2026), un-migrated Legacy Global accounts **default to Active Archive** — not to the closer functional analog (Global Collaboration). This means a passive customer who does nothing experiences both a price change ($4→$6/TB storage, $7→$20/TB egress) and a service-tier downgrade (30-day retention floor, slower retrieval, larger min billable object size). Confirmed in the Storj community forum by Storj staff (Jacob): *"If they don't choose a different tier by November 1st, 2026 they will be migrated to Active archive."* Notably, the official storj.dev/dcs/pricing/legacy and storj.dev/dcs/pricing/tiered docs state only that the grandfather period is one year — they do not state the default destination. https://forum.storj.io/t/update-to-storj-object-storage-pricing-what-node-operators-need-to-know/30725

### Effective price impact for customers

The Nov 2025 change is in net effect an **increase for most workloads**:
- Storage at the new entry tier (Global Collaboration) is **$15/TB vs $4/TB legacy** — 3.75× higher.
- The lowest tier (Active Archive) at $6/TB is still 50% higher than the legacy $4/TB, with paid egress.
- Only customers whose monthly egress meaningfully exceeds stored volume (>1×) benefit — they now get free egress up to 1× storage on the two top tiers.
- Forum community modelling: 60–244% price increase for cold/low-egress users, 94–155% for high-egress users.
- https://forum.storj.io/t/new-pricing-model-up-or-downgrade/30729

## Storage Node Operator (SNO) payouts — supply side

These don't affect customer prices but are the supply-side compensation that determines whether nodes will stay on the network.

| Date | Storage | Egress | Repair/Audit egress |
|---|---|---|---|
| Pre-Dec 2020 | $1.50/TB-mo | $20/TB | $10/TB |
| ~2021 – Nov 2023 | $1.50/TB-mo | **$6/TB** (cut) | $6/TB |
| **1 Dec 2023** | $1.50/TB-mo | **$2/TB** | **$2/TB** |
| Nov 2025 onward | Unchanged ($1.50 / $2 / $2) |

- December 2023 cut: egress and repair payouts reduced by ~2/3, with Storj stating total SNO income fell ~12% because egress was only ~18% of total payouts.
- The November 2025 customer-pricing change explicitly **does not change SNO rates**.
- However, "expansion factors" (the redundancy multiplier for erasure-coded data placement) are increasing for the Global tier, so nodes will fill more storage faster (more GB-months billable per unit of customer data stored).
- https://forum.storj.io/t/announcement-changes-to-node-payout-rates-as-of-december-1st-2023-closed/24125
- https://forum.storj.io/t/update-to-storj-object-storage-pricing-what-node-operators-need-to-know/30725

## STORJ-token vs credit-card pricing

- Service prices are **denominated in USD** on the customer side. The token is a payment rail, not a unit of pricing.
- Deposits in STORJ tokens are credited as USD balance at the spot price **at deposit time** — so the customer carries token-price risk only between deposit and billing burn-down, not on the headline $/TB rate.
- **+10% bonus** on STORJ-token deposits of $10 or more — auto-upgrades the account to Pro.
- Token-paying accounts are **exempt from the $5/month minimum**; credit-card-only accounts pay it.
- The 10% bonus and minimum-waiver have survived all customer-pricing changes including the Nov 2025 restructuring.

## What kinds of price changes has Storj made?

**Direct list-price reductions:** one major event — the Apr 2021 Tardigrade → DCS rebrand cut storage by 60% and egress by 84%.

**Direct list-price increases:** one major event — the Nov 2025 tier restructuring. Although framed as a tier addition, for the bulk of customer workloads the effective minimum price went from $4/TB storage + $7/TB egress to $6/TB storage + $0.02/GB egress (Active Archive) or $15/TB storage with included egress (Global Collaboration). Either path is a meaningful increase for low-egress workloads.

**New SKUs above the legacy price**: Storj Select (2023, sales-quoted), Object Mount (Production Cloud Regional at $40/TB/mo annual) — these sit at significantly higher price points than the legacy DCS service, though they target different use cases.

**Free-tier compression**: 150 GB free → 25 GB free (Apr 2023) → no free tier (Feb 2024). Each step removed value, though list-price-per-GB for paying customers didn't change at these moments.

**SNO payout cuts**: Dec 2023 (~2/3 cut on egress/repair). Doesn't affect customer prices but is the supply-side trajectory.

## Comparison to OVHcloud's pattern

| Dimension | Storj | OVHcloud |
|---|---|---|
| Years between launch and first list-price increase | ~6 years (2019 → 2025) | ~7 years (2015 → 2022) |
| Magnitude of first increase | ~50–275% (workload-dependent) | +10% (Swift Standard), +20% (Cloud Archive) |
| Reductions on live products | $10→$4 storage, $45→$7 egress (2021 rebrand) | HPOS €0.025→€0.02 (2023); egress eliminated (2025) |
| Grandfathering on increases | Yes, 1 year | Implicit — legacy products still listed at old price |
| Free-tier evolution | 150 GB → 25 GB → 0 | n/a |
| Multi-currency pricing | USD only | EUR + USD list books |

Both providers held legacy prices flat for 5–7 years before raising, but Storj's 2025 increase is substantially larger in magnitude than OVHcloud's 2022 wave.

## Caveats

- **Documentation gap on the default-migration destination**: the most consequential detail of the Nov 2025 transition — that un-migrated Legacy Global accounts default to Active Archive — appears only in a forum reply from Storj staff, not in the canonical storj.dev pricing docs. The docs confirm the one-year grandfather period but stop short of stating the default destination. A passive customer reading only the official docs would not learn this until billing changes.
- **Regional Workflows tier is real but under-marketed**: the public storj.io/pricing marketing page emphasizes Global Collaboration, Active Archive, and Object Mount, but the storj.dev/dcs/pricing/tiered developer docs confirm a fourth tier — Regional Workflows at $10/TB-mo storage with 1× storage-equivalent included egress and $0.01/GB over. US-first, other regions stated as coming. So the tier system is effectively four-way for new accounts, not three-way.
- The segment-fee read in the 2025-01 snapshot ("$0.008 per 10k segments") may or may not be a redenomination of the historical $0.0000088 per segment-month — context unclear, flagging as needs verification.
- Storj Select and Object Mount have multiple sub-SKUs (named-user vs footprint-based, annual vs monthly) with different prices; only the canonical entry points are captured here.

## Sources

Wayback Machine snapshots (primary evidence):
- 2020 Tardigrade pricing blog: https://web.archive.org/web/20200808161339/https://tardigrade.io/blog/post/business/announcing-pioneer-2-and-tardigrade-io-pricing-1/
- 2021-04 Storj DCS rebrand: https://web.archive.org/web/20210424041154/https://www.storj.io/pricing
- 2023-02 (150 GB free, $4/$7 stable): https://web.archive.org/web/20230208223126/https://www.storj.io/pricing
- 2023-04 (free tier cut to 25 GB): https://web.archive.org/web/20230406062712/https://www.storj.io/pricing
- 2024-02 (free tier still 25 GB, soon discontinued): https://web.archive.org/web/20240201191248/https://www.storj.io/pricing
- 2025-01 ($4/$7 + redenominated segment fee): https://web.archive.org/web/20250108153145/https://www.storj.io/pricing
- 2025-10 (pre-restructure, new tiers visible): https://web.archive.org/web/20251025082803/https://www.storj.io/pricing
- 2025-11 (post-restructure): https://web.archive.org/web/20251111081523/https://www.storj.io/pricing
- 2025-12: https://web.archive.org/web/20251206085941/https://www.storj.io/pricing

Forum threads:
- Free Tier reduction (Apr 2023): https://forum.storj.io/t/storj-free-tier-update-for-new-accounts-25-gb-storage/22155
- Free Tier discontinuation (Feb 2024): https://forum.storj.io/t/discontinuation-of-the-storj-free-tier/25332
- SNO payout change (Dec 2023): https://forum.storj.io/t/announcement-changes-to-node-payout-rates-as-of-december-1st-2023-closed/24125
- Nov 2025 pricing for node operators: https://forum.storj.io/t/update-to-storj-object-storage-pricing-what-node-operators-need-to-know/30725
- Community impact analysis: https://forum.storj.io/t/new-pricing-model-up-or-downgrade/30729

Press / announcements:
- Tardigrade launch (Nov 2019): https://www.prnewswire.com/news-releases/storj-labs-announces-pricing-for-tardigrade-cloud-storage-service-beta-2-release--delivering-resiliency-and-affordability-for-users-in-the-cloud-300960667.html
- Tardigrade GA (Mar 2020): https://www.coindesk.com/tech/2020/03/19/storjs-decentralized-cloud-storage-service-tardigrade-goes-live
- Storj DCS rebrand (Apr 2021): https://www.businesswire.com/news/home/20210420005963/en/Storj-Launches-Storj-DCS-The-Developers-Gateway-to-the-Decentralized-Internet
- StorageNewsletter coverage of original $10/TB pricing: https://www.storagenewsletter.com/2019/11/26/storj-labs-pricing-for-tardigrade-cloud-storage-service-at-10-for-1tb-month-and-45-tb-of-bandwidth/
- Inveniam acquisition announcement (Oct 2025): https://www.prnewswire.com/news-releases/inveniam-acquires-storj-to-power-the-future-of-decentralized-data-infrastructure-302590751.html
- Storj's own framing of the acquisition: https://www.storj.io/blog/storj-joins-inveniam-to-accelerate-innovation
- CoinDesk coverage: https://www.coindesk.com/business/2025/10/22/inveniam-capital-partners-acquires-storj-to-advance-decentralized-data-infrastructure
- Blocks & Files coverage: https://blocksandfiles.com/2025/10/23/web-3-storage-supplier-storj-sold-to-inveniam/
- Tokenholder implications (forum): https://forum.storj.io/t/what-storj-s-acquisition-means-for-storj-tokenholders/31010

Docs:
- Current pricing: https://www.storj.io/pricing
- Legacy pricing reference: https://storj.dev/dcs/pricing/legacy
- Tiered pricing reference: https://storj.dev/dcs/pricing/tiered
- Object Mount pricing: https://storj.dev/dcs/pricing/object-mount
- STORJ token payment: https://storj.dev/support/account-management-billing/payment-methods/how-can-I-use-the-storj-token-to-pay
