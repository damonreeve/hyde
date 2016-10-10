---
layout: page
title: Implementation Architecture
---

There are a number of different configurations that can be utilized when deploying Bidstream Optimizer. Choosing the right one depends on individual preference based on the level of control and risk mitigation you want to introduce.

1. [CNAME DNS (Recommended)](#1--cname-dns--recommended-)
1. [Change API endpoints](#2--change-api-endpoints)
1. [Side Loading](#3--side-loading)

Whether you are a DSP or an SSP/Exchange any of these implementations are applicable. See [Optimizer for DSP](#) and [Optimizer for SSP](#) for implementation scenario's.

<a id="1--cname-dns--recommended-"></a>
## 1. CNAME DNS (Recommended)

The following architecture provides the highest level of control and flexibility for the both the customer and Authenticated in managing all failover scenarios.

![FAILOVER SETUP](https://docs.google.com/drawings/d/1uO5VKL-3CHp3TD25OElKXlbRmnVqkshkwVe7tP5u53c/pub?w=934&h=526)

### Supply Stream URL
This should be to a subdomain managed by the customer. This should be changed with the supplier if a dedicated URL is not currently being used.

```
[SUPPLIER].[CUSTOMER].com
```

For a standard Optimizer configuration this URL should CNAME to the Authenticated Stream URL.

> In the event of an Authenticated system failure the customer can change the CNAME to the Customer Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).

### Bidstream Optimizer URL
This is the URL the stream should CNAME to. This is to access the Optimizer service.

```
[SUPPLIER].[CUSTOMER].rtb.authenticated.digital
```

Once Optimizer processes a bid request it passes the request on to the Customer Bidder URL

> In the event of an Authenticated system failure Authenticated can change the CNAME to the Customer Bidder URL (Option A), or if a failover server is installed then to the Failover Server URL (Option B).

### Customer Bidder URL
This is the URL for the bidder. All optimized streams are forwarded to this URL.

```
bidder.[CUSTOMER].com
```

### Failover server URL (Optional)
An optional step to protect the bidder from being flooded with requests in the event of Authenticated critical failure, is to install a failover server within the customer stack to handle inbound bidstreams and throttle requests passed through to the bidder. This is a simple nginx server that is configured to send a set percentage of requests to the bidder and to ignore the rest. This way traffic will still flow through to the bidder but not the full stream from the supplier. The volume of requests to pass through is a simple server configuration. A repository for the server configuration can be found [here].

```
failover.[CUSTOMER].com
```

<a id="2--change-api-endpoints"></a>
## 2. Change API endpoints

Changing API endpoints with the supplier is a simpler implementation to making any CNAME DNS change.

![API ENDPOINT CHANGE](https://docs.google.com/drawings/d/1-uZh8grkXfV3SFbZFIq-ScCM1xBXbrXeFDvRfI4eZ64/pub?w=934&h=526)

### Supply Stream URL
This should be changed to the a URL supplied by Authenticated which will point to the Optimizer service.

```
[SUPPLIER].[CUSTOMER].rtb.authenticated.digital
```

> In the event of an Authenticated system failure the supply stream URL will be changed from the Bidstream Optimizer URL to the Customer Bidder URL.

<a id="3--side-loading"></a>
# 3. Side Loading

In specific circumstances (particularly under high load conditions) it is possible for Bidstream Optimizer to recieve specific fields from a stream and respond with whether the request should be filtered. This is a more conventional `Pre-bid` implementation but would require the platform to be able to act on the information that is passed back from Bidstream Optimizer.

> Note this is a deep integration and not a standard implementation of Bidstream Optimizer. There is no failover protection required as Bidstream Optimizer is simply acting as a data enrichment partner.

![SIDE LOAD](https://docs.google.com/drawings/d/1AaAgIoOovc-v1vTnrn4GuYraMjG1nEbcicggkpCcIs0/pub?w=934&h=526)
