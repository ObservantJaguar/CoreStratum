---
grand_parent: Practice
title: IP Telephony
parent: Guides
---

# IP Telephony

## Goal

A self-hosted **IP PBX (private branch exchange)** for a small organization using open-source software: internal calls between employees, voicemail, IVR, call queues, and optional connection to the public telephone network via a **SIP trunk** from an operator. Softphones run in the browser or on mobile phones over **WebRTC** — no desk phones required.

The primary stack is **FreePBX** (on top of Asterisk) or **VitalPBX** (also Asterisk-based, modern administration UI). This guide covers both.

## Scope and out of scope

**In scope:**
- PBX installation (FreePBX or VitalPBX)
- Internal extensions for users
- Softphone/WebRTC clients
- Voicemail, IVR, ring groups, call queues
- SIP trunk integration (external calls)
- Recording, monitoring and backup of the PBX

**Out of scope:**
- Complex contact-center/ACD deployments
- Fax over IP (possible later with T.38)
- High-availability clustering

## The Asterisk family: choose your UI

| | FreePBX | VitalPBX | Issabel |
|---|---|---|---|
| Base | Asterisk | Asterisk | Asterisk |
| UI style | Battery-included, huge module ecosystem | Modern, focused | All-in-one distro (also mail/messaging) |
| Docs/community | Largest | Active | Smaller |
| Best for | Any SMB, most instructions online | Teams wanting a cleaner UX | Turnkey appliance approach |

This guide assumes **FreePBX** (most documentation) and notes VitalPBX differences where relevant.

## Prerequisites

- A dedicated VM or a small server (2 GB RAM, 2 vCPU minimum; 4 GB more comfortable)
- A static IP or a stable domain for remote admin (optional)
- A SIP provider if you need external calls (or just internal PBX)
- Firewall: UDP 5060/5061 (SIP/TLS), UDP 10000РІР‚вЂњ20000 (RTP media), 8089 (WebRTC), 80/443 (admin)

## Architecture

```
   РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’        РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’        РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’
   РІвЂќвЂљ Browser  РІвЂќвЂљ WebRTC РІвЂќвЂљ                          РІвЂќвЂљ  SIP   РІвЂќвЂљ  SIP trunk  РІвЂќвЂљ
   РІвЂќвЂљ softphoneРІвЂќвЂљРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ   FreePBX / VitalPBX    РІвЂќвЂљРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ (operator)  РІвЂќвЂљ
   РІвЂќвЂљ (JitsiРІР‚В¦) РІвЂќвЂљ        РІвЂќвЂљ   РІвЂќвЂќРІвЂќР‚ Asterisk            РІвЂќвЂљ        РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
   РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ        РІвЂќвЂљ   РІвЂќвЂќРІвЂќР‚ MySQL/MariaDB        РІвЂќвЂљ
   РІвЂќРЉРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќС’        РІвЂќвЂљ   РІвЂќвЂќРІвЂќР‚ Web admin (HTTPS)    РІвЂќвЂљ
   РІвЂќвЂљ Mobile   РІвЂќвЂљ  SIP   РІвЂќвЂљ                          РІвЂќвЂљ
   РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂ“С”РІвЂќвЂљ                          РІвЂќвЂљ
                        РІвЂќвЂќРІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќР‚РІвЂќВ
```

## Roadmap

### Stage 1 — Install the PBX

The simplest path is to install the PBX as the whole OS (FreePBX distro or VitalPBX ISO), on a VM with bridged networking. Skip this if you prefer running inside Docker — FreePBX is not officially container-friendly; the ISO/VM approach is the community standard.

- [ ] Download and install **FreePBX Distro** (or VitalPBX) on a VM
- [ ] Set the hostname, network and admin password during install
- [ ] Note the IP and open the web admin UI

### Stage 2 — Initial configuration

- [ ] Complete the first-run wizard (time zone, admin password, extension range)
- [ ] Set the external SIP port and RTP port range
- [ ] Change default credentials for the web UI and add an admin

### Stage 3 — Create extensions (users)

In FreePBX: **Applications РІвЂ вЂ™ Extensions**, choose **PJSIP** (modern) or **CHAN_SIP** (legacy).

- [ ] Create one extension per employee (e.g. 200, 201, 202...)
- [ ] Set the secret (SIP password) and voicemail PIN
- [ ] Assign a password policy

### Stage 4 — WebRTC softphones

- [ ] Enable the WebRTC module (FreePBX: **Settings РІвЂ вЂ™ WebRTC**, or use "FreePBX WebRTC" app)
- [ ] Configure the API to use HTTPS (a domain + Let's Encrypt from the Traefik/TLS layer)
- [ ] Connect a WebRTC client (e.g. **Jitsi Meet phone**, **WebRTC Softphone**, or the built-in browser client)
- [ ] Test an internal call between two extensions

### Stage 5 — Mobile softphones

- [ ] Install a SIP client on phones: **Zoiper** (free), **Linphone**, **Jami**, **Sipdroid**
- [ ] Configure the server IP/domain, port 5060, transport UDP/TLS
- [ ] Enable STUN for NAT traversal (or run behind a VPN — see [VPN](../networking/vpn/index.md))

### Stage 6 — Voicemail, IVR, queues

- [ ] Assign voicemail box to each extension (done in Stage 3)
- [ ] Create an **IVR** for the main number (Applications РІвЂ вЂ™ IVR)
- [ ] Create a **Ring Group** and a **Call Queue** for department phones
- [ ] Test: call the main number, follow the IVR, land in the queue

### Stage 7 — SIP trunk (external calls)

- [ ] Sign up with a SIP trunk provider (choose one that supports Asterisk)
- [ ] In FreePBX: **Connectivity РІвЂ вЂ™ Trunks**, add a SIP trunk with provider credentials
- [ ] Configure outbound routes (which extensions may call outside) and inbound routes (map the DID to the IVR/queue)
- [ ] Test an external call

### Stage 8 — Recording, monitoring, backup

- [ ] Enable call recording per extension (legal: inform users as required)
- [ ] Set up CDR reporting (call detail records) in the web UI
- [ ] Back up the PBX: `amportal backup` or the FreePBX Backup module (write to NFS/SSH)
- [ ] Include the backup destination in the main [Backup guide](backup-restic-borg.md)

## Verification

- [ ] Call between two internal extensions (audio both ways)
- [ ] Call to the external number through the SIP trunk (audio, correct CLID)
- [ ] Voicemail left and retrievable
- [ ] IVR route works from the outside line
- [ ] WebRTC softphone registers and rings
- [ ] CDR shows the call records
- [ ] After a restore from backup, extensions and trunks work again

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Phone registers but calls dead | RTP port range blocked or NAT | Open UDP 10000РІР‚вЂњ20000; set STUN/provided NAT handling in the client |
| One-way audio | NAT asymmetric audio | Enable symmetric RTP; set up STUN/TURN in the PBX |
| WebRTC won't connect | Browser requires HTTPS | Use a domain + Let's Encrypt for the WebRTC API endpoint |
| External calls fail | SIP trunk or route not set | Check trunk status (Connectivity РІвЂ вЂ™ Trunks), outbound route, provider docs |
| Incoming calls dumped to operator | Inbound route missing | Create inbound route DID РІвЂ вЂ™ IVR/queue/extension |

## Related pages

- [Asterisk](../communications/voip/asterisk.md)
- [FreePBX](../communications/voip/freepbx.md)
- [VitalPBX and Issabel](../communications/voip/vitalpbx.md)
- [Kamailio and FreeSWITCH (alternatives)](../communications/voip/kamailio.md)
- [Matrix Messenger guide (chat + video)](matrix-messenger.md)