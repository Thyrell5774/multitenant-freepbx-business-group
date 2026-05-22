# Multi-Tenant FreePBX — 5-Company Business Group

![FreePBX](https://img.shields.io/badge/FreePBX-Multi--Tenant-FF6600?style=flat-square)

![MikroTik](https://img.shields.io/badge/MikroTik-RouterOS-CC0000?style=flat-square)

![SIP](https://img.shields.io/badge/SIP-Per--Tenant_Trunks-4CAF50?style=flat-square)

![VPN](https://img.shields.io/badge/VPN-Site--to--Site-9C27B0?style=flat-square)

**Role:** VoIP & Network Engineer  
**Scale:** 5 companies · 75+ users · Single hosted FreePBX  
**Deployment:** On-site hosted PBX serving a multi-company business group  
**Status:** Live — actively maintained  

---

## Project Overview

Designed and deployed a multi-tenant FreePBX system for a business group 
operating 5 separate companies under single ownership. Each company runs 
as a fully isolated tenant on a shared FreePBX instance — separate 
extensions, dedicated DIDs, individual IVR menus, independent call 
routing, and its own SIP trunk. Tenants connect via a combination of 
site-to-site VPN and public IP, with a mix of Yealink, Grandstream, 
and softphone clients across all sites.

Despite sharing a single PBX instance, each company operates completely 
independently — no crossover in extensions, call routing, or visibility 
between tenants.

---

## Infrastructure Summary

| Component | Detail |
|---|---|
| PBX Platform | FreePBX (on-site hosted) |
| Total Tenants | 5 companies |
| Users per Tenant | 15 |
| Total Users | 75+ |
| SIP Trunks | Separate trunk per company |
| Connectivity | Mixed — VPN + Public IP |
| Phones | Yealink · Grandstream · Softphones |
| Tenant Isolation | Full — extensions, DIDs, IVR, routing |
| Ownership | Single business group owner |

---

## Architecture

### Multi-Tenant Design
- Each company configured as a fully **isolated tenant** within FreePBX
- Separate extension ranges per tenant — no overlap or crossover
- Each tenant has its own **dedicated DID number(s)** for inbound calls
- Individual **IVR menus** per company with custom voice recordings
- Separate **outbound routes and SIP trunks** per company — 
  each business presents its own caller ID on outbound calls
- Call recording, CDR, and reporting isolated per tenant — 
  one company cannot see another's call history

### Connectivity
- **VPN-connected sites** — MikroTik site-to-site VPN tunnels 
  back to the hosted FreePBX server
- **Public IP sites** — phones register directly via public IP 
  and port forwarding with IP whitelisting and strong credentials
- **Softphone users** — connect remotely via SIP credentials 
  over public IP

### SIP Trunking
- Each of the 5 companies has its own **dedicated SIP trunk**
- Outbound calls route through the correct company trunk 
  automatically based on the originating extension
- Inbound DIDs route to the correct company IVR without 
  any crossover between tenants

---

## Per-Tenant Features

Each of the 5 companies has the following configured independently:

- ✅ Dedicated DID inbound number(s)
- ✅ Custom IVR menu with dedicated voice recordings
- ✅ Ring groups — simultaneous and sequential ringing options
- ✅ Call queues with hold music and overflow routing
- ✅ Outbound routes with correct CLI presentation per company
- ✅ Call recording for compliance and quality monitoring
- ✅ CDR reporting — call history per company
- ✅ Custom music on hold
- ✅ Time-based routing — business hours and after-hours handling
- ✅ Separate SIP trunk with independent inbound and outbound routing

---

## Phone Deployment

- **Yealink phones** — auto-provisioned via FreePBX EPM 
  (End Point Manager) using MAC-based templates
- **Grandstream phones** — provisioned via FreePBX EPM 
  with model-specific config templates
- **Softphones** — SIP credentials distributed to remote 
  and mobile users connecting over public IP
- All phones receive correct extension, SIP credentials, 
  and feature settings automatically on first boot

---

## Challenges & Solutions

**Challenge:** Configuring 5 completely isolated tenants on a single 
FreePBX instance required careful planning to prevent extension range 
collisions and ensure inbound DID routing always reached the correct 
company without crossover.  
**Solution:** Designed a structured extension numbering plan before 
deployment — each company assigned a dedicated range with no overlap. 
Inbound routes mapped each DID exclusively to its tenant IVR. Tested 
all inbound and outbound routing per tenant before going live.

---

**Challenge:** Each company needed its own outbound caller ID so 
customers would see the correct business name and number on outbound 
calls — not a generic number shared across all tenants.  
**Solution:** Configured separate SIP trunks and outbound routes per 
company with CID forcing enabled in FreePBX — every outbound call 
presents the correct company caller ID regardless of which extension 
initiates the call.

---

**Challenge:** Remote softphone users connecting over public IP 
experienced NAT traversal issues causing one-way audio and 
registration instability.  
**Solution:** Configured FreePBX SIP settings for correct NAT 
traversal — external IP and local network defined, STUN enabled 
for remote clients. Softphone users configured with correct 
SIP transport settings — registration and audio stabilised.

---

**Challenge:** Provisioning a mix of Yealink and Grandstream phones 
across 5 tenants required each device to receive the correct 
extension and company-specific settings without manual programming.  
**Solution:** Used FreePBX End Point Manager — MAC addresses 
registered per device, model templates built for both Yealink 
and Grandstream, and tenant-specific settings applied per 
extension. Phones auto-configured on first boot with zero 
manual programming required.

---

## Key Outcomes

- **5 fully isolated companies** on a single FreePBX instance — 
  no crossover in extensions, routing, recording, or CDR
- **Independent caller ID** per company on all outbound calls
- **Zero manual phone programming** — all devices auto-provisioned 
  via FreePBX EPM across both Yealink and Grandstream hardware
- **Centralised management** for the business group owner — 
  one PBX to manage, five independent phone systems delivered
- **Flexible connectivity** — VPN, public IP, and softphone 
  clients all supported simultaneously

---

## Related Projects

| Project | Scale | Stack |
|---|---|---|
| 🔧 [FreePBX Enterprise Multi-Site VoIP](https://github.com/Thyrell5774/freepbx-enterprise-multisite) | 11 branches · 180+ users | FreePBX · MikroTik · SIP |
| 🔧 [MikroTik Multi-Site VPN Network](https://github.com/Thyrell5774/mikrotik-vpn-multisite) | 11 sites · 165+ users | MikroTik · L2TP · QoS |
| 🔧 [Grandstream UCM Enterprise Deployment](https://github.com/Thyrell5774/grandstream-ucm-enterprise) | 10 branches · 150+ users | Grandstream UCM · MikroTik · SIP |
| 🔧 [UniFi Hotel Enterprise Network](https://github.com/Thyrell5774/unifi-hotel-enterprise-network) | 2 blocks · 3 floors · 22 APs | UniFi · UDM-SE · Grandstream |

---

## About

**Thyrell Naidoo** — Senior Network & VoIP Engineer, Johannesburg SA  
7+ years managing enterprise VoIP and networking infrastructure across South Africa.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-thyrellnaidoo-0077B5?style=flat-square&logo=linkedin)](https://linkedin.com/in/thyrellnaidoo)

[![Credly](https://img.shields.io/badge/Credly-Certifications-FF6B00?style=flat-square&logo=credly)](https://credly.com/users/thyrell-naidoo)

[![Email](https://img.shields.io/badge/Email-Thyrell.naidoo@gmail.com-D14836?style=flat-square&logo=gmail)](mailto:Thyrell.naidoo@gmail.com)
