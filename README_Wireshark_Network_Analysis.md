# Network Traffic Analysis Using Wireshark

## Project Overview

This project documents a practical network-traffic analysis exercise
using **Wireshark** on a Windows computer. Traffic was captured on the
Ethernet interface and examined using display filters to understand DNS,
TCP, and UDP communication.

## Objectives

-   Capture network packets from a local Ethernet interface.
-   Identify source and destination IP addresses and port numbers.
-   Inspect DNS queries and matching responses.
-   Understand basic TCP and UDP traffic characteristics.
-   Record observations without treating normal network activity as
    malicious.

## Environment and Tools

-   Operating system: Windows
-   Packet analyzer: Wireshark 4.6.9
-   Capture interface: Ethernet
-   Capture file format: PCAPNG

## Methodology

1.  Opened Wireshark and selected the active Ethernet interface.
2.  Captured normal network activity while using the computer.
3.  Applied display filters to isolate relevant traffic.
4.  Inspected packet details, protocol fields, and request/response
    relationships.
5.  Recorded observations and prepared a report.

## Display Filters Used

  -----------------------------------------------------------------------
  Filter                              Purpose
  ----------------------------------- -----------------------------------
  `dns`                               Display DNS packets

  `tcp`                               Display TCP packets

  `udp`                               Display UDP packets

  `dns.flags.response == 0`           Display DNS queries

  `dns.flags.response == 1`           Display DNS responses

  `dns.flags.rcode != 0`              Find DNS responses with non-zero
                                      response codes
  -----------------------------------------------------------------------

## DNS Analysis -- Observed Example

A DNS query for `web.whatsapp.com` was observed.

  Field                   Observed value
  ----------------------- ---------------------------
  Querying host           `192.168.0.170`
  DNS resolver            `192.168.0.1`
  Query type              A (IPv4 address)
  Transport               TCP, destination port 53
  Query packet            38
  Response packet         47
  DNS response            No error
  CNAME                   `mmx-ds.cdn.whatsapp.net`
  Returned IPv4 address   `57.144.211.32`
  Response time           Approximately 6.2757 ms
  CNAME TTL               495 seconds
  A-record TTL            55 seconds

The different TTL values indicate different cache lifetimes for the
alias and address records. DNS over TCP is supported and is not, by
itself, evidence of suspicious activity.

## TCP and UDP Analysis

TCP and UDP traffic were filtered and inspected to understand their
packet structure and transport behavior. TCP provides
connection-oriented, reliable delivery; UDP is connectionless and has
lower protocol overhead. Include only packet examples and observations
actually verified in the accompanying capture. Do not infer a security
incident from protocol usage alone.

## Findings and Security Observations

-   The observed DNS request received a successful response.
-   The response included a CNAME and an IPv4 address.
-   The capture demonstrated DNS communication over TCP port 53.
-   No malicious activity or security incident is concluded from this
    DNS exchange alone.
-   Any additional TCP/UDP observations should be supported by the saved
    capture and screenshots.

## Evidence

Add screenshots that show: 1. Wireshark interface with the Ethernet
capture selected. 2. DNS query packet details (packet 38). 3. DNS
response packet details (packet 47), including the CNAME, A record, and
response time. 4. TCP packet details or a TCP stream/handshake, if
captured and verified. 5. UDP packet details, if captured and verified.

Redact public IPs, local identifiers, MAC addresses, hostnames, or other
information if needed before making screenshots public.

## Limitations

-   This is a small sample of ordinary traffic from one capture session.
-   A packet capture represents only the traffic visible on the selected
    interface during the capture period.
-   The absence of suspicious packets in this sample does not prove that
    a network is completely secure.
-   The report should not claim a confirmed attack unless supported by
    packet-level evidence.

## Conclusion

The exercise provided practical experience in capturing and filtering
network traffic, correlating DNS requests with responses, and inspecting
TCP/UDP communication. It also reinforced the importance of interpreting
packet evidence carefully and distinguishing normal protocol behavior
from genuinely suspicious activity.
