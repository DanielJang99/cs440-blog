---
layout: post
title: "Understanding Partial Reachability in the Internet Core"
date: 2026-09-30
paper_authors: "G. Baltra, T. Saluja, Y. Pradkin, J. Heidemann"
paper_venue: "NINeS 2026"
paper_url: "https://nines-conference.org/papers/p004-Baltra.pdf"
week: 1
tags: [partial reachability, outages, Internet core]
---

## Key Idea

While outage detectors often dismiss partial reachability as noise, the paper argues that it a fundamental and underexplored feature of the Internet casued by peering disputes, firewalls, NAT and political pressure. Its main contribution is a principled definition of "the Internet core" based on connectivity, which requires bidirectional reachability from more than 50% of active public IP addresses. The authors use this definition to derive *peninsulas* and *islands* separate from complete Internet outages, and show that they can enhance the sensitivity of measurement systems (e.g., RIPE's DNSmon). 


## Critique
The Internet core definition is elegant because it guarantees a single core and turns fragmentation into a concrete threshold, and the RIPE DNSmon case shows real operational value. But this definition is mostly symbolic; it seemingly doesn't matter for peninsula detection (Taitao), which just flags vantage points that disagree, and even island detection (Chiloe) mostly finds vantage points that can reach almost nothing, so the 50% cutoff rarely decides the outcome. Since observers agree on 98.5–99.5% of the core in practice, the threshold only matters in hypothetical scenarios like a large country seceding. The paper is also missing a way to separate ICMP filtering from actual unreachability. 


## Connections
This paper echoes back to [Misa et al.,](/2026/09/28/internet-invariants/) in how certain patterns in Internet measurement (here, vantage points disagreeing on reachability) could be structural feature of the Internet rather than an artificat. 