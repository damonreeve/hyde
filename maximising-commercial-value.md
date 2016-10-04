---
layout: page
title: Maximising commercial value
---

# Case Study

There are many different strategies that can be employed when using Bidstream Optimizer. You may want to

* maximise commercial value from a throttled bidstream
* remove arbitrage and duplicated bid requests
* remove fraud, or simply 
* filter requests that you can't sell

Optimizer can implement these strategies in a simple, fast and controllable way.

Its important that with any changes you make to your bidstream there is a clear understanding of what success looks like and KPI's are measured.

Outlined here are the results of two similar strategies focusing on the commercial value of the bidstream, but with some important differences:

1. Reducing QPS to meet demand
1. Maximising Revenue

The key measure of success in both of these strategies is the revenue that is generated from the bidstream QPS (`Revenue / QPS`).

## 1. Reducing QPS to meet demand

In this strategy an assumption is made that there is no latent demand from the platform and the primary objective is to reduce costs by filtering the bidstream to meet available demand. Another assumption is that there is enough quality supply available to meet the demand. The point at which revenue starts to fall is the maximum filter rate available.

 | BASELINE | LOW | MEDIUM | HIGH | MAX
:--- | ---: | ---: | ---: | ---: | ---:
Inbound QPS | 7,843 | 8,376 | 9,565 | 11,975 | 13,333
Inbound Net Revenue | $24,627 | $26,301 | $30,036 | $37,602 | $41,867
 |  |  |  |  | 
Impression Filter Rate | 0% | 20% | 40% | 60% | 80%
Revenue Filter Rate | 0% | 6.3% | 18.0% | 34.5% | 41.1%
 |  |  |  |  | 
Outbound QPS | 7,843 | 6,701 | 5,739 | 4,790 | 2,666
Outbound Net Revenue | $24,627 | $24,627 | $24,627 | $24,627 | $24,627
 |  |  |  |  | 
Infrastructure | $11,764 | $10,051 | $8,609 | $7,185 | $4,000
Cost Reduction | 0 | 1.6% | 10.2% | 18.7% | 37.6%


<table class="case-study">
<tr><td></td><td>BASELINE</td><td>LOW </td><td>MEDIUM </td><td>HIGH </td><td>MAX </td></tr>
<tr><td class="l">Inbound QPS</td><td>7,843</td><td>8,376</td><td>9,565</td><td>11,975</td><td>13,333</td></tr>
<tr><td class="l">Inbound Net Revenue</td><td>$24,627</td><td>$26,301</td><td>$30,036</td><td>$37,602</td><td>$41,867</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Impression Filter Rate</td><td>0%</td><td>20%</td><td>40%</td><td>60%</td><td>80%</td></tr>
<tr><td class="l">Revenue Filter Rate</td><td>0%</td><td>6.3%</td><td>18.0%</td><td>34.5%</td><td>41.1%</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Outbound QPS</td><td>7,843</td><td>6,701</td><td>5,739</td><td>4,790</td><td>2,666</td></tr>
<tr><td class="l">Outbound Net Revenue</td><td>$24,627</td><td>$24,627</td><td>$24,627</td><td>$24,627</td><td>$24,627</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Infrastructure</td><td>$11,764</td><td>$10,051</td><td>$8,609</td><td>$7,185</td><td>$4,000</td></tr>
<tr><td class="l">Cost Reduction</td><td>0</td><td>1.6%</td><td>10.2%</td><td>18.7%</td><td>37.6%</td></tr>
</table>

Actual platform revenue (`Outbound Net Revenue`) is fixed at $24,627. As the filter rate increases so does the inbound QPS to ensure there are enough relevant impressions passing through the filter to meet demand.

As the filtering increases and the bidstream becomes more relevant, infrastructure costs start to come down (`Infrastructure`)as the platform doesn't need to process as many requests (`Outbound QPS`).

In this case study, infrastructure costs savings of over 37% were achieved with zero impact on revenue.

## 2. Increasing Bidstream Revenue (Constant QPS)

If growth is constrained by infrastructure capacity and there is significant latent demand available, then a different commercial model can be applied, where the inbound bidstream to the platform is fixed and the most relevant bidstream is passed into the system to meet the latent demand.

<table class="case-study">
<tr><td></td><td>BASELINE</td><td>LOW </td><td>MEDIUM </td><td>HIGH </td><td>MAX </td></tr>
<tr><td class="l">Inbound QPS</td><td>7,843</td><td>9,803</td><td>13,071</td><td>19,607</td><td>39,215</td></tr>
<tr><td class="l">Inbound Net Revenue</td><td>$24,627</td><td>$30,783</td><td>$41,045</td><td>$61,567</td><td>$12,3135</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Impression Filter Rate</td><td>0%</td><td>20%</td><td>40%</td><td>60%</td><td>80%</td></tr>
<tr><td class="l">Revenue Filter Rate</td><td>0%</td><td>6.3%</td><td>18.0%</td><td>34.5%</td><td>41.1%</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Outbound QPS</td><td>7,843</td><td>7,843</td><td>7,843</td><td>7,843</td><td>7,843</td></tr>
<tr><td class="l">Outbound Net Revenue</td><td>$24,627</td><td>$28,823</td><td>$33,653</td><td>$40,322</td><td>$72,430</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td class="l">Infrastructure</td><td>$11,764</td><td>$11,764</td><td>$11,764</td><td>$11,764</td><td>$11,764</td></tr>
<tr><td class="l">Profit Uplift</td><td>0%</td><td>15.0%</td><td>41.3%</td><td>77.6%</td><td>252.3%</td></tr>
</table>

In this study the QPS to the platform (`Output QPS`) is kept constant at 7,843 QPS. The `Inbound QPS` to Optimizer is increased to find the most relevant bid requests for the latent demand growing from 7,843 to 39,215 QPS. 

The net revenue impact is significant growing to more than 2.5x with maximum filtering.

-----
