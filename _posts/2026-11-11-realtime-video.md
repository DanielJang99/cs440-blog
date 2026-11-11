---
layout: post
title: "Responsive Congestion Control for Real-Time Video"
date: 2026-11-11
paper_authors: "P. Karimi, S. Fouladi, V. Sivaraman, M. Alizadeh"
paper_venue: "NINeS 2026"
paper_url: "https://2026.nines-conference.org/papers/p009-Karimi.pdf"
week: 7
tags: [real-time traffic, congestion control, video streaming]
---

## Key Idea
Real-time video rate controllers like WebRTC’s GCC take seconds to react to network changes, because the encoder sends frames in unpredictable bursts and the congestion controller loses steady feedback from the network. 
Instead of modifying the codec, the authors propose **Vidaptive**, which paces video packets at the congestion controller’s rate and fills any gaps with dummy packets, so an existing delay-based algorithm (e.g., Copa) always sees a backlogged flow. It then sets the encoder’s target bitrate to a fraction of that rate, adjusted online to keep frame latency within a target.

## Critique
I found the paper's core idea simple and convincing, and the ablation study shows that the dummy traffic drives the gains, and an analysis with an idealized encoder shows that the tradeoff between latency and quality is built into variable links (rather than design flaw).
However, the authors claim that it inherits the congestion controller’s fairness without testing against competing flows, which matters because the padding uses up capacity, data and battery, and the authors only mention this in passing.

## Connections
Like [LeoCC](/cs440-blog/2026/11/09/leo/), Vidaptive shows that congestion control breaks down when conditions change faster than the controller can observe them. But while LeoCC tailors the algorithm to LEO satellite dynamics, Vidaptive keeps the general-purpose CC algorithm and instead reshapes the traffic it sees (e.g., padding the video stream to mimic backlogged flow). 
