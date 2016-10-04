---
layout: page
title: Implementation Architecture
---

There are a number of different configurations that can be utilized when deploying Bidstream Optimizer. Choosing the right one depends on individual preference based on the level of control and risk mitigation you want to introduce.

1. [CNAME DNS (Recommended)](#cname-dns-recommended-architecture-)
1. [Change API endpoints](#change-api-endpoints)
1. [Side Loading](#side-loading)

## Recommended architecture - CNAME DNS

The following architecture provides the highest level of control and flexibility for the both the client and Authenticated in managing all failover scenarios.

![FAILOVER SETUP](https://docs.google.com/drawings/d/1uO5VKL-3CHp3TD25OElKXlbRmnVqkshkwVe7tP5u53c/pub?w=934&h=526)

### Supply Stream URL
This should be to a subdomain managed by the client. This should be changed with the supplier if a dedicated URL is not currently being used.
```
opera.admedo.com
```

For a standard Optimizer configuration this URL should CNAME to the Authenticated Stream URL.

> In the event of an Authenticated system failure the client can change the CNAME to the Client Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).

### Bidstream Optimizer URL
This is the URL the stream should CNAME to. This is to access the Optimizer service
```
opera.admedo.rtb.authenticated.digital
```

Once Optimizer processes a bid request it passes the request on to the Client Bidder URL

> In the event of an Authenticated system failure Authenticated can change the CNAME to the Client Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).

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

## Change API endpoints


