---
layout: page
title: How Optimizer Works
---

Bidstream Optimizer is a bidstream management layer that analyzes in real time the bidstream that is passing from one ad platform to another and enables a set of controls and filters based on information contained in the bidstream.

Optimizer is designed as a pre-processor to make generalised decisioning that doesn't interfere with the specific decisioning an exchange or DSP makes.

## Built for scale

Optimizer executes a narrow set of decisions very quickly. The objective is to provide control to the bidstream while adding negligible latency or impact to the platform. Optimizer adds no more than 3ms of internal latency to any bidstream regardless of scale.

An Optimizer deployment will generally be co-located inside a clients data-center to reduce any connectivity latency between the service and platform.

## 4-Step run-time process

When optimizer receives a bid request
