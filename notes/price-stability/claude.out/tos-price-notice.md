# Cloud storage TOS: price-change notice and termination rights

Survey of the price-modification clauses in the customer agreements of major and notable cloud object-storage providers, plus the legal background behind the unusual termination rights at French providers.

## Comparison table

| Provider | Notice period | Customer termination right tied to price change | Contractual price-lock |
|---|---|---|---|
| AWS | 30 days (Customer Agreement §3.1) | No — only general termination-for-convenience | No |
| Google Cloud / GCS | None — at-will (GCP TOS §2.6, "at any time") | Termination-for-convenience only | No (the 30-day Workspace/Looker carve-out does *not* apply to GCP) |
| Microsoft Azure (consumption) | "Upon notice" — no minimum stated | No | EA / RIs only |
| Cloudflare R2 | 30 days (Self-Serve Subscription Agreement §4.2) | Non-renewal only | No |
| Backblaze B2 | "Commercially reasonable" — no fixed days | No | No |
| DigitalOcean Spaces | None stated | No | No |
| Scaleway | 1 month (General TOS Art. 7) | **Yes — explicit, no penalty** | No |
| OVHcloud | 30 days (4 months for consumers) (General TOS §11.2) | **Yes — explicit, no penalty** | **Yes — services in a Commitment Period are not subject to mid-term increases** |
| Hetzner | "Prior notification" — no minimum (T&Cs §1.3) | No | No |
| IBM Cloud | 30 days (Cloud Services Agreement Z126-6304) | No | Yes — for committed term |
| Oracle Cloud | n/a on-term | No | Yes — for ordered Services Period |
| Wasabi | 60 days, plus right to prepay up to 12 months at the existing rate | No | Effective via prepay |

Sources: AWS Customer Agreement (https://aws.amazon.com/agreement/); GCP TOS (https://cloud.google.com/terms/); Azure MCA / Online Services Terms (https://azure.microsoft.com/en-us/support/legal/subscription-agreement); Cloudflare Self-Serve Subscription Agreement (https://www.cloudflare.com/terms/); Backblaze ToS (https://www.backblaze.com/company/policy/terms-of-service); DigitalOcean ToS (https://www.digitalocean.com/legal/terms-of-service-agreement); Scaleway General TOS v.17/07/24 (https://www-uploads.scaleway.com/General_Terms_of_Services_v17072024_45d4879c08.pdf); OVHcloud General TOS v10.0 (https://storage.gra.cloud.ovh.net/v1/AUTH_325716a587c64897acbef9a4a4726e38/contracts/cf2d578-contrat_genServices-GB-10.0.pdf); Hetzner T&Cs (https://www.hetzner.com/legal/terms-and-conditions/); IBM Cloud Services Agreement Z126-6304 (https://assets.applytosupply.digitalmarketplace.service.gov.uk/g-cloud-14/documents/700064/927449436764831-terms-and-conditions-2024-05-01-1353.pdf); Oracle CSA (https://www.oracle.com/contracts/docs/cloud_csa_us_en_2351289.pdf); Wasabi Product Terms (https://wasabi.com/product-terms).

## Distinctions worth flagging

- **Material-adverse-change vs. price-change.** Several agreements (AWS §1.6, Cloudflare §14) reserve a longer / more protective notice for SLA or material changes — not specifically price. Don't conflate.
- **Termination-for-convenience as a sham recourse.** AWS, Cloudflare, Backblaze, GCP and Azure boil down to "we'll tell you, your only out is to leave." Real protection only kicks in if leaving is cheap.
- **Lock comes through commitment, not through the TOS.** With the partial exception of Wasabi (12-month prepay) and OVH (Commitment Period), price stability requires a separately negotiated term commitment.
- **GCP's GCS has no notice period.** The 30-day clause in Google's TOS applies only to Workspace, Looker (original), and Cloud Identity. GCS is explicitly outside it.

## The French termination right — what it actually means

Both Scaleway and OVHcloud bake a no-penalty termination right into their general TOS. This looks unusual to anyone used to AWS-style "you can stop using a usage-billed service whenever, no clause needed." The right is specifically a Franco-European legal artefact.

**What the clauses actually cover.**

OVH's clause is the more precise of the two, and it answers the question directly. The TOS distinguishes:

1. **Services *without* a Commitment Period** (i.e., pay-as-you-go object storage, on-demand instances, etc.). OVH may raise prices, but only after 30 days' email notice (4 months for consumers). During that notice window the customer may cancel the affected services without penalty.
2. **Services *with* a Commitment Period** (e.g., 12-month bare metal contracts, pre-paid VPS, committed object-storage capacity). OVH **cannot** raise the price mid-commitment at all — this is the price-lock entry in the table above. So no termination right is needed: the price simply can't change.

OVH's clause also carries an explicit carve-out for "unpredictable circumstances making the execution excessively expensive for OVHcloud, which had not agreed to assume the risk" — this is a direct reference to the *théorie de l'imprévision* (see below). The carve-out lets OVH invoke imprévision to revise prices even during a commitment, but not without going through the legal mechanism.

Scaleway's clause is broader — "Services under subscription," with no Commitment-Period carve-out — but the substantive structure is the same: 1 month notice, customer may cancel within the notice window, otherwise deemed to have accepted the new price.

**Why the clause exists at all when you can "just stop using" a usage-billed service.**

For a pure metered service with zero stickiness, the formal termination right is largely redundant. It still does work for a few non-trivial reasons:

- **Notice protection.** Even on PAYG, the price change doesn't take effect for 30 days. That is enforceable as a contractual obligation, distinct from any unilateral provider behavior.
- **Cleanup and data egress.** "Stopping use" of object storage is not instantaneous — you have to migrate data out. The notice window plus right-to-cancel guarantees the operational time to do so under the old price.
- **Pre-paid balances, vouchers, and credits.** Most providers maintain customer balances. The clause sets the terms under which those are handled when the customer leaves over a price change.
- **Sub-services with implicit lock-in.** Domain renewals, IP reservations, license SKUs, SSL certificates and similar items often have minimum durations even on otherwise-PAYG accounts.
- **Legal certainty.** It removes any argument that the customer's continued use during the notice window constitutes acceptance of the new price.

**Why it is a French/European thing.**

Three legal layers stack here:

1. **French Civil Code Art. 1195** (introduced by the 2016 ordonnance reforming contract law) — the *théorie de l'imprévision*. If unforeseen circumstances make performance excessively onerous, the disadvantaged party may demand renegotiation, and failing that, judicial revision or termination. This is *the* legal mechanism French providers use when invoking cost shocks. OVH's "unpredictable circumstances" carve-out is a direct nod to it.
2. **French civil-law principle that essential contract terms cannot be unilaterally modified.** Price is canonically essential. Permitting one party to change it requires giving the other an exit — otherwise the modification clause itself can be struck down as a *clause abusive* (unfair term).
3. **EU consumer law.** The Unfair Contract Terms Directive 93/13/EEC (transposed into the French Code de la consommation) requires that consumers be given clear notice and a termination right when essential terms change. The longer 4-month notice for consumers in OVH's clause is the consumer-law-driven version. For B2B customers, Article L. 442-1 of the Code de commerce (formerly L. 442-6) prohibits significantly imbalanced obligations — a unilateral price-change clause without an exit is a textbook example.

US-headquartered providers draft TOS against US contract law, where the doctrine is much more permissive: a clear notice provision plus the customer's general termination right is generally enough. So AWS, Cloudflare, and Backblaze ToSes don't carry the explicit no-penalty termination wording. They could — and competitive pressure plus EU operations may eventually push them — but it isn't legally required of them in their home jurisdiction.

**Bottom line for the user's question.** It's a French thing, yes. The right matters most for services *with* some lock-in element; for pure PAYG it is largely formal but does pin down notice timing, cleanup, and balances. OVH's clause is the cleanest example because it explicitly distinguishes Commitment Period (price-locked, no exit needed) from non-Commitment (price changeable, 30-day exit). Scaleway has a similar structure without the same explicit Commitment-Period carve-out in the price-modification article.
