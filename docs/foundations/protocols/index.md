---
title: Open Protocols
parent: Foundations
grand_parent: Theory
---

# Open Protocols

An **open protocol** is a set of rules and data formats that define how two or more systems communicate, published publicly so that anyone may read, implement and extend the specification without licensing fees or vendor lock-in. Open protocols are the foundation of interoperability: any client that follows the specification can talk to any server that follows it, regardless of the vendor that produced the software.

Because the specification is public, open protocols encourage competing implementations, improve auditability and keep the ecosystem free from proprietary control. They are distinct from proprietary protocols, which are controlled by a single vendor and typically require licensed implementations.

## The Internet transport layer

- **TCP/IP** — the fundamental protocol suite of the Internet. IP provides addressing and routing at layer 3; TCP provides reliable, ordered, connection-oriented delivery at layer 4; UDP provides lightweight, connectionless delivery.
- **DNS** — the Domain Name System translates human-readable names into IP addresses. It is a distributed, hierarchical database maintained by many cooperating servers.
- **DHCP** — the Dynamic Host Configuration Protocol assigns IP addresses and network configuration to hosts automatically.
- **TLS** — Transport Layer Security provides encryption, authentication and integrity for traffic between two endpoints; it is the security layer under HTTPS, IMAPS, SMTPS and many other protocols.

## Application-layer protocols

- **HTTP/HTTPS** — the Hypertext Transfer Protocol is the foundation of the World Wide Web, used to transfer web pages, APIs and media.
- **FTP / SFTP** — file transfer protocols. Classic FTP is unencrypted; SFTP runs over SSH and is the standard for secure file transfer.
- **SSH** — Secure Shell provides encrypted remote login, command execution and file transfer between computers.
- **SMTP** — the Simple Mail Transfer Protocol delivers email between servers.
- **IMAP and POP3** — mail access protocols: IMAP keeps mail on the server and synchronises folders; POP3 downloads mail to the client.
- **SIP** — the Session Initiation Protocol sets up, manages and tears down real-time sessions such as voice and video calls (used in IP telephony, see [Asterisk](../../communications/voip/asterisk.md)).
- **RTP/RTCP** — Real-time Transport Protocol carries the actual audio/video packets in VoIP and WebRTC sessions, with RTCP providing statistics and control.
- **WebRTC** — a set of standards and APIs for real-time audio, video and data communication between browsers and applications, built on SRTP, ICE and DTLS.

## Messaging and federation

- **XMPP (Jabber)** — an open, federated instant-messaging protocol with extensions for voice/video via Jingle. See the [XMPP Messenger guide](../../guides/xmpp-messenger.md).
- **Matrix** — an open protocol for decentralised, real-time communication with end-to-end encryption. See the [Matrix Messenger guide](../../guides/matrix-messenger.md) and [Synapse](../../communications/messaging/synapse.md).
- **ActivityPub** — a federated social-networking protocol used by Mastodon, PeerTube, Pixelfed and the [Fediverse](../../communications/fediverse/index.md).
- **IRC** — the Internet Relay Chat protocol, one of the oldest and simplest open chat protocols, still widely used by open-source communities.

## Discovery and directories

- **LDAP** — Lightweight Directory Access Protocol for reading and searching directory services (users, groups, devices). Used by [FreeIPA](../../security/directory-services/freeipa.md) and [Samba 4](../../security/directory-services/samba4.md).
- **Kerberos** — an authentication protocol based on symmetric key cryptography and a trusted third party (the KDC). It is central to Active Directory and FreeIPA.
- **RADIUS** — AAA (Authentication, Authorization, Accounting) protocol used by network access servers, [FreeRADIUS](../../networking/intrusion-prevention/freeradius.md) being a prominent open implementation.

## Related pages

- [Open Standards](../standards/index.md) — the formal specifications built on open protocols.
- [Foundations](../index.md) — the theory and knowledge base of the wiki.