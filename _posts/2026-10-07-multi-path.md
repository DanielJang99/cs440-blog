---
layout: post
title: "Unlocking ECMP Programmability for Precise Traffic Control"
date: 2026-10-07
paper_authors: "Y. Liu, Y. Xiao, X. Zhang et al."
paper_venue: "NSDI 2025"
paper_url: "https://www.usenix.org/conference/nsdi25/presentation/liu-yadong"
week: 1
tags: [data-center fabrics, ecmp, multi-path routing]
---

## Key Idea
ECMP's random hashing balances data center traffic well in aggregate but prevents precise per-flow control. The paper's core contribution is P-ECMP, which repurposes the ECMP-group feature of commodity switches into a control matrix whose row is selected by a header field. End hosts can then select a flow's path by an offset or pin exact next hops, while all other traffic still uses ordinary ECMP. 

## Critique
The one-year Tencent deployment is the most convincing part, as it showed that on heterogeneous commodity switches alongside production traffic, P-ECMP brought most network-failure downtime under a minute. 
However, the premise that ECMP groups sit unused is measured only in Tencent's DCN, which undermines the generalizabilty of the paper's proposal. 

## Connections
This paper discusses silent packet drops, where only flows hashed onto a bad path are impacted. This is analogous to the notion of "peninsulas" in  [Baltra et al.,](/cs440-blog/2026/09/28/partial-reachability/), in the sense that reachability depends on which path you take, leading to partial failures getting missed in aggregate health checks. It's interesting hwo the lack of observability is a recurring theme in many of the papers we've read so far. 