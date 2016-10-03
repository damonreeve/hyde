---
layout: page
title: How Optimizer Works
---

Bidstream Optimizer is a bidstream management layer that analyzes in real time the bidstream that is passing from one ad platform to another and enables a set of controls and filters based on information contained in the bidstream.

Optimizer is designed as a pre-processor to make generalised decisioning that doesn't interfere with the specific decisioning an exchange or DSP makes.

* [Built for scale](#built-for-scale)
* Simple implementation
* Real-time monitoring
* 5-Step run-time process
  * Basic Filtering
  * Quality and Fraud Filtering
  * Commercial Profiling
  * Data Enrichment
  * Throttling
  
<a name="built-for-scale"></a>
## Built for scale

Optimizer executes a very specific set of decisions very quickly. The objective is to provide control over the bidstream while adding negligible latency or impact to the platform. Optimizer adds no more than `3ms` of internal latency to any bidstream regardless of scale.

## Distributed Architecture

Optimizer architecture is separated into Optimizer run-time nodes that are a stateless, distributed set of services that can be run in any location, and central services for deep level analysis and model maintenance.

Optimizer run-time nodes will generally be co-located inside a clients data-center to reduce any connectivity latency between the service and platform. Read more about [Deployment Scenario's](deployment-scenarios).

## Simple Implementation

Optimizer

## 5-Step run-time process

The 5 primary steps every bid request passes through is:

1. Basic Filtering
1. Quality and Fraud Filtering
1. Commercial Profiling
1. Data Enrichment
1. Throttling

### Basic Filtering
