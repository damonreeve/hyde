Bidstream Optimizer Trial One-pager

Something we get asked a bit is "what's the fastest and easiest way to try out Optimizer?". 

While bidstream optimizer can do amazing things for platform performance, and deploying can be relatively simple, it can touch many different parts of a platforms architecture and therefore involve many people in decision-making and onboarding.

So what's the easiest way to evaluate Optimizer to see if its right for your platform? We've put this one-pager together to visualize what a quick evaluation of Optimizer can look like.

5 Steps to a Bidstream Optimizer trial

1. Choose supply to evaluate
1. Pick a datacenter
1. Determine KPIs
1. Go Live
1. Review Performance

## Choose supply to evaluate

Optimizer is designed to manage a supply stream. When onboarding we generally will migrate suppliers one at a time. So to run a trial pick one supplier that you want to evaluate. Don't make it your best performing supplier. Choose one that is causing you problems and you were about to cancel them. The risk to you is much lower that way. Maybe they aren't generating many matched requests. Or maybe there are concerns about supply quality.

## Pick a data-center

Overall latency is a big challenge in programmatic advertising. In a full deployment Optimizer will generally be co-locat in your data center or with your cloud provider (if we aren't there already). If you are operating from multiple data-centers then we will co-locate in multiple data-centers.

For a trial pick one data-center. If it's a datacenter that's in or near an AWS or GCE location (eg Virginia or California or Frankfurt) then we won't need to install anything as latency between our platforms will be low. 

## Determine KPIs

It's always good to know what success looks like before running a trial. Nice to know what we are aiming for!

This is largely dependent on what you are trying to achieve as a business. As a prompt here are some of the more common ones

Strategy | Description | Measure
Maximise revenue with constant QPS | I want to cap the inbound QPS from this supplier and maximise the revenue I generate from them | Revenue / QPS
Constant Revenue with minimum QPS | I want to cap the demand I am giving to this supplier and want to reduce the bidstream down to the minimum possible | Revenue / QPS
Fraud and Quality filtering | I want to remove all fraudulent and low/zero quality inventory from the suppliers stream | Authentication Rate
Direct inventory | I only want directly sourced inventory from the supplier (remove arbitrage and duplicate header bidding requests from the bidstream) without losing access to supply | Direct %; count(distinct domains/apps)

## Go Live

Once we have determined the supplier, which location we are testing and what our test criteria are it's time to go live. Here is the list of simple tasks for onboarding

Task | Who | Description
Sign a test agreement | Both | The test period is no charge, but it's good to have a simple agreement that covers each party for the test
Create a new Optimizer account | Authenticated | So you have access to our admin console, generate api keys and endpoints
Update Optimizer with bidder endpoint | Authenticated | This is so Optimizer send requests to the right place
Update supplier with new Authenticated endpoint | Supplier/Authenticated | This then sends the bidstream to Authenticated instead of directly to your bidder. This can also be CNAMED from your DNS provider rather than updating the endpoint if preferred
Monitor bidstream | You | Real-time monitoring will activate so you can see the profile of your bidstream. We can immediately begin applying filters based on your target strategy
