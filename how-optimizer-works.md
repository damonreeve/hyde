---
layout: page
title: How Optimizer Works
---

Bidstream Optimizer analyzes in real-time a stream of bid requests that passes from one ad platform to another (a "bidstream"), provides monitoring to determine the content of the bidstream and a set of controls to enrich or filter each bid request in the stream.

Optimizer is designed as a pre-processor to make generalised decisioning that doesn't interfere with the specific decisioning a customer platform makes.

![Optimizer Architecture](https://docs.google.com/drawings/d/1aTqqnJSk6gunFY6p2bSZY_VG7h3ZTyuTvoGfbRwvT0E/pub?w=1072&h=294)

## Built for scale

Optimizer performs a very specific [set of tasks](#5-step-run-time-process) very quickly. The objective is to provide control over the bidstream while adding negligible latency. Optimizer adds no more than `3ms` of internal latency to any bidstream regardless of scale.

## Distributed Architecture

Optimizer architecture is separated into run-time Optimizer Nodes that are a stateless and can be deployed into any data-center, and Central Services for analysis and model training.

## Simple Implementation

Optimizer Nodes are generally co-located inside or near a clients data-center to reduce any connectivity latency between the Optimizer service and the Customer Platform. Read more about [Deployment Scenario's](../#deployment-scenarios).