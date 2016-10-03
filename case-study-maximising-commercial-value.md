---
layout: page
title: Case Study - Maximising commercial value
---

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

The key measure of success in both of these strategies is the revenue that is generated from the QPS passed to the bidder (`Revenue / QPS`).

## 1. Reducing QPS to meet demand

In this strategy an assumption is made that there is no latent demand from the platform and the primary objective is to reduce costs by filtering the bidstream to meet available demand. The point at which revenue starts to fall is the maximum filter rate available.

<table>
<tr><td></td><td>BASELINE</td><td>LOW </td><td>MEDIUM </td><td>HIGH </td><td>MAX </td></tr>
<tr><td>Inbound QPS</td><td>7,843</td><td>8,376</td><td>9,565</td><td>11,975</td><td>13,333</td></tr>
<tr><td>Inbound Net Revenue</td><td>$24,627</td><td>$26,301</td><td>$30,036</td><td>$37,602</td><td>$41,867</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td>Impression Filter Rate</td><td>0%</td><td>20%</td><td>40%</td><td>60%</td><td>80%</td></tr>
<tr><td>Revenue Filter Rate</td><td>0%</td><td>6.3%</td><td>18.0%</td><td>34.5%</td><td>41.1%</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td>Outbound QPS</td><td>7,843</td><td>6,701</td><td>5,739</td><td>4,790</td><td>2,666</td></tr>
<tr><td>Outbound Net Revenue</td><td>$24,627</td><td>$24,627</td><td>$24,627</td><td>$24,627</td><td>$24,627</td></tr>
<tr><td></td><td></td><td></td><td></td><td></td><td></td></tr>
<tr><td>Infrastructure</td><td>$11,764</td><td>$10,051</td><td>$8,609</td><td>$7,185</td><td>$4,000</td></tr>
<tr><td>Cost Reduction</td><td>0</td><td>1.6%</td><td>10.2%</td><td>18.7%</td><td>37.6%</td></tr>
</table>

In this example, you can see the effect of using Authenticated with different filter rates, and the vastly lowered QPS needed to achieve the same spend levels.  At the highest filter setting (, the same spend can be achieved with 1/3 of the inbound traffic.  This can reduce infrastructure costs by more than a third.

## 2. Increasing Bidstream Revenue (Constant QPS Worksheet)
In this example, Authenticated was used to improve the quality of the bidstream - and you can see the effect of different Authenticated settings for the same QPS levels.  Authenticated can deliver higher quality, more commercially viable inventory, so that if AOL advertisers have latent demand, the same QPS can generate 2.5x more profit (e.g. net revenues minus infrastructure costs and Authenticated fees), and 4x more revenues.

In both examples, Authenticated uses a commercial model and a quality model to achieve these results.  The underlying raw SSP traffic in this example had a 2% bid rate, 50% win rate, and 75% impression rate before Authenticated was enabled.

Authenticated fees are $1K + 30% revenue uplift in this case.

We will also send through the before/after metrics regarding supply quality for each of the cases (e.g. recycled/arbitraged inventory, accurately described inventory, etc.)





## PUBLISHER DIRECT MODEL

By using the "publisher direct" quality model, and filtering out "recycled" and "secondary" suppliers, we are able to control the bidstream to allow the best supplier for inventory without reducing access to any publisher domains or apps. With be bidstreams we have live this is resulting in the ability to filter 20% of bid requests without reducing acccess to any supply (web domains or apps) and only reducing impression supply by 5%.

By using the "publisher direct" quality model, and filtering out "recycled" and "secondary" suppliers, you can bid on only the best supplier without reducing access to any publisher domains.  Our model in general will allow you to filter 20% of bids which are deemed duplicate supply, which removes only 5% of impressions. Note that the 5% of impressions will not necessarily be lost.  These are most likely impressions that will be won on the best supplier rather than the secondary supplier in the future if you implement these rules.  You just won't be bidding against yourself.
