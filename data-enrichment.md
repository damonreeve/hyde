---
layout: page
title: Data Enrichment
---

## Introduction

Bidstream Optimizer provides an interface for bid requests to be enriched at run-time with external data, to increase the value and targeting options for a bid request. Enriching data can be sourced from 1st party datasets, or can be licensed from 3rd parties, such as DMPs. 

The purpose of the enrichment service is to provide platforms with a standard interface for the integration of data and data partners, reducing the upfront resource overhead for integrating a new data partner and reducing the time to market for new product.

## Bidstream Enrichment Workflow

![Data Enrichment Workflow](https://docs.google.com/drawings/d/1CCpxSkW7agj19ZmJq_ZeBhp8kuBTxl1upUfVrQqItfA/pub?w=1020)

## Bidder

There are two important changes that need to be made to the bidder:

1. __Targeting__:The bidder must be pre-configured to be able to allow for data from a specific data partner to be used in campaign planning
1. __Matching__:The bidder needs to recognize the data in the bid request when making bids and target accordingly

Bidder modification is outside of the scope of the Optimizer enrichment service. The examples provided here are to explain how it works.

### Targeting

In the bidder configuration new fields need to be made available in campaign targeting and stored with the line item targeting parameters.

For example consider the following 24 standard targeting segments provided by Grapeshot:

![Grapeshot Standard Segments](https://damonreeve.github.io/optimizer-docs/grapeshot_segments.png)

Each segment has subsegments that can be drilled in to. For example the News segment is structured in the following way:

```
"gs_news": {
    "name": "gs_news",
    "display_name": "gs_news",
    "type": "standard",
    "subtype": "reach",
    "total": 2,
    "channels": {
        "gs_news_and_weather": {
            "name": "gs_news_and_weather",
            "display_name": "gs_news_and_weather",
            "type": "standard",
            "subtype": "primary",
            "channelset": {
                "english": {
                    "published": "live",
                    "readonly": true,
                    "safety": false,
                    "hidden": false,
                    "active": true,
                    "throttle": 1
                }
            }
        }
    }
}
```

The bidder must be modified to allow end-users to target these segments. Specific advice and documentation can be provided by each data provider.

### Matching

When the bidder receives a bid request it must be able to interpret the new data being passed in the bid request and match to any campaigns accordingly.

Using the Grapeshot News segment example again, the bid request received from Bidstream Optimizer for the URL `http://qz.com/805563` would look like this:

```
{
	 "id": "67cb34fd-1bed-42ef-b247-89b48b9dfc6b",
	 "ext": {
	 	"Grapeshot": {
			"channels": [
				{
					  "name": "gs_news",
					  "score": 54.300
				},
				{
					  "name": "gs_news_and_weather",
					  "score": 32.239
				}
			]
		}
	 }
}
```

Any campaigns targeting `gs_news` or `gs_news_and_weather` can be matched to this bid request.

## Bidstream Optimizer

Optimizer performs four primary functions

1. Receives bid requests from suppliers
1. Calls the enrichment cache to see if there is any data to enrich the bid request with
1. Enriches the bid request with any data, generally as a new explicitly named data object in the `ext` object of the bid request
1. Passes the bid request on to the bidder

## Data Partner

This is the data source providing the information to enrich the bid request with. Each data partner provides two datasets:

1. A taxonomy of data fields and descriptions that the bidder uses to enable targeting to be setup up
1. A mapping table that is used at run-time by Bidstream Optimizer to enrich a bid request with specific data when conditions match. This will generally be a database or file that is maintained by the data partner. 

There are more specific details for these data partners:
* Grapeshot
* Comscore
* Lotame

## Cache

Bidstream Optmizer implements a local cache infront of any data enrichment partner in order to minimize latency. Cache refresh rates are set based on the recommendation of the data partners and are often different for each partner. Any inbound bid request will first be passed to the cache for a response. If the cache passes nothing back then a request is then made to the data service.

A timeout for each enrichment is set to `2ms`. If no response is received by the cache or data service within this time then the bid request is not enriched. This timeout is not configurable.

Depending on cache hit rates, we generally recommend each data partner co-locate within the Authenticated data center to minimize timeouts. 

## Enrichment Parameters

Authenticated makes available a standard set of parameters from the bid request. The parameters are:

OpenRTB object | Description
--- | ---
site.page | URL of the page where the impression will be shown
app.bundle | A platform-specific application identifier intended to be unique to the app and independent of the exchange. On Android, this should be a bundle or package name (e.g., com.foo.mygame). On iOS, it is a numeric ID.
app.domain | Domain of the app (e.g., “mygame.foo.com”).
app.storeurl | App store URL for an installed app; for IQG 2.1 compliance.
device.ua | Browser user agent string.
device.ip | IPv4 address closest to device.
device.geo.lat | Latitude from -90.0 to +90.0, where negative is south.
device.geo.lon | Longitude from -180.0 to +180.0, where negative is west.
device.geo.country | Country code using ISO-3166-1-alpha-3.
user.id | Exchange-specific ID for the user. At least one of id or buyeruid is recommended.
user.buyerid | Buyer-specific ID for the user as mapped by the exchange for the buyer. At least one of buyeruid or id is recommended.
device.ifa | ID sanctioned for advertiser use in the clear (i.e., not hashed).
didsha1 | Hardware device ID (e.g., IMEI); hashed via SHA1.
didmd5 |   Hardware device ID (e.g., IMEI); hashed via MD5.
dpidsha1 |   Platform device ID (e.g., Android ID); hashed via SHA1.
dpidmd5 |   Platform device ID (e.g., Android ID); hashed via MD5.
macsha1 |   MAC address of the device; hashed via SHA1.
macmd5 |   MAC address of the device; hashed via MD5.


## Data Sources

### 1st party data - custom integration

If you have your own data that you would like to enrich the bid request with then we can create a custom enrichment service just for you. Contact us if you would like to enrich your bid requests with custom data and we can get you set up.

## Managing Data partners and bidstreams

Data enrichments are configured for each `stream` you have running with Bidstream Optimizer. This is because you may have different data partners set up for each stream or supplier. For example in the US you may be using one data provider but in Europe you have a different partner.
