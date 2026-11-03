---
layout: post
title: "Exploring the Benefits of Carbon-Aware Routing"
date: 2026-11-02
paper_authors: "S. El-Zahr, P. Gunning, N. Zilberman"
paper_venue: "CoNEXT 2023"
paper_url: "https://dl.acm.org/doi/10.1145/3629165"
week: 6
tags: [carbon emissions, green networking, routing]
---

## Key Idea

ISP routing ignores the fact that a router's carbon cost depends on how clean its local power grid is at the moment. The paper measures how much carbon-aware routing can actually save, comparing power- and carbon-based link costs on real ISP networks. The authors propose **CATE**, a heuristic that also switches off lightly used links on high-carbon routers. The main finding is mostly negative, as rerouting alone saves little because most of a router's power goes to just being on; hence vendors need to redesign equipment to cut idle power.

## Critique

The paper is convincing because it tests on real ISP networks (BT and GEANT) with real, time-varying carbon data for each region, and it explains why the savings are small, e.g., idle power, bottleneck nodes, and short streaming paths.Less convincing is that the power numbers come from stand-in datasheets rather than the routers these networks actually run, and that CATE’s savings are a best case, since it switches links off with no limit on added delay and no requirement to keep backup paths. I would have also liked the authors to discuss any carbon cost of manufacturing the new routers they recommend.

## Connections

[Raha](/cs440-blog/2026/10/05/wan/) shows that a WAN relies on spare links to absorb failures, but those spare links are exactly what CATE switches off, so running Raha on CATE's reduced network could potentially show how much resilience the carbon savings cost.
