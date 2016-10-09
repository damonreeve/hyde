---
layout: page
title: Bidstream Optimizer Trial One-pager
---

Bidstream Optimizer can do amazing things for your platform's performance, and while deploying it can be relatively simple, the process can touch many different parts of a platform's architecture, and thus involve a lot of people in the onboarding process. 

So what's the easiest way to try Optimizer, and see if it's right for your platform? We've put this one-pager together to visualize what a quick evaluation of Optimizer can look like.

__4 Steps to a Bidstream Optimizer trial__

1. Choose a Supplier You'd Like to Evaluate
2. Pick a Data Center
3. Determine KPIs
4. Go Live

## 1. Choose a Supplier You'd Like to Evaluate

Optimizer is designed to manage a supply stream. When onboarding, we will generally will migrate one supplier at a time. So to run a trial, pick just one supplier that you want to evaluate; perhaps one that is causing you problems, or one that you were considering canceling anyway due to cost or quality concerns. Then the risk to you is minimal.

## 2. Pick a Data Center

Just as it's easiest to start with one supplier and then expand, it's easiest to integrate with one data center for the duration of a trial. Ideally, your test data center is near an AWS or GCE location (such as Virginia or Frankfurt), and we can be assured that latency will be low. We can test the TTL from your chosen data center to the nearest Authenticated data center to ensure minimal impact.

## 3. Determine KPIs

Before running a trial, it's important to know what success looks like. This is of course dependent on your organization's goals, and A|D will work with you to carve out reliable metrics and benchmarks. Below are some examples from our existing client base:

| Strategy | Metric |
| :-------- | :-------- |
| Maximize revenue without increasing infrastructure costs | **Profit margin**: (Revenue - QPS costs)/QPS costs |
| Minimize costs given a fixed revenue stream | **Profit margin**: (Revenue - QPS costs)/QPS costs |
| Remove fraudulent inventory from my bidstream | **Authentication rate**: Authentic impressions/Total impressions |
| Cut out indirect inventory (remove arbitrage and duplicate header bids) | **Direct traffic rate**: Direct impressions/Total impressions |


## 4. Go Live!


Going live can be boiled down to just a few simple tasks, as follows:


| Task | Description | Who's Responsible |
:-------- | :-------- | :-------- |
| 1. Sign a test agreement | There's no charge for a trial, but test agreements are important for setting expectations. | Client/AD |
| 2. Create an Optimizer account | This gives you access to our admin console, and generates API keys and endpoints. | AD |
| 3. Test and QA | Test the configuration to ensure that data is flowing end-to-end. | Client/AD |
| 4. Update test supplier with the new AD endpoint | This step reroutes traffic from your bidder to AD; alternatively, this can be CNAMED from your DNS provider. | Supplier/AD |
| 5. Monitor bidstream | AD has a variety of dashboards that will allow you to monitor the real-time performance of your AD bidstream, and propose changes to your filters. | Client |
