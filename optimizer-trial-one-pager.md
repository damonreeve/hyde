---
layout: page
title: Bidstream Optimizer Trial One-pager
---

Something we get asked a bit is "what's the fastest and easiest way to try out Optimizer?". 

Bidstream Optimizer can do amazing things for platform performance, and deploying can be relatively simple, but it can touch many different parts of a platforms architecture and therefore involve many people in decision-making and onboarding.

So what's the easiest way to evaluate Optimizer to see if its right for your platform? We've put this one-pager together to visualize what a quick evaluation of Optimizer can look like.

__5 Steps to a Bidstream Optimizer trial__

1. Choose supply to evaluate
1. Pick a datacenter
1. Determine KPIs
1. Go Live
1. Review Performance

## Choose supply to evaluate

Optimizer is designed to manage a supply stream. When onboarding we generally will migrate suppliers one at a time. So to run a trial pick one supplier that you want to evaluate. Don't make it your best performing supplier. Choose one that is causing you problems and you were about to cancel them. The risk to you is much lower that way. Maybe they aren't generating many matched requests. Or maybe there are concerns about supply quality.

## Pick a data-center

Overall latency is a big challenge in programmatic advertising. In a full deployment Optimizer will generally be co-locat in your datacenter or with your cloud provider (if we aren't there already). If you are operating from multiple datacenters then we will co-locate in multiple datacenters.

For a trial pick one datacenter. If it's a datacenter that's in or near an AWS or GCE location (eg Virginia or California or Frankfurt) then we won't need to install anything as latency between our platforms will be low. 

## Determine KPIs

It's always good to know what success looks like before running a trial. Nice to know what we are aiming for!

This is largely dependent on what you are trying to achieve as a business. As a prompt here are some of the more common ones

<table>
<tr><th>Strategy</th><th>Description</th><th>Measure</th></tr>
<tr><td>Maximise revenue with constant QPS</td><td>I want to cap the inbound QPS from this supplier and maximise the revenue I generate from them</td><td>Revenue / QPS</td></tr>
<tr><td>Constant Revenue with minimum QPS</td><td>I want to cap the demand I am giving to this supplier and want to reduce the bidstream down to the minimum possible</td><td>Revenue / QPS</td></tr>
<tr><td>Fraud and Quality filtering</td><td>I want to remove all fraudulent and low/zero quality inventory from the suppliers stream</td><td>Authentication Rate</td></tr>
<tr><td>Direct inventory</td><td>I only want directly sourced inventory from the supplier (remove arbitrage and duplicate header bidding requests from the bidstream) without losing access to supply</td><td>Direct %; count(distinct domains/apps)</td></tr>
</table>

## Go Live!

Once we have determined the supplier, which location we are testing and what our test criteria are it's time to go live. Here is the list of simple tasks for onboarding

<table>
<tr><th>Task</th><th>Who</th><th>Description</th></tr>
<tr><td>Sign a test agreement</td><td>Both</td><td>The test period is no charge, but it's good to have a simple agreement that covers each party for the test</td></tr>
<tr><td>Create a new Optimizer account</td><td>Authenticated</td><td>So you have access to our admin console, generate api keys and endpoints</td></tr>
<tr><td>Update Optimizer with bidder endpoint</td><td>Authenticated</td><td>This is so Optimizer send requests to the right place</td></tr>
<tr><td>Test/QA</td><td>Authenticated/You</td><td>Test the configuration to make sure data is flowing end-to-end</td></tr>
<tr><td>Update supplier with new Authenticated endpoint</td><td>Supplier/Authenticated</td><td>This then sends the bidstream to Authenticated instead of directly to your bidder. This can also be CNAMED from your DNS provider rather than updating the endpoint if preferred</td></tr>
<tr><td>Monitor bidstream</td><td>You</td><td>Real-time monitoring will activate so you can see the profile of your bidstream. We can immediately begin applying filters based on your target strategy</td></tr>
</table>
