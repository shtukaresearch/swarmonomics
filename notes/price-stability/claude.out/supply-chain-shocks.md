# Supply-chain shocks affecting cloud object storage pricing

A consolidated record of the supply-chain shock events that have affected cloud object storage providers over the last 15 years, the upstream price moves they involved, and which providers passed them through to customer pricing vs absorbed them. Drawn from the price-history research compiled in the adjacent memos on hyperscalers, independents, OVHcloud, and Storj.

## What counts as a relevant shock?

Cloud object storage providers buy commodity inputs whose prices are set in markets they don't control:
- **HDD** — bulk capacity disk, the dominant medium for object storage today (especially nearline / hyperscale-grade)
- **NAND** — for high-performance/SSD-backed tiers
- **DRAM** — for cache and metadata
- **Electricity** — running the datacenter and cooling the hardware
- **Network transit / IP transit** — for egress and inter-region
- **Datacenter construction** — labor, steel, concrete, transformers

Of these, **HDD** and **electricity** are the dominant cost drivers for object storage specifically. NAND and DRAM matter at the margins, mostly for premium tiers. The shocks below are events where one or more of these inputs moved sharply and for an extended period.

## Major shock events

### 1. 2011 Thai floods → HDD supply collapse (Oct 2011 – mid-2012)

- **Trigger**: massive flooding in Bangkok industrial estates wiped out a substantial fraction of global HDD production capacity. Western Digital and Seagate both had major facilities affected.
- **Upstream impact**: HDD wholesale prices nearly tripled. Recovery took ~12 months.
- **Coverage**: https://www.darkreading.com/application-security/hard-drive-prices-rise-due-to-thai-floods , https://www.theregister.com/2011/12/20/hp_disk_price_rises/
- **Cloud provider response — pass-through**: I could not find a documented case of any major cloud storage provider explicitly raising customer prices and attributing it to the floods. The headline story was the opposite of pass-through.
- **Cloud provider response — absorption**: **Backblaze publicly absorbed the shock** via "drive farming" — sending employees and contractors to retail stores (Costco, Best Buy, Fry's) to buy externals and shuck them rather than pay tripled wholesale prices. The company kept its $5/month unlimited backup intact through the entire shock. https://www.backblaze.com/blog/farming-hard-drives-2-years-and-1m-later/ , https://www.theregister.com/2012/10/11/backblaze_drive_farming/
- **Why this matters**: this is a clean case-study of a cloud provider visibly choosing to eat a major input-cost increase rather than pass it through. Backblaze didn't yet have B2 (object storage launched 2015) but the same posture carried over to B2.

### 2. 2021–2023 NAND/DRAM/shipping crunch (broad inflationary wave)

- **Trigger**: stacked — pandemic supply-chain disruption, container shipping cost spikes (Shanghai-LA rates ~10×), chip shortages, post-pandemic demand surge, then 2022 inflation.
- **Upstream impact**: NAND and DRAM spot prices moved sharply in both directions; HDD prices climbed steadily; datacenter construction costs rose materially.
- **Cloud provider response — clear pass-through cluster in late 2023**:
  - **Backblaze B2: $5→$6/TB-mo (+20%), Oct 2023** — first hike in 7 years. https://www.backblaze.com/blog/2023-product-announcement/
  - **Wasabi: $5.99→$6.99/TB-mo (+17%), Aug/Oct 2023** — explicitly cited "rising HDD manufacturing and data-center build/operate costs". https://docs.wasabi.com/docs/wasabi-pricing-update-june-2023
- **Cloud provider response — no public hyperscaler attribution**: AWS, Google, and Microsoft did not publicly attribute any object-storage pricing decision to NAND/HDD/shipping pressures during this period. Hyperscaler list prices for S3 Standard / GCS Standard / Blob Hot remained roughly flat. Ancillary fees moved (e.g., Google's 2022–2023 GCS ops/replication restructuring), but the public framing was "aligning prices to costs," not supply-chain pass-through.
- **Why this matters**: the late-2023 Backblaze + Wasabi cluster is the cleanest documented direct pass-through of input-cost pressure to object-storage customer pricing in this dataset. The lag (~18 months after the worst of the 2021–2022 shipping/NAND crunch) suggests these are not knee-jerk responses but absorbed inflation that finally became too expensive to keep eating.
- Added note: https://cloud.google.com/storage/pricing-announce

### 3. 2022 European energy crisis (Sep 2021 – Q4 2022)

- **Trigger**: Russia-Ukraine war disrupting Russian gas supply to Europe; French nuclear fleet maintenance outages reducing baseload; resulting electricity spot price spikes across the EU.
- **Upstream impact**: French electricity wholesale prices roughly tripled at peak. Scaleway publicly disclosed an **85% YoY rise in its electricity costs from Q3 2021 to Q3 2022**.
- **Cloud provider response — direct pass-through at French/European providers**:
  - **Scaleway: +10% across-the-board, 1 Dec 2022.** Explicitly attributed to soaring gas prices, French nuclear maintenance, and the 85% YoY rise in electricity costs. https://www.scaleway.com/en/news/changes-to-scaleways-pricing/ — cleanest energy-crisis pass-through in the dataset.
  - **OVHcloud: +10% wave, Nov 2022 / Dec 2022.** Energy + inflation attribution. Public Cloud, Bare Metal, Hosted Private Cloud, Web Hosting, Dedicated, Eco, VPS, Web Hosting. Object Storage was included for the legacy Swift products (Swift PCS +10%, Cloud Archive Swift +20%); the new S3 Standard product launched two months earlier was held flat. https://blog.ovhcloud.com/ovhcloud-price-adjustments-in-2022-and-2023/
- **Cloud provider response — no analogous US wave**: the same energy spike did not produce announced US-provider price moves on object storage. US electricity prices rose but less dramatically, and most US hyperscaler datacenters are on long-term PPAs (often renewables) that smooth short-term wholesale-price moves.
- **Why this matters**: this is the clearest case of geographically-specific cost shocks producing geographically-specific pricing responses. European providers passed through; US providers didn't.

### 4. 2022–2023 US chip export controls on China (BIS rule, Oct 2022; expansion Oct 2023)

- **Trigger**: US Bureau of Industry and Security export controls restricting advanced compute chip and equipment exports to China; significantly expanded in October 2023.
- **Upstream impact**: Chinese cloud providers lost direct access to NVIDIA H100 / A100 and successors; restrictions on lithography equipment (ASML EUV) affecting domestic fabrication.
- **Cloud provider response — counterintuitive direction in China**: rather than raising prices, **Chinese hyperscalers cut prices in 2023 and 2024** to defend market share and to monetize their constrained AI compute via cloud rental rather than equipment sale.
  - Alibaba "up to 50%" cuts, 26 April 2023 — OSS included. https://www.theregister.com/2023/04/26/chinas_alibaba_cloud_to_cut/
  - Tencent up to 40% on core products, 16 May 2023. https://technode.com/2023/05/17/tencent-cloud-cuts-prices-by-up-to-40-to-compete-with-alibaba/
  - China Mobile Cloud, JD Cloud followed within weeks.
  - April 2024 "Spring Thunder" international cut (Alibaba average 23%, up to 59%) — OSS-Resource 1-year reservation 500 GB went US$63 → US$16.99.
- **Cloud provider response — no documented OSS-class hike** from any major Chinese provider through May 2026 directly attributable to chip controls.
- **Why this matters**: shows that a major supply-side restriction can produce price *cuts* rather than rises, when the strategic response is to monetize captured-on-side capacity (cloud-renting scarce AI compute) rather than to pass through input shortages.

### 5. 2025–2026 NAND / HDD / DRAM / electricity squeeze (AI-demand-driven)

This is the active, ongoing shock as of May 2026, and it is the largest in the dataset.

- **Trigger**: AI infrastructure buildout consuming HBM, DRAM, NAND, and HDD capacity faster than fabs and disk makers can supply. Compounded by hyperscaler capex commitments locking up multi-year output from Samsung, SK Hynix, Micron, Western Digital, Seagate.
- **Upstream impact (per Caixin, Tom's Hardware, TrendForce, TechPowerUp)**:
  - **DDR4 prices ~+1,800%** in 2025 (Caixin)
  - **DDR5 prices ~+500%** in 2025
  - **NAND spot prices >+100% in H2 2025**; SanDisk reportedly doubling enterprise 3D NAND contract prices in Q1 2026
  - **Nearline HDD contract prices +4% Q4 2025** (largest rise in 8 quarters); WD raised HDD prices 5–10% in April 2024 already
  - TrendForce expects tightness through 2027
  - Coverage: https://www.tomshardware.com/pc-components/storage/perfect-storm-of-demand-and-supply-driving-up-storage-costs , https://www.techpowerup.com/344108/hdd-prices-soar-sparking-fears-of-incoming-shortage , https://www.tomshardware.com/pc-components/ssds/sandisk-to-double-price-of-3d-nand-for-enterprise-ssds-in-q1-2026-hyperscalers-to-pay-top-dollar-for-storage-as-ai-continues-to-roll
- **Cloud provider response — pass-through wave underway**:
  - **Hetzner: +30–50% in places, effective 1 Apr 2026.** Cited energy, hardware, memory/CPU bottlenecks, AI-boom demand. https://www.hetzner.com/pressroom/statement-price-adjustment/
  - **Alibaba, Baidu, Tencent: Mar–Apr 2026** — first broad upward move from Chinese hyperscalers. **Alibaba +5–34% on AI compute, +30% on CPFS parallel file storage; Baidu +5–30%, ~30% on file storage; Tencent ~5%.** Caixin attribution: 2025 memory spikes directly. https://www.caixinglobal.com/2026-03-19/alibaba-tencent-hike-cloud-prices-as-ai-boom-drives-up-hardware-costs-102424744.html
  - **Storj: 1 Nov 2025 tier restructuring** (effective price increase for most workloads, +50–275%). Storj didn't explicitly attribute the change to supply-side pressures, but the timing coincides with the Inveniam acquisition (22 Oct 2025) and the broader storage-input squeeze.
  - **Vultr Object Storage: ~3× hike March 2025** via Standard tier relaunch.
  - **IDrive e2: +65–148% Sept 2024.**
- **Cloud provider response — explicit exclusions of object storage**:
  - **Alibaba/Baidu/Tencent March 2026**: the hikes target AI compute and **parallel/file storage**, NOT standard object storage (OSS/COS/OBS/BOS). Object storage was not named in the Caixin or Register coverage.
  - **OVHcloud April 2026 wave**: +9–11% on instances/VPS/Bare Metal/Databases, but **Object Storage and Block Storage explicitly excluded**. https://blog.ovhcloud.com/pricing-evolution-of-public-cloud-bare-metal-and-vps-at-ovhcloud/
- **Cloud provider response — no AWS/Azure/GCP S3-class hike yet**: through May 2026 none of the three Western hyperscalers has announced a list-price increase on their headline hot object storage tier (S3 Standard, Blob Hot, GCS Standard) directly attributing it to the 2025–26 shock. Ancillary fees and tier mechanics continue to evolve (e.g., Azure's 128 KiB minimum-billable size for cool tiers, effective 2026/2027), but the headline $/GB-month rates remain stable.
- **Why this matters**: this is the live test of whether the 2017-onward pattern of frozen-headline-prices-on-object-storage can hold under sustained supply pressure. So far the answer is mixed:
  - Adjacent products (parallel/file storage, AI compute, instances) are being raised openly and aggressively.
  - Headline object storage rates at major providers are being deliberately protected.
  - Smaller / value-tier providers (Vultr, IDrive) are doing the unprotected pass-through that hyperscalers and OVHcloud are avoiding.

## Patterns across all five shocks

### Who passes through, who absorbs

| Provider class | 2011 Thai floods | 2021–23 NAND/shipping | 2022 EU energy | 2022–23 BIS controls | 2025–26 AI squeeze |
|---|---|---|---|---|---|
| US hyperscalers | absorbed (no public response) | absorbed on headline; ancillary moves | absorbed | n/a | absorbed on headline so far |
| Backblaze | **absorbed (drive farming)** | passed through (+20%) | n/a (US) | n/a | n/a so far |
| Wasabi | n/a (founded 2017) | passed through (+17%) | n/a (US) | n/a | n/a so far |
| Cloudflare R2 | n/a | n/a (launched 2022) | n/a | n/a | absorbed so far |
| OVHcloud | n/a | partial pass-through (Nov 2022 wave hit Swift legacy products) | passed through | n/a | object storage explicitly excluded from 2026 wave |
| Scaleway | n/a | n/a | passed through (+10%) | n/a | (not yet announced) |
| Hetzner | n/a | n/a | n/a | n/a | passed through (+30–50%) |
| Chinese hyperscalers | n/a | n/a | n/a | **cut prices** (counterintuitive) | passed through on AI compute / parallel storage, NOT object storage |
| Decentralized (Storj) | n/a | held legacy $4/$7 throughout | n/a | n/a | tier restructuring (effective increase) |
| Smaller value providers (Vultr, IDrive) | n/a | partial pass-through | n/a | n/a | sharp pass-through |

### Three observations

**1. Object storage list price is the most sticky line item.** Across all five shocks, the headline per-GB-month rate on standard hot object storage has been more protected than any other major cloud SKU. Providers raise compute, raise file/parallel storage, raise ancillary fees, raise legacy/archive tiers, eliminate or compress free tiers — but the headline number on the marketing page is treated as a strategic anchor.

**2. Smaller and value-tier providers pass through first.** The pattern across multiple shocks: smaller providers (Backblaze, Wasabi, Vultr, IDrive, Hetzner) raise prices roughly when the underlying input pressure becomes too expensive to keep absorbing. Hyperscalers and infrastructure-strategic providers (OVHcloud) hold the line longer, presumably because (a) they have deeper margins to absorb against, (b) they have long-term PPAs and supply contracts smoothing input volatility, and (c) the headline price is a more important strategic anchor for their land-and-expand sales model.

**3. Supply-side stress can produce price cuts when the strategic response is capacity-monetization rather than cost-recovery.** The 2022–23 Chinese price wars under BIS export controls are the canonical example: providers blocked from selling captured AI compute as hardware monetized it as cloud-rental at aggressively cut prices. The 2025–26 Chinese wave is the partial reversal — once memory/HDD pressure hit, the AI compute that was being cut became expensive to keep cutting, so the strategy flipped to pass-through on AI compute (while still protecting object storage). The strategic context matters as much as the absolute input cost.

## What's open

- **Will any US/EU hyperscaler raise S3 Standard / Blob Hot / GCS Standard list prices on object storage during the 2025–26 squeeze?** As of May 2026 no announcement. The ~9-year-flat pattern on S3 Standard since the Dec 2016 cut is now under genuine pressure.
- **Will the 2025–26 wave produce a second Backblaze/Wasabi-style cluster of independent-provider hikes?** Vultr and IDrive have already moved. Backblaze and Wasabi have not announced follow-ups to their Oct 2023 increases. If the squeeze persists into 2027 per TrendForce projections, another cluster looks likely.
- **Will Storj's Inveniam-era pricing settle, or is the Nov 2025 restructuring the first of multiple changes?** No signal yet.

## Sources

Industry coverage of 2025–26 supply situation:
- https://www.tomshardware.com/pc-components/storage/perfect-storm-of-demand-and-supply-driving-up-storage-costs
- https://www.techpowerup.com/344108/hdd-prices-soar-sparking-fears-of-incoming-shortage
- https://www.tomshardware.com/pc-components/ssds/sandisk-to-double-price-of-3d-nand-for-enterprise-ssds-in-q1-2026-hyperscalers-to-pay-top-dollar-for-storage-as-ai-continues-to-roll
- https://www.caixinglobal.com/2026-03-19/alibaba-tencent-hike-cloud-prices-as-ai-boom-drives-up-hardware-costs-102424744.html
- https://www.datacenterdynamics.com/en/news/chinese-cloud-providers-hike-up-prices-for-cloud-and-ai-services/

2011 Thai floods:
- https://www.backblaze.com/blog/farming-hard-drives-2-years-and-1m-later/
- https://www.theregister.com/2012/10/11/backblaze_drive_farming/
- https://www.darkreading.com/application-security/hard-drive-prices-rise-due-to-thai-floods

2021–23 cluster:
- https://www.backblaze.com/blog/2023-product-announcement/
- https://docs.wasabi.com/docs/wasabi-pricing-update-june-2023
- https://knowledgebase.wasabi.com/hc/en-us/articles/15566987584795-Wasabi-Pricing-Update-June-2023

2022 EU energy:
- https://www.scaleway.com/en/news/changes-to-scaleways-pricing/
- https://blog.ovhcloud.com/ovhcloud-price-adjustments-in-2022-and-2023/
- https://www.theregister.com/2022/10/27/ovhcloud_price_energy/

2022–23 BIS / China cuts:
- https://www.theregister.com/2023/04/26/chinas_alibaba_cloud_to_cut/
- https://technode.com/2023/05/17/tencent-cloud-cuts-prices-by-up-to-40-to-compete-with-alibaba/
- https://www.theregister.com/2024/04/08/alibaba_intl_price_cut/
- https://cset.georgetown.edu/article/bis-2023-update-explainer/

2025–26 wave:
- https://www.hetzner.com/pressroom/statement-price-adjustment/
- https://www.theregister.com/2026/03/18/alibaba_cloud_hikes_prices_by/
- https://blog.ovhcloud.com/pricing-evolution-of-public-cloud-bare-metal-and-vps-at-ovhcloud/
- https://blogs.vultr.com/object-storage-relaunch
- https://forum.rclone.org/t/idrive-e2-raising-prices-24/47910
- https://www.trendforce.com/news/2026/04/10/news-ai-compute-prices-rise-across-china-tencent-joins-alibaba-baidu-in-hikes-zhipu-raises-prices-again/
