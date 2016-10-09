---
layout: page
title: Optimizer Strategies
---

Might be a simple thing to ask but not always so simple to answer as you may be trying to achieve more than one thing when introducing Bidstream Optimizer.

## Define a Strategy - What does success look like?

While there may be more than one ambition it's good to have an overarching objective. That way you can be clear on what success looks like and set targets to achieving this.

To help we have described here some popular strategies worth considering. More than one of these may be important but aim for one to be primary.

## Demand-side Strategies

These strategies are most suited to a demand platform (DSP) or a supply platform that is ingesting inventory from a third party via API.

Strategy | Description | Metric
:--- | :--- | :---
[Reduce OPEX without affecting spend](#reduce-opex-without-affecting-spend) | I want to reduce my infrastructure costs by removing any bid requests that aren't generating any bid activity without affecting gross spend | Gross Spend; Spend / QPS
Remove low quality inventory | I want to remove any fraudulent or low quality inventory from my bidstream | Authentication Rate
Maximize top line revenue but not increase infrastructure costs | :--- | :---
Enrich bid requests with new data to maximize revenue (as a supplier) | :--- | :---
Turn on new supply | :--- | :---

## Supply-side Strategies

These strategies are for a supply platform that is managing the outbound bidstream it is sending to it's demand partners.

Strategy | Description | Metric
:--- | :--- | :---
Profile demand partner bidstream to inventory that generates value to a fixed output QPS | :--- | :---
Enrich bid requests with new data to maximize revenue | :--- | :---
Turn on new demand | :--- | :---

<a id="#reduce-opex-without-affecting-spend"></a>
### Reduce OPEX without affecting spend

Objective

You have steady/fixed demand but the volume of bid requests you have to manage is rising. You want to remove bid requests that aren't generating any value from your bidstream to reduce infrastructure costs and platform load.

Background

There are underlying causes for the rise in bid requests: header bidding, bid duplication by exchanges/SSPs and arbitrage. There are also many bid requests that are passed in streams that have zero value to the demand partner. For example, if you only buy video inventory then you only want to receive video inventory in your stream. But often this is not the case.

Strategy

With Bidstream Optimizer you can implement a commercial strategy to remove supply that is generating no bid activity. This will slowly remove from the bidstream those requests that are not relevant ensuring that spend levels are not affected in any way. There is always a percentage of inventory that is allowed through in the bidstream as a control group to ensure that inventory is not filtered out that may meet future demand.

KPIS

KPI | Description
:--- | :---
Gross Spend | Should be monitored to ensure there is minimal impact on Gross Spend
Gross Spend / QPS | This value should be rising compared to the control group. As the spend stays constant but the overall volume of supply reduces the Spend / QPS will rise

Controls - Adjusting Strategy

Different levels of filtering can be applied to Optimizer to reduce the bidstream. The more aggressive the filtering the greater the risk to Gross Spend, but also the greater the reduction in OPEX. Deciding what the "threshold" should be is individual choice.

This is best illustrated in the following chart:




Run-time Monitoring





### Remove low quality inventory
### Maximize top line revenue but not increase infrastructure costs
### Enrich bid requests with new data to maximize revenue (as a supplier)
### Turn on new supply
### Profile demand partner bidstream to inventory that generates value to a fixed output QPS
### Enrich bid requests with new data to maximize revenue
### Turn on new demand
