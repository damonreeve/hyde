---
layout: page
title: Failover
---

# Managing DNS and failover

There are a number of different configurations that can be utilized when deploying Bidstream Optimizer. Choosing the right one depends on individual preference based on the level of control and risk mitigation you want to introduce.

## Recommended architecture - CNAME DNS

The following architecture provides the highest level of control and flexibility for the both the client and Authenticated in managing all failover scenarios.

![FAILOVER SETUP](https://docs.google.com/drawings/d/1uO5VKL-3CHp3TD25OElKXlbRmnVqkshkwVe7tP5u53c/pub?w=934&h=526)

### Supply Stream URL
This should be to a subdomain managed by the client. This should be changed with the supplier if a dedicated URL is not currently being used.
```
opera.admedo.com
```

For a standard Optimizer configuration this URL should CNAME to the Authenticated Stream URL.

`In the event of an Authenticated system failure the client can change the CNAME to the Client Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).`

### Bidstream Optimizer URL
This is the URL the stream should CNAME to. This is to access the Optimizer service
```
opera.admedo.rtb.authenticated.digital
```

Once Optimizer processes a bid request it passes the request on to the Client Bidder URL

`In the event of an Authenticated system failure Authenticated can change the CNAME to the Client Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).`

### Client Bidder URL
This is the URL for the bidder. All optimized streams are forwarded to this URL.
```
bidder.admedo.com
```

### Failover server URL (Optional)
An optional step to protect the bidder from being flooded with requests in the event of Authenticated critical failure, is to install a failover server within the client stack to handle inbound bidstreams and throttle requests passed through to the bidder. This is a simple nginx server that is configured to send a set percentage of requests to the bidder and to ignore the rest. This way traffic will still flow through to the bidder but not the full stream from the supplier. The volume of requests to pass through is a simple server configuration. A repository for the server configuration can be found [here].
```
failover.admedo.com
```


## System Failure and actions

The primary objective is to mitigate risk in the event of a system failure. System failure can result at three primary points in the service:
* Node/Application failure
* Data-center failure
* DNS failure

### Node/Application Failure
[define properly]

All Authenticated nodes are elastic load-balanced, auto-scale with no single points of failure, which means if there is a failure at the application-level for a given node then traffic will shift to nodes that are active within the same data-center.

### Data-center Failure
[define properly] Authenticated's run-time nodes are most-often co-located with the bidder, which means any failure at a data-center has likely affected the bidder as well.

### DNS Failure
This is where the Authenticated service domain is no longer accessible.

## Automated fail-over vs manual failover
With the high availability nature, and extensive monitoring and alerting on all aspects of the service, we recommend not implementing an automated failover solution. 
