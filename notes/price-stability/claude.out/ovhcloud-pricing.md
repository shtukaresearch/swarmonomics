# OVHcloud object storage — pricing history

Wayback-Machine-verified history of OVHcloud's object storage pricing from launch (2015) to May 2026. Corrects an earlier, simpler narrative that OVHcloud "never raised object storage prices" — the actual record shows one increase event in November 2022 (legacy Swift products only), one substantial cut on High Performance Object Storage in 2023, and an elimination of egress fees in late 2025.

## Timeline of products

| Date | Event |
|---|---|
| 2011 | hubiC consumer file storage launches — OVH's first OpenStack Swift deployment, the technological seed for later object storage |
| 2014 | RunAbove beta exposes Swift-based object storage to public-cloud customers |
| 2015 | Public Cloud GA, including **Public Cloud Storage (PCS)** on OpenStack Swift, plus **Cloud Archive** (cold-tier Swift) |
| 31 Dec 2019 | S3 API support added on top of the Swift backend |
| 23 Jul 2020 | Acquires **OpenIO** (Lille, FR), the S3-native engine that becomes the basis of High Performance Object Storage |
| 22 Feb 2022 | **High Performance Object Storage GA** (S3-native, OpenIO-based). Free beta until October |
| 29 Sep 2022 | **Standard Object Storage (S3 API) GA** as a separate product from legacy Swift PCS, at €7/TB/month with included internal traffic |
| 1 Nov 2022 | Public Cloud price wave (+10% on most services). Legacy Swift Object Storage and Cloud Archive included; new Standard S3 product not |
| 3 May 2023 | **Cold Archive GA** at €1.30/TB/month — tape-based (IBM 3592 + Atempo Miria), 6-month minimum, 4 French sites, 8+4 erasure coding |
| Aug-Sep 2023 | HPOS list price cut from €0.025 to €0.02/GB-mo (−20% EUR, −33% USD) |
| Jan 2024 | OVHcloud blog post welcoming Google's egress-fee removal as "a first step" — operationalizes anti-egress-fee position |
| 1 Nov 2025 – 31 Jan 2026 | Promotional first 3 TB free on Standard Object Storage in 3-AZ regions |
| Dec 2025 / Jan 2026 | **Egress fees eliminated** across all object storage classes, all regions, including transfers to other clouds |
| Feb 2026 | **Active Archive** class added — fills the gap between Infrequent Access and Cold Archive at ~$5.32/TiB/month |
| 1 Apr 2026 | Public Cloud +9–11% wave on instances/VPS/Bare Metal/Databases. **Object Storage and Block Storage explicitly excluded** |

## Current tier structure (May 2026)

Five S3-compatible classes plus legacy Swift:

1. **High Performance** (SSD, 1-AZ regions only)
2. **Standard** (1-AZ, 3-AZ, Local Zones)
3. **Infrequent Access** (30-day minimum, restore fees)
4. **Active Archive** (90-day min, instant retrieval — added Feb 2026)
5. **Cold Archive** (180-day min, tape-based)

Legacy Swift Public Cloud Storage and Cloud Archive remain accessible but documented as "older generation, no further development."

## Per-product price trajectory (EUR list, FR domain)

### Public Cloud Storage / Standard Object Storage Swift API (legacy)
- 2015-09: €0.01/GB/month, x3 replication, free ingress, €0.01/GB egress
- 2016-03 → 2022-02: held at €0.01/GB/month for **6+ years**
- 2022-10: still €0.01
- 2022-12: **€0.011/GB/month — +10%**, first-ever increase, aligned with the Nov 1 2022 Public Cloud wave
- 2023-02 onward: held at €0.011

### Cloud Archive Swift (legacy)
- 2017-01: €0.002/GB/month
- 2017-01 → 2022-10: held at €0.002 for ~5 years
- 2022-12: **€0.0024/GB/month — +20%**, larger relative bump than Standard
- Held at €0.0024 thereafter

### Standard Object Storage S3 API (new product from Sept 2022)
- 2022-09 launch: **€0.007/GB/month (€7/TB)** — 30% below the legacy Swift price. Internal traffic free.
- 2022-12 / 2023-02 / 2023-12 / 2024-06: held at €0.007/GB/month. No changes detected.

### High Performance Object Storage (new product from Feb 2022)
- 2022-02: free beta
- 2022-10 GA / 2023-07: €0.025/GB/month (€25/TB) in EUR; $0.03 in USD
- 2023-09: **€0.02/GB/month — −20% EUR, −33% USD**. Cut occurred between July and September 2023.
- 2023-11 → 2024-06: held at €0.02 / $0.02

### Cold Archive (new tape product from May 2023)
- 2023-02 (beta): €0.0013/GB/month, free during beta
- 2023-05 GA: €0.0013/GB/month (≈$0.0014 USD). Held since.
- 46% cheaper than legacy Cloud Archive Swift

### Egress
- 2015–2025: €0.01/GB outbound (~$0.011 USD), relatively stable across all classes
- Dec 2025 / Jan 2026: **eliminated entirely** across all object storage classes, including transfers to other clouds

## What kinds of price reductions has OVHcloud made?

Three distinct kinds:

1. **Direct list cut on a live product**: HPOS €0.025 → €0.02/GB/month (−20% EUR, −33% USD) in Aug-Sept 2023. This is the only true list-price reduction on a single product I verified.
2. **New product priced below the legacy it supersedes**: Standard S3 at €0.007 vs Swift PCS at €0.01–0.011 (~30–36% below). Cold Archive at €0.0013 vs Cloud Archive Swift at €0.0024 (~46% below). The legacy products weren't repriced down — they were left behind on a deprecated track. For a customer who actively migrates, this is an effective price cut; for one who doesn't, list price went up.
3. **Elimination of an ancillary fee**: egress went from €0.01/GB to zero in Dec 2025. For a typical workload this is a much larger effective price reduction than any of the storage-class changes.

## What price increases has OVHcloud made?

Two events, both in November 2022, both on legacy Swift products:

1. Swift Public Cloud Storage: €0.01 → €0.011/GB/month (+10%) — first-ever increase after 7+ years of stability.
2. Cloud Archive Swift: €0.002 → €0.0024/GB/month (+20%) — first-ever increase after ~5 years of stability.

No further increases detected on any object storage class through May 2026.

## Behavioral pattern toward customers

- **Customer who stayed on legacy Swift since 2015**: paid €0.01/GB/mo from 2015 to Oct 2022, then €0.011/GB/mo from Nov 2022 onward. One +10% bump in 11 years.
- **Customer who migrated to S3 Standard at Sep 2022 launch**: pays €0.007/GB/mo flat through May 2026. No increases.
- **Customer using HPOS since 2022 GA**: paid €0.025 then €0.02 (one ~20% cut).
- **Customer with significant egress**: paid €0.01/GB outbound until Dec 2025, then zero.

So OVHcloud's object storage isn't strictly "prices only ever go down" — but for a customer following the strategic product line (S3 API, not Swift), the effective trajectory has been flat or downward, with substantial improvements via egress elimination and HPOS cuts. The 2022 Swift increases happened on products OVHcloud was effectively winding down.

## Positioning vs hyperscalers

- OVHcloud has framed itself as the anti-lock-in, sovereignty-first alternative since the 2020 OpenIO acquisition, intensifying after the 2021 Strasbourg fire and Euronext IPO.
- The Jan 2024 "Google egress fees" blog post articulates the anti-egress position: egress fees are "artificial," part of hyperscaler lock-in, removal should be "comprehensive, automatic, universal."
- Operationalized in Dec 2025 / Jan 2026 with full egress elimination including transfers to competing clouds.
- CEO Octave Klaba has continued the line publicly through 2025–2026 (Il Sole 24 Ore, EU Commission discussions).

## Caveats

- All prices above are EUR list on the FR domain (HT, ex-VAT). USD prices on the world domain track EUR but with conversion-rate noise (e.g., the Swift PCS USD bump 2022-02 to 2023-03 was +9.8%, blending the +10% EUR list change with EUR/USD movement).
- Pre-2022 Wayback snapshots are dense for 2015–2018 but thinner for 2019–2021. The exact dates of intermediate changes (if any) within those gaps cannot be definitively ruled out, but no anomalies were detected at the snapshots checked (2019-07, 2020-03, 2021-04).
- HPOS pricing was checked in USD only for the cut event. The cut may have been timed differently in different currencies.

## Sources

Wayback Machine snapshots:
- 2015-09 Swift PCS launch pricing: https://web.archive.org/web/20150905084420/https://www.ovh.com/fr/cloud/storage/
- 2017-01 with Cloud Archive: https://web.archive.org/web/20170131072523/https://www.ovh.com/fr/public-cloud/storage/
- 2022-02 baseline: https://web.archive.org/web/20220216052739/https://www.ovhcloud.com/fr/public-cloud/prices/
- 2022-10 (post-S3 launch, pre-hike): https://web.archive.org/web/20221010035631/https://www.ovhcloud.com/fr/public-cloud/prices/
- 2022-12 (post-hike): https://web.archive.org/web/20221204144713/https://www.ovhcloud.com/fr/public-cloud/prices/
- 2023-02 (Cold Archive Beta): https://web.archive.org/web/20230208165329/https://www.ovhcloud.com/fr/public-cloud/prices/
- 2023-09 (HPOS post-cut): https://web.archive.org/web/20230926192506/https://www.ovhcloud.com/en/public-cloud/prices/
- 2024-06: https://web.archive.org/web/20240601090736/https://www.ovhcloud.com/en/public-cloud/prices/

Press / blog:
- 2022 price wave announcement: https://blog.ovhcloud.com/ovhcloud-price-adjustments-in-2022-and-2023/
- Coverage: https://www.theregister.com/2022/10/27/ovhcloud_price_energy/ , https://www.datacenterdynamics.com/en/news/ovhcloud-to-raise-prices-by-10-percent-in-2023-citing-energy-costs-and-inflation/
- 2026 price wave (object storage excluded): https://blog.ovhcloud.com/pricing-evolution-of-public-cloud-bare-metal-and-vps-at-ovhcloud/
- Egress-fee elimination: https://news.ycombinator.com/item?id=46634330
- S3 API launch: https://blog.ovhcloud.com/ovhcloud-object-storage-clusters-support-s3-api/
- HPOS launch: https://corporate.ovhcloud.com/en-gb/newsroom/news/High-Performance-Object-Storage/
- Standard Object Storage relaunch: https://corporate.ovhcloud.com/en/newsroom/news/storage-solutions-compatibilitys3/
- Cold Archive GA: https://corporate.ovhcloud.com/en/newsroom/news/cold-archive-ga/
- OpenIO acquisition: https://corporate.ovhcloud.com/en/newsroom/news/acquisition-openio-ovhclouds-ambition-create-best-object-storage-offer-market/
- Anti-egress positioning: https://blog.ovhcloud.com/egress-fees/
- Q1 FY26 update with Active Archive: https://www.ovhcloud.com/en/lp/quarterly-product-update-q1-fy26/
- Current tier structure: https://www.ovhcloud.com/en/public-cloud/object-storage/classes/
