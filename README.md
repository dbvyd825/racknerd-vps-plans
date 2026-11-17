# RackNerd Linux VPS: Which Plan Fits Your Workload, What Renewal Really Costs, and What "Unmanaged" Means in Practice

RackNerd's Linux VPS specials currently start at **$21.99/year for 1 GB RAM** and **$35.99/year for 2 GB RAM**, both with a 1 Gbps port and full root access. For most people reading this, the $35.99/year 2 GB plan is the one to buy: it clears the 2 GB floor that nearly every one-click app in RackNerd's ctrl panel asks for, and it doubles your RAM for $14 more per year than the entry plan.

Below: every plan on the current specials page with exact specs and yearly prices, whether the promo price survives renewal, how to pick a plan from the app you actually want to run, what "unmanaged KVM" obligates you to do yourself, and the setup steps that trip people up.

## Quick verdict before you read the rest

> Buy the **$35.99/year 2 GB plan** for a single self-hosted app, a small Docker stack, or a VPN and panel combo. Buy the **$21.99/year 1 GB plan** only if you know you need one lightweight service. Buy the **$59.99/year 4 GB plan** if you plan to run Ollama, AnythingLLM, LibreChat, or n8n with Postgres. The 8 GB plan is for OpenClaw and almost nothing else on this list.
>
> 👉 [See the current RackNerd VPS specials and pick a datacenter](https://bit.ly/RacKnerd)

## All five RackNerd Linux VPS plans, side by side

These are the five plans on RackNerd's VPS Specials page. Every one includes KVM virtualization, RAID-10 SSD storage, full root access, one IPv4 address, a 1 Gbps network port, the ctrl control panel, and a choice of datacenter at checkout. Nothing is tier-gated except the hardware itself.

| Plan | Specs | Price and billing | Who it suits | Order |
| --- | --- | --- | --- | --- |
| **1 GB** | 1 vCPU · 20 GB SSD · 1 GB RAM · 3 TB/mo | $21.99/year (≈ $1.83/mo) | A single small container, WireGuard, a lightweight panel | [Get the 1 GB plan](https://bit.ly/RacKnerd) |
| **2 GB** | 2 vCPU · 35 GB SSD · 2 GB RAM · 5 TB/mo | $35.99/year (≈ $3.00/mo) | One self-hosted app, small Docker stack, n8n or Coolify | [Get the 2 GB plan](https://bit.ly/RacKnerd) |
| **4 GB** | 3 vCPU · 60 GB SSD · 4 GB RAM · 7 TB/mo | $59.99/year (≈ $5.00/mo) | Ollama, AnythingLLM, LibreChat, Hermes Agent, production n8n | [Get the 4 GB plan](https://bit.ly/RacKnerd) |
| **6 GB** | 6 vCPU · 100 GB SSD · 6 GB RAM · 12 TB/mo | $89.99/year | Several services plus a database on one box | [Get the 6 GB plan](https://bit.ly/RacKnerd) |
| **8 GB** | 7 vCPU · 150 GB SSD · 8 GB RAM · 20 TB/mo | $119.99/year (≈ $10.00/mo) | OpenClaw, or a genuinely heavy multi-app host | [Get the 8 GB plan](https://bit.ly/RacKnerd) |

The jump from 1 GB to 2 GB costs $14/year and doubles RAM and vCPU. The jump from 2 GB to 4 GB costs $24/year. Above 4 GB, the price curve gets steeper relative to what most single-app deployments need: 6 GB to 8 GB is $30/year for 2 GB of RAM, and at that point you are paying for 20 TB of transfer you probably will not use.

## The promo price is the renewal price, and that changes the math

Most budget VPS offers are first-term discounts, and the second invoice is the one that stings. RackNerd states the opposite for these specials, in writing: "These RackNerd VPS specials are lifetime recurring. You can renew at the same rate for as long as you decide to keep the service."

So a 2 GB plan is $35.99 in year one, $35.99 in year three, and $35.99 in year five. Three years of that plan costs $107.97 total. Run the entry plan for the same period and you pay $65.97.

This matters because it removes the usual "cheap now, expensive later" trap from your decision. You can compare plans on what they actually cost, not on what the first invoice says. It also means there is no reason to buy a bigger plan than you need as insurance against a future price hike.

Billing cycles are monthly, quarterly, semi-annual, or annual, chosen at checkout. Payment methods are PayPal, credit card, cryptocurrency, and wire transfer. Note that RackNerd's knowledgebase states plainly that there is no money-back guarantee and no refunds under the terms of service, so the annual price is a commitment rather than a trial. If you want to test the network before committing a year, the honest approach is to start with the smallest plan you can use and treat the annual prepay as a decision you have already validated.

👉 [Check the plan list and current yearly pricing](https://bit.ly/RacKnerd)

## Pick the plan from the app you want to run

RackNerd publishes minimum requirements for the apps in its ctrl one-click catalog. These numbers are the most useful plan-selection tool available, because they are specific and they split the lineup cleanly.

**1 GB is enough for:** WireGuard with the wg-easy web UI (1 vCPU / 1 GB), Webmin (1 vCPU / 1 GB), CyberPanel (1 vCPU / 1 GB). These are single-purpose services with small footprints.

**2 GB is the floor for:** Portainer (1 vCPU / 2 GB), CloudPanel (1 vCPU / 2 GB), AdminBolt (2 vCPU / 2 GB, installed on AlmaLinux 9 with a 30-day app trial), n8n (2 vCPU / 2 GB), Coolify (2 vCPU / 2 GB). RackNerd recommends 4 GB for n8n and Coolify once you add Postgres and a reverse proxy, which is realistic: a database plus a proxy plus the app itself will crowd 2 GB.

**4 GB is the floor for:** Hermes Agent, AnythingLLM, Ollama with Open WebUI, and LibreChat. All four are listed at 2 vCPU / 4 GB minimum. Ollama in particular will want more RAM and disk for larger models, so 4 GB is a starting point rather than a comfortable ceiling.

**8 GB is required for:** OpenClaw, listed at 4 vCPU / 8 GB. That is the only app in the catalog that forces the $119.99/year plan. If you are not running OpenClaw, the 8 GB plan is hard to justify for a single workload.

Anything not in the catalog installs over SSH. Docker and Docker Compose work on every plan because you have full root, and Portainer is available as a one-click install if you want a GUI.

## What "unmanaged" actually costs you

RackNerd calls these unmanaged KVM VPS. In practice that means RackNerd handles the platform and you handle everything inside the VM. Support is available 24/7 for platform issues, and RackNerd's blog cites an average response time under 10 minutes.

The ctrl panel covers the day-to-day operational work so you are not locked out of basic recovery:

- power on, off, and reboot
- OS reinstall from the template list
- HTML5 VNC console for out-of-band access
- root password reset
- bandwidth and resource monitoring
- inbound firewall rules via the ctrl Network Firewall
- one-click app installs
- plan upgrades

What ctrl does not do is administer your server. Patching, hardening SSH, configuring services, managing backups, debugging a broken application: all yours. If you have never run a Linux server, budget an evening for the first setup. If you have, this is the same workflow as any other KVM box.

Two operational details worth knowing before you click install:

**One-click installs wipe the disk.** RackNerd states that a one-click install permanently erases existing data on the VPS, including the OS, apps, and files. The install takes roughly 15 to 45 minutes, and credentials appear in the panel when it finishes. Do not run a one-click install on a server that already has data you want.

**Custom ISOs go through a ticket.** If your OS is not in the template list, open a support ticket with a download link and RackNerd will mount it so you can install through the HTML5 console. You cannot upload an ISO yourself.

👉 [Start with the 2 GB plan if you want one app and room to grow](https://bit.ly/RacKnerd)

## Datacenters, operating systems, and what happens after you pay

Datacenter choice happens at checkout. RackNerd lists Los Angeles, San Jose, Seattle, Dallas, Atlanta, Chicago, New York, Ashburn, Amsterdam, France, and Dublin. Pick the one closest to your users; a VPN endpoint should sit near the people connecting to it, and a self-hosted app should sit near you.

OS templates include CentOS, Rocky Linux, AlmaLinux, Fedora, Debian, and Ubuntu. Ubuntu is offered in 20.04, 22.04, 24.04, and 26.04. RackNerd notes that Ubuntu 20.04's standard support ended in May 2025 and that extended security maintenance requires Ubuntu Pro, so use a newer LTS for anything new.

Provisioning is automatic after payment. RackNerd's blog gives the range as most deployments completing within 5 to 15 minutes; the product page says the server comes online in minutes. Either way, you are not waiting on a human.

You will get two emails: an order confirmation and a separate "KVM VPS Login Information" message containing the IP address, SSH root credentials, the ctrl panel URL, and the ctrl username and password. The ctrl login is separate from your RackNerd client area login, which catches people out. If you lose the ctrl credentials, they are in the client area under the email log for that service.

From the client area, Services > VPS Hosting gives you the service, and ctrl lives at ctrl.racknerd.com. If you have a time-sensitive request, open a support ticket after ordering rather than putting it in the order notes.

## Who should not buy one of these

Skip RackNerd's VPS specials if any of these describe you:

**You want managed hosting.** Nobody will configure your app, tune your database, or fix your broken WordPress. You are buying a server, not a service.

**You need a GPU.** These are CPU-only KVM instances. Running local models means CPU inference on 4 GB of RAM, which is fine for small models and slow for anything substantial.

**You need Windows.** The specials are Linux. Windows options exist on other RackNerd product lines, not on this page.

**You need more than 8 GB of RAM on one machine.** The specials top out at the 8 GB plan. Past that, a dedicated server is the correct product, and the per-GB economics change completely.

**You need a refund window.** There is no money-back guarantee. If you are not ready to commit a year to a $21.99 or $35.99 purchase, wait until you are.

## How to decide in one pass

Match your workload to the list below and stop there:

- One VPN, one lightweight panel, or one tiny container → **$21.99/year 1 GB**
- One self-hosted app, Portainer plus a few containers, n8n or Coolify without heavy extras → **$35.99/year 2 GB**
- Ollama, AnythingLLM, LibreChat, Hermes Agent, or n8n with Postgres and a reverse proxy → **$59.99/year 4 GB**
- Several services plus a database on a single box, or you want headroom you will actually use → **$89.99/year 6 GB**
- OpenClaw → **$119.99/year 8 GB**, since nothing smaller meets its 8 GB requirement

Before checkout, confirm two things: the datacenter nearest your users, and the billing cycle plus OS template you actually want. Both are selected during the order, and changing the OS later means a reinstall that wipes the disk.

👉 [Compare all five RackNerd Linux VPS plans and order](https://bit.ly/RacKnerd)
