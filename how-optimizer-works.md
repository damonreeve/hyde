---
layout: page
title: How Optimizer Works
---

Bidstream Optimizer analyzes in real-time a stream of bid requests that passes from one ad platform to another (a "bidstream") and provides monitoring to determine the content of the bidstream and a set of controls to enrich or filter each bid request in the stream.

Optimizer is designed as a pre-processor to make generalised decisioning that doesn't interfere with the specific decisioning an exchange or DSP makes.

## Built for scale

Optimizer performs a very specific set of tasks very quickly. The objective is to provide control over the bidstream while adding negligible latency. Optimizer adds no more than `3ms` of internal latency to any bidstream regardless of scale.

## Distributed Architecture

Optimizer architecture is separated into Optimizer run-time nodes that are a stateless, distributed set of services that can be deployed into any data-center, and central services for deep level analysis and model maintenance.

## Simple Implementation

Optimizer run-time nodes will generally be co-located inside or near a clients data-center to reduce any connectivity latency between the Optimizer service and the client's platform. Read more about [Deployment Scenario's](deployment-scenarios).

## 5-Step run-time process

Step | Type | Description | Example
--- | --- | --- | ---
Basic Filtering | --- | --- | ---
Quality and Fraud Filtering | --- | --- | ---
Commercial Profiling | --- | --- | ---
Data Enrichment | --- | --- | ---
Throttling | --- | --- | ---
