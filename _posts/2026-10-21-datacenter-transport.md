---
layout: post
title: "Simulate Before Sending: Rethinking Transport in Datacenter Networks"
date: 2026-10-21
paper_authors: "D. Straussman, I. Keslassy, A. Shpiner, L. Liss"
paper_venue: "NINeS 2026"
paper_url: "https://doi.org/10.4230/OASIcs.NINeS.2026.19"
week: 4
tags: [datacenter, transport, ai]
---

## Key Idea

AI training collectives are highly bursty, which often leads to packet drops and retransmissions that delay the entire collective in commodity datacenter networks. 
The authors propose **dcSim**, where each data packet is preceded by a tiny probe that takes a random path through a smaller high-priority queue, and the data packet later follows that exact path if its probe made it through. 
In effect, the probes act as per-packet reservations built from features commodity switches already have (traffic classes and token buckets), making the network practically lossless without new hardware.

## Critique

I found the idea of probing a path for congestion before sending data on it to be intuitive and convincing as a way to avoid packet loss, especially given that dcSim stays lossless even in the oversubscribed network. 
However, I am more skeptical of how it avoids multi-hop losses; the solution relies on a data buffer that holds twice as many packets as the probe buffer, a threshold found in one simulated setup with fixed per-port buffers, whereas DCTCP showed that busy ports in real shared-memory switches can shrink the buffer available to others.
Also missing is validation on real hardware: unlike DCTCP, which was grounded in production measurements and tested on commodity switches, dcSim is evaluated only in simulation. 


## Connections
In my [P-ECMP post](/cs440-blog/2026/10/07/multi-path/) I discussed silent drops, where only the flows hashed onto a bad path lose packets. dcSim addresses this from the end hosts by sending each probe on a new random path, so a bad path is revealed by losing a cheap probe instead of real data.