# DMIT Los Angeles VPS: How to Choose Between CN2 GIA, CMIN2 and Tier 1 Plans, and What Each One Actually Costs

Searching "DMIT Los Angeles VPS" usually lands you somewhere confusing. DMIT's LAX pricing page lists three different network profiles, several hardware generations that share nearly identical product names, and a handful of plans that keep disappearing and reappearing based on whether the racks are full.

So the real question isn't "is DMIT good." It's which of these plans you should buy — and the honest answer depends on which Chinese carrier your visitors or your own connection uses, and how much of that traffic you expect to burn through each month.

This is a breakdown of what's actually on the LAX line, what it costs, and where the fine print will bite you.

## The three network profiles, in plain terms

Every Los Angeles plan carries one of three labels. They are not hardware tiers — they're routing profiles, and that's what you're paying for.

**Premium (Pro)** is the CN2 GIA product. China Telecom outbound runs on AS4809, China Unicom goes out directly via AS4837, China Mobile outbound routes through Hong Kong Mobile (AS58453), and all three return paths use AS4809. This is the profile people are usually hunting for when they search DMIT at all.

**Eyeball (EB)** sits one step down on cost and adds traffic. Telecom routes split between AS9929 and AS58807, Unicom mainly uses AS9929, Mobile runs CMIN2. In practice EB gives you more monthly transfer for the same money, and the differences versus Pro show up mostly at peak hours on telecom.

**Tier 1 (T1)** is straight international BGP with no mainland optimization. If your users are in Europe, Southeast Asia or North America, this is the sensible pick — and the cheapest one.

| Profile | Return routing to mainland China | Best fit |
| --- | --- | --- |
| Premium (Pro) | CN2 GIA (AS4809) on all three carriers | Sites and apps where mainland latency matters |
| Eyeball (EB) | CMIN2 + AS9929 | Mobile/Unicom-heavy audiences, higher traffic needs |
| Tier 1 (T1) | International BGP, no China optimization | Overseas projects, backups, downloads, transit |

## What "AS3" means, and why plan names look repeated

DMIT builds its LAX product names from the hardware generation plus the routing profile. You'll see `LAX.AS3`, `LAX.AN4` and `LAX.AN5` in the same price list, and the spec sheets on third-party sites often mix them up.

- **AS3** uses AMD EPYC 7003-series CPUs. It's the value generation and the one most of the current LAX lineup belongs to.
- **AN4** also used EPYC 7003 hardware and has largely been retired for LAX.
- **AN5** runs AMD EPYC 9005 and costs noticeably more. The AN5 Pro entry plan is priced around $12.98/month against $10.90 for the AS3 equivalent.

That price gap is the whole story. If a spec table shows a DMIT Los Angeles plan at $29.90/month and another shows a similar one at $34.90/month, you're probably looking at two different generations, not a price change.

Two things worth knowing before you plan around availability:

DMIT paused sales across all products for a stretch while it worked through LAX rack space, power and storage cluster capacity. Subsequent restocks have been described as the newest hardware going up in one batch, with the next restock timing unknown. Some regions come back before others — in at least one recent round, Pro and T1 returned while Eyeball stayed out of stock.

DMIT also states that LAX AS3 is still in an ongoing optimization phase, and that disk performance and SLA may be lower than on a mature platform. That's the vendor saying it, not a competitor. If you're deploying something that matters, test first.

## LAX.AS3 Premium (CN2 GIA) plans and pricing

This is the lineup most readers of this page are after. All plans include free setup, 1 IPv4 plus an IPv6 /64, standard DDoS protection, and KVM virtualization. Traffic is counted bidirectionally — outbound and inbound both eat into your monthly allowance.

| Plan | vCPU | RAM | SSD | Monthly transfer | Port | Throttled to | Price |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Pro.TINY | 1 | 2GB | 20GB | 1000GB | 1Gbps | 4Mbps | $10.90/mo |
| Pro.Pocket | 2 | 2GB | 40GB | 1500GB | 4Gbps | 4Mbps | $16.90/mo |
| Pro.STARTER | 2 | 2GB | 80GB | 3000GB | 10Gbps | 4Mbps | $34.90/mo |
| Pro.MINI | 4 | 4GB | 80GB | 5000GB | 10Gbps | 8Mbps | $62.90/mo |
| Pro.MICRO | 4 | 4GB | 160GB | 7000GB | 10Gbps | 8Mbps | $87.90/mo |
| Pro.MEDIUM | 6 | 8GB | 160GB | 14000GB | 10Gbps | 10Mbps | $199.90/mo |

👉 [Check current LAX Premium availability and order](https://www.dmit.io/aff.php?aff=12046&pid=253)

Notice the upgrade curve. Going from TINY to Pocket buys you a second core, double the disk and 1500GB more transfer for $6. TINY to STARTER triples the traffic and pushes the port to 10Gbps for $24 more. Above STARTER the increments get expensive fast, because you're buying CPU and RAM rather than network.

The overage behaviour matters more than the port speed for most buyers. Hit your transfer cap on Premium and the connection is throttled rather than cut off — 4Mbps on the two cheapest plans, 8Mbps from MINI up. At 4Mbps a small site or a monitoring panel keeps running; a video-heavy site does not.

## LAX.AS3 Eyeball (CMIN2) plans and pricing

Eyeball gives you more transfer for the same monthly figure as Premium at every tier. What you give up is the uniform CN2 GIA return path.

| Plan | vCPU | RAM | SSD | Monthly transfer | Port | Throttled to | Price |
| --- | --- | --- | --- | --- | --- | --- | --- |
| EB.TINY | 1 | 2GB | 20GB | 1500GB | 2Gbps | 4Mbps | $10.90/mo |
| EB.Pocket | 2 | 2GB | 40GB | 3000GB | 4Gbps | 4Mbps | $16.90/mo |
| EB.STARTER | 2 | 2GB | 80GB | 5000GB | 10Gbps | 4Mbps | $34.90/mo |
| EB.MINI | 4 | 4GB | 80GB | 10000GB | 10Gbps | 8Mbps | $62.90/mo |
| EB.MICRO | 4 | 4GB | 160GB | 14000GB | 10Gbps | 8Mbps | $87.90/mo |
| EB.MEDIUM | 6 | 8GB | 160GB | 30000GB | 10Gbps | 10Mbps | $199.90/mo |

👉 [See the current Eyeball plan list and pricing](https://www.dmit.io/aff.php?aff=12046)

The catch: Eyeball has been the hardest LAX line to get. It was left out of at least one restock round entirely while Pro and T1 went back on sale, and multiple deal sites were still listing it as out of stock after that. If EB is the plan you want, the practical move is to check stock before you build a deployment timeline around it.

If you're mainly on Unicom or Mobile, EB at the same price as Pro with 50% more transfer is usually the better deal. If your audience is telecom-heavy and evening latency is the thing you're optimising for, pay the Premium premium.

## LAX.AS3 Tier 1 (international) plans and pricing

Tier 1 is where DMIT's LAX pricing gets genuinely cheap — and where the overage policy is most generous.

| Plan | vCPU | RAM | SSD | Monthly transfer | Port | Throttled to | Price |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T1.WEE | 1 | 1GB | 20GB | 1000GB | 4Gbps | 100Mbps | $36.90/yr |
| T1.TINY | 1 | 1GB | 20GB | 2000GB | 4Gbps | 200Mbps | $6.90/mo |
| T1.STARTER | 2 | 2GB | 40GB | 4000GB | 10Gbps | 200Mbps | $12.90/mo |
| T1.MINI | 2 | 4GB | 80GB | 8000GB | 10Gbps | 200Mbps | $21.90/mo |
| T1.MICRO | 4 | 4GB | 120GB | 16000GB | 10Gbps | 500Mbps | $32.90/mo |

👉 [Review the Tier 1 plans and current stock](https://www.dmit.io/aff.php?aff=12046)

WEE is the cheapest way into a DMIT Los Angeles box by a wide margin, and $36.90 a year for 4Gbps port speed is hard to argue with if you don't need China routing. Run out of the 1000GB and you drop to 100Mbps rather than getting suspended, which is a genuinely usable fallback for backups and mirrors.

What Tier 1 does not give you is the free IP replacement conditions that Pro and EB customers get. Don't assume the policies carry across profiles.

## Picking one, based on what you're actually doing

**Personal blog or small site with mainland readers.** Pro.TINY at $10.90/month. 2GB of RAM and 1000GB of bidirectional traffic covers a WordPress install comfortably; the CN2 GIA return path is the reason you're paying.

**Mobile or Unicom audience, more traffic.** EB.TINY or EB.Pocket. You get 1500–3000GB instead of 1000–1500GB for the same money.

**Overseas users, backups, CI runners, download mirrors.** T1.STARTER or T1.MINI. $12.90–$21.90 a month for 4–8TB of transfer and a 10Gbps port is a different category of value, and the relatively high throttled floor means an overage isn't an outage.

**Anything that needs to survive an overage without noticing.** Tier 1, for the 100–500Mbps throttle. Premium and Eyeball drop to single-digit Mbps.

**Production business workload.** Pro.MINI or above. Not because of the network, but because 4 cores and 4GB is the first configuration here that won't choke on a database under load.

## Billing cycles, discounts and promo codes

DMIT changes promotional structure often enough that copying a coupon code from a blog post is a gamble. A few things are worth knowing anyway.

Billing cycles affect the effective monthly rate. WEE exists only as an annual plan — there's no monthly option at $36.90/year. Annual billing on higher tiers is generally cheaper per month than monthly billing, and DMIT has previously run automatic annual discounts on select plans without requiring a code at all.

The most widely circulated code for the LAX Eyeball line is `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF`, which is described as a recurring 20% discount on Eyeball plans at quarterly billing or longer. "Recurring" means it applies on renewals, not just the first invoice, which is a meaningfully better deal than a one-time discount. Validate it at checkout — the promo box has a validate function, and codes do expire.

DMIT has also run seasonal promotions (Christmas campaigns, for example) structured as a percentage discount plus a credit-back component paid into your account balance in monthly instalments over a year. Those come and go; check what's live before you assume a code from an older post still works.

One payment detail that matters more than it sounds: refunds via Alipay are reported to carry no gateway fee, while other channels may deduct one. If you're ordering to test routes and might refund, that changes which button you click.

## The fine print people skip

**The three-day refund window.** DMIT's policy allows a full refund within three days provided you've used under 30GB of traffic, and a refund of remaining value within one month, minus payment gateway fees. That 30GB condition is the part that catches people — a speed test marathon can blow through it.

**Free IP replacement.** If your IPv4 gets blocked, Pro and EB customers can request a replacement roughly every 15 days. Other cases carry a $5 charge. Pro and EB also have self-service IP changing in the control panel, which covers promotional plans too, not just full-price ones.

**Bidirectional traffic counting.** Your 1000GB on Pro.TINY is inbound plus outbound, not each. Serving files, running a proxy, or syncing backups all count twice against the allowance. Tier 1's more generous throttle cushion softens this; Premium's 4Mbps doesn't.

**Stock is not stable.** DMIT sells out. Plans vanish from the order page and come back weeks later. Nothing on any third-party spec sheet is a guarantee that the plan is purchasable right now — the checkout page is the only source of truth.

**Test before you commit.** DMIT runs a public Looking Glass with separate endpoints for the LAX Pro and LAX EB networks. A trace route and a peak-hour download from your own carrier tells you more than any review, including this one.

## Common questions

**Is DMIT Los Angeles the same as DMIT LAX?** Yes. LAX is the airport code for Los Angeles and DMIT uses it as the location prefix in every plan name.

**What's the difference between LAX.AS3 and LAX.AN5?** Hardware generation and price. AS3 is AMD EPYC 7003, AN5 is EPYC 9005, and AN5 plans start higher — roughly $12.98/month for the Pro entry plan versus $10.90 on AS3.

**Can I get CN2 GIA cheaper?** Only through the Promotional or Eyeball lines, and EB is CMIN2 rather than CN2 GIA. Full CN2 GIA on all three carriers means Premium pricing. If budget is the constraint, EB or Tier 1 is where the value is.

**Do I need CN2 GIA at all if my users aren't in China?** No. Tier 1's international routing is the correct and much cheaper answer, and its overage throttle is 25–50× more forgiving.

**How fast does DMIT Los Angeles stock sell out?** Fast enough that restock announcements tend to circulate with "order sooner rather than later" attached. There's no reliable pattern to the timing.

## What to do next

The short version: figure out which carrier your audience uses and how much bidirectional traffic you'll actually move, then pick the profile — not the biggest plan you can afford. Premium for telecom-heavy mainland audiences, Eyeball for Unicom and Mobile with higher transfer needs, Tier 1 for everything that isn't China-facing.

Then check what's actually in stock, run a Looking Glass trace from your own network, and use Alipay if there's any chance you'll want the refund path. DMIT's LAX line is well-regarded for routing quality, but it's a vendor that sells out and doesn't discount predictably, so going in with a clear requirement beats going in with a coupon you found on a blog.

👉 [See every live LAX plan and current pricing](https://www.dmit.io/aff.php?aff=12046)
