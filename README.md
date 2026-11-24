# VPS with Free Backup: What "Free" Actually Includes, How Long It's Kept, and Which Plans Bundle It (Full Plan Table)

Free backup on a VPS is one of four things, and which one you get matters more than the CPU count: a manual snapshot you have to remember to take, a scheduled daily image stored in the same data centre as your server, a copy stored outside that data centre, or a paid add-on that the marketing page lists as a feature. Evoxt sits in the third group. Every VM it sells includes an automatic weekly off-site backup at no extra cost, starting with the VM-0.5 at $2.99/month.

Three questions separate the four grades, and none of them are answered on most "free backup" comparison pages: how many days of backups are kept, where the copies physically sit, and whether restoring takes the server offline. The answers change the value of a $6 plan more than 2 GB of extra RAM does.

## Quick answer: the plan most people should pick

> **VM-1, $5.99/month.** 1 vCPU up to 6.0 GHz, 2 GB RAM, 20 GB disk, 500 GB monthly transfer, weekly off-site backup included. Enough for a small site, a staging box, a VPN endpoint, or one Docker stack.
>
> Skip VM-0.5 (512 MB) unless you know why you need it. 512 MB will not run a control panel, and 5 GB of disk fills quickly. If you're putting MySQL or Postgres on the box, start at VM-2 ($11.99, 2 cores / 4 GB).

Evoxt prices all plans in USD and bills monthly out to three years, with no hourly option. Card, PayPal, Bitcoin and USDt Tron are accepted, so a prepaid term doesn't require a credit card.

👉 [See every Evoxt plan and the current monthly price](https://bit.ly/EvoXt)

## Evoxt's full plan lineup, with backup inclusion per tier

Evoxt's pricing page currently lists eleven plans on a single line. The CPU clock speed is the same on all of them (up to 6.0 GHz), and so is the backup column.

| Plan | vCPU / RAM / Disk | Monthly transfer | Backup | Price (USD/mo) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB / 5 GB | 250 GB | Weekly off-site | $2.99 | [ Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB / 10 GB | 250 GB | Weekly off-site | $4.99 | [ Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB / 20 GB | 500 GB | Weekly off-site | $5.99 | [ Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB / 20 GB | 500 GB | Weekly off-site | $6.95 | [ Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB / 30 GB | 1,000 GB | Weekly off-site | $11.99 | [ Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB / 30 GB | 1,000 GB | Weekly off-site | $14.99 | [ Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB / 60 GB | 2,000 GB | Weekly off-site | $23.99 | [ Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB / 60 GB | 2,000 GB | Weekly off-site | $29.99 | [ Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB / 80 GB | 3,000 GB | Weekly off-site | $47.99 | [ Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB / 80 GB | 3,000 GB | Weekly off-site | $60.95 | [ Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB / 100 GB | 5,000 GB | Weekly off-site | $95.99 | [ Deploy VM-16](https://bit.ly/EvoXt) |

Two things the table doesn't show. Transfer past the monthly allowance is throttled rather than billed, so a busy month costs you speed, not overage. And individual resources can be added to an existing VM without switching plans, which is cheaper than jumping a whole tier when you only need another gigabyte of RAM.

The odd plan is VM-1.5. For 96 cents more than VM-1 you get a second core at the same RAM and disk, which is unusual at this price point and worth taking if you run anything multi-threaded.

## The four grades of "free backup"

**Free manual snapshots.** Snapshots cost nothing extra on VPS.org and capture a full compressed copy of the disk while the server keeps running. A snapshot only exists if you remember to take one, which makes it a tool for the ten minutes before an upgrade, not a data-protection policy. The same provider states that snapshots and backups sit on the same storage cluster in the same New Jersey location and are not encrypted: useful against a deleted file or a bad upgrade, useless if the location itself is lost.

**Scheduled daily backups in the same building.** OVHcloud includes a daily backup with every VPS, kept on a rolling 7-day basis, excluding additional disks. The image is exported and replicated three times inside the same data centre; a copy on separate storage requires the paid Premium automatic backup or external backup option. VPS.org sells the same idea as an add-on: daily backups add 30% to the monthly price and weekly backups add 20%, so daily protection on a $10 plan costs $3.00 a month. Retention there is 7 days for daily and 28 days for weekly, identical on every plan.

**A copy stored outside the data centre.** This is the grade that survives a lost facility, and it is what Evoxt includes at zero cost on all eleven plans. PomeloHost also bundles a free weekly off-site backup plus snapshots, with daily backups optional, but its site currently says "We're opening soon" and collects a waitlist. You cannot buy a PomeloHost VPS today, so the free off-site copy there is a promise rather than a product.

**Paid add-ons.** Contabo's Auto Backup keeps 10 days of incremental backups on off-server storage across nine regions and is a separate line item on the invoice. It works, and it isn't free, and restoration overwrites the current disk while the VPS is unavailable until the process completes.

## What Evoxt's free backup covers, and what it doesn't

The backup is described on Evoxt's own site as automatic, weekly, off-site, and included on every VM at zero cost, with self-service restore from the control panel whenever needed. That combination puts the $2.99 plan ahead of most sub-$5 offerings on data protection alone, since the usual pattern in this bracket is a free snapshot and a paid schedule.

Retention is the gap. Evoxt doesn't publish how many weekly copies it keeps on the pricing page, and a backup you can't date is hard to plan around. Ask support for the retention window before you treat the free backup as evidence for anything with a compliance requirement.

The second gap is arithmetic. A weekly backup means worst-case data loss of up to seven days. If the box takes orders, holds customer records, or runs a database, seven days is not a recovery plan. Pair the included backup with an application-level dump on a schedule you control: `pg_dump` or `mysqldump` for the database, then `restic` or `borgbackup` to push it to storage outside Evoxt. That way the free weekly image handles the "the server won't boot" case and your own dump handles the "restore Tuesday's data" case.

Evoxt's panel also lists VM cloning, a firewall, monitoring charts and an admin REST API. Cloning a machine before a risky change gives you a rollback point that doesn't touch the weekly schedule.

👉 [Start with VM-1 and check the backup terms on the order page](https://bit.ly/EvoXt)

## How Evoxt compares with three providers that also bundle backups

| Provider | Verified price | What that buys | Backup terms |
| --- | --- | --- | --- |
| Evoxt | $2.99–$95.99/month, USD | VM-1: 1 core up to 6.0 GHz, 2 GB, 20 GB, 500 GB transfer | Weekly off-site backup included on all plans, no extra cost |
| OVHcloud | VPS-3 from £9.01/month ex. VAT (£10.81 incl. VAT) | 6 vCores, 12 GB RAM, 100 GB NVMe, unlimited traffic, 2 Gbps | Daily automatic backup included, rolling 7 days, replicated three times in the same data centre; external copy is paid |
| Contabo | CLOUD VPS 4 €5.50/month for the first 24 months | 4 vCPU, 8 GB RAM, 100 GB SSD, 200 Mbit/s, unlimited traffic, €0 setup | Auto Backup is a paid add-on: 10 days of incremental backups on off-server storage; VPS offline during restore |
| Rabisu | x4 promotional price from $6.10/month | 2 cores, 4 GB RAM, 40 GB NVMe | Daily backup included, 2 restore points, and the provider states it "does not guarantee full data recovery" |

Two footnotes on that table. Rabisu's own page contradicts itself: the same plan appears at $6.10, $7.63 and $9.99 in different blocks, and uptime is claimed as 99%, 99.95% and 99.99% in three places, so treat $6.10 as a promotional slot rather than a stable price. Contabo's €5.50 is expressly a first-24-months rate.

On pure price per gigabyte of RAM, Contabo wins and it isn't close. What you pay for that is a backup you have to buy separately and a much slower port on the entry tier. OVHcloud's daily backup is the strongest free schedule of the four, but it never leaves the building.

## Pick by what you're protecting

**You only need to survive a bad `apt upgrade` or a deleted directory.** A free snapshot or a clone is enough, and Evoxt's weekly image is a bonus. Cheapest Evoxt plan that fits the workload, no add-ons.

**You run a database, a shop, or anything with customer records.** Off-site matters more than frequency. Evoxt's weekly copy plus your own nightly dump covers both the lost-server and the bad-migration case, and it costs nothing beyond the VPS.

**You need point-in-time recovery.** No provider in this comparison offers it. VPS.org says so outright and points customers at binary logs or WAL archiving, which is the honest answer for everyone at this price.

**Your workload is single-core bound.** Game servers, PHP and Node apps, and small databases care about clock speed more than core count, and Evoxt advertises up to 6.0 GHz per core across the lineup. VM-1.5 at $6.95 with two cores is the value pick there.

**DDoS mitigation is non-negotiable.** VPSBenchmarks' feature table for Evoxt marks DDoS protection as not included. If always-on mitigation is a requirement, confirm it with Evoxt before ordering rather than assuming.

**You're budget-driven and comparing first-year prices.** Check the renewal column. PomeloHost's $6.49 intro becomes $11.99 after the two-year term, and Contabo's €5.50 is a 24-month rate. Evoxt lists one monthly price per plan with no intro-versus-renewal split.

## FAQ

**How long does Evoxt keep the free weekly backup?**
Not published on the pricing page. Ask support before relying on it for anything regulatory, and keep your own copy of data you can't recreate.

**Can I download a backup from the panel?**
Evoxt doesn't document an export path. Assume you may need to pull data out yourself with rsync or restic if you want a copy you control.

**Will restoring take the server offline?**
Providers that document this all say yes. VPS.org notes restores usually take several minutes and longer for large disks; Contabo says the VPS is unavailable until recovery finishes. Plan a quiet window.

**Snapshot or backup?**
A snapshot is taken by hand, usually right before a change. A backup runs on a schedule and expires on a retention timer. You want the scheduled one for disasters and the snapshot for maintenance.

**Does a free backup protect against losing the whole data centre?**
Only if the copy sits elsewhere. Evoxt's weekly backup is off-site; OVHcloud's included daily backup is replicated inside the same facility and needs a paid upgrade to leave it.

## Before you order

Match the term to the job: monthly if you're testing, a longer prepay only if you've already run a workload on the box for a few weeks. Then send support two questions, retention window and restore procedure, because neither is spelled out on the pricing page and both decide whether the free backup is enough on its own.

If you want the cheapest VM here that still ships with an off-site backup, VM-0.5 at $2.99 covers it. For almost everyone else, VM-1 at $5.99 has enough RAM to run a real site with room for the occasional spike.

👉 [Deploy an Evoxt VM with the weekly off-site backup included](https://bit.ly/EvoXt)
