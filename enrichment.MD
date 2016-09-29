## Introduction

The Bidstream Optimizer Enrichment API provides an interface for bid requests to be enriched at run-time with external data, to increase the value and targeting options for a bid request. Enriching data can be sourced from 1st party datasets, or can be licensed from 3rd parties, such as DMPs. 

The purpose of the Authenticated Enrichment API is to provide platforms with a standard interface for the integration of data and data partners, reducing the upfront resource overhead for integrating a new data partner and reducing the time to market for new product.

## Architecture built for scale and low latency

The Bidstream Optimizer Enrichment API is designed to enrich bid requests at high scale, while adding negligible latency to the bidstream. 

[include a diagram]

1. Bid requests are passed to Bidstream Optimizer by a supply partner.
2. An internal services layer checks to see if the request qualifies for enrichment by any external data sources. If so, each qualified data source is passed parameters from the bid request to get data to enrich the bid request with. 
3. Once a response is received from the enrichment partners Optimizer collates and organises the data and inserts it into the bid request. 
4. The bid request is then passed on to the demand platform that can target campaigns based on the enriched dataset. 

## Caching and co-location

Bidstream Optmizer implements a local cache infront of any data enrichment partner in order to minimize latency. Cache refresh rates are set based on the recommendation of the data partners and are often different for each partner. Any inbound bid request will first be passed to the cache for a response. If the cache passes nothing back then a request is then made to the data service.

Depending on cache hit rates, we generally recommend each data partner co-locate within the Authenticated data center to minimize timeouts. 

[diagram showing the cache architecture]

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

## Timouts

A timeout for each enrichment is set to `2ms`. If no response is received by the cache or data service within this time then the bid request is not enriched. This timeout is not configurable.

## Data Sources

### 1st party data - custom integration

If you have your own data that you would like to enrich the bid request with then we can create a custom enrichment service just for you. Contact us if you would like to enrich your bid requests with custom data and we can get you set up.

### 3rd Party data partners

Authenticated enables a simple plugin framework for working with 3rd party data partners. This significantly reduces development time and gets you to market faster with new integrations.

Because there are contractual considerations specific to each data partner, it's not currently possible to create a new data partner connection using the API. This needs to be set up with your account rep. Once it's active then you are able to use the API to configure.

The following 3rd party data partners are available to you for enrichment

Company | Service Description
--- | ---
Grapeshot | Contextual categorization of URLs, brand safety categories
Comscore | Brand safety, categorization

Contact us if you would like to set up an enrichment service with one of these partners.

## Managing Data partners and bidstreams

Data enrichments are configured for each `stream` you have running with Bidstream Optimizer. This is because you may have different data partners set up for each stream or supplier. For example in the US you may be using one data provider but in Europe you have a different partner.

### List Data partners

To know which data partners you have available and which are already assigned to a stream you can use the following command;
```
curl 'http://localhost:4000/api/data/partners' \
-H 'Authorization: Bearer <enter your token here>' 
```

You will get a response similar to this:

```
{
   "data.partners":[
      {
         "name":"Grapeshot",
         "id":1,
         "active_streams": [1,4,5]
      },
      {
         "name":"Comscore",
         "id":2
      }
   ]
}
```

### Turning data enrichment partners on or off

To turn on an enrichment partner you can do so by using.
```
curl -X POST \
'http://localhost:4000/api/data/partners'
-H 'Authorization: Bearer <enter your token here>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-d '{ "data.partners.id": 2, "status": "active" }' \
```

You will get a response similar to this:

```
{
   "data.partners":[
      {
         "name":"Comscore",
         "id":2,
         "active_streams": [1,4,5]
      }
   ]
}
```

This will turn off the data partner across all streams it is currently active.

If you want to turn the data partner off for a specific stream then include the stream_id
```
curl -X POST \
'http://localhost:4000/api/data/partners'
-H 'Authorization: Bearer <enter your token here>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-d '{ "data.partners.id": 2, "stream_id": 4, "status": "active" }' \
```

To turn a data partner off you would use the following
```
curl -X POST \
'http://localhost:4000/api/data/partners'
-H 'Authorization: Bearer <enter your token here>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-d '{ "data.partners.id": 2, "status": "inactive" }' \
```

Or for a specific stream:
```
curl -X POST \
'http://localhost:4000/api/data/partners'
-H 'Authorization: Bearer <enter your token here>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-d '{ "data.partners.id": 2, "stream_id": 4, "status": "inactive" }' \
```

You will get a response similar to this:

```
{
   "data.partners":[
      {
         "name":"Comscore",
         "id":2,
         "active_streams": [1,5]
      }
   ]
}
```

## Example enrichment

By default bid requests are enriched by modifying the `ext` object. Each data partner has it's own taxonomy for describing and structuring the data enriching the bid request. There is specific documentation for each data partner that you will need to review before setting up your bidder to intepret the data.

Other fields in the bid request can be modified, particularly if you are using 1st party data. This can be discussed during when setting up a new data source.

Example

Here's the same bid request after it has been enriched by Grapeshot (the changes are highlighted)
```
// Indicative bid request with Grapeshot enrichment
// Enrichment can be modified to meet bidder requirements as needed

{
    "channels": [
        {
            "name":gs_employment",
            "score":12.133
        },
        {
            "name":"gs_society",
            "score":10.219
        },
        {
            "name":"gs_economy",
            "score":9.44
        }
    ]
}


{
  "wseat": [
    "167"
  ],
  "user": {
    "keywords": "",
    "ext": {
      "ug": 0
    }
  },
  "tmax": 240,
  "site": {
    "ref": "http:\/\/kissmanga.com\/ads\/adprotect300.aspx",
    "publisher": {
      "name": "KissManga_MW_KissManga_MW_300x250_ATF_MobileWebsite_MEDIUMRECTANGLE_300x250_IAB1",
      "id": "smaato_1100004890"
    },
    "page": "kissmanga.com",
    "name": "KissManga_MW_KissManga_MW_300x250_ATF_MobileWebsite_MEDIUMRECTANGLE_300x250_IAB1",
    "id": "smaato_130159609",
    "ext": {
      
    },
    "cat": [
      "IAB1"
    ]
  },
  "regs": {
    "coppa": 0
  },
  "imp": [
    {
      "tagid": "smaato_130159609",
      "secure": 0,
      "instl": 0,
      "id": "1",
      "ext": {
        
      },
      "exp": 300,
      "displaymanagerver": "adtag2218s",
      "displaymanager": "SOMA",
      "bidfloorcur": "USD",
      "bidfloor": 0.01134,
      "banner": {
        "w": 300,
        "pos": 1,
        "mimes": [
          "text\/javascript",
          "application\/javascript",
          "image\/jpeg",
          "image\/png",
          "image\/gif",
          "text\/html",
          "text\/plain"
        ],
        "h": 250,
        "btype": [
          1
        ],
        "battr": [
          1,
          3,
          5,
          6,
          8,
          9
        ],
        "api": [
          
        ]
      }
    }
  ],
  "id": "67cb34fd-1bed-42ef-b247-89b48b9dfc6b",
  "ext": {
    "wt": 141.23529411765,
    "ssp": "smaato",
    "is_secure": 0,
    "clktrkrq": 0,
    "grapeshot": {
        "channels": [
            {
                "name":gs_employment",
                "score":12.133
            },
            {
                "name":"gs_society",
                "score":10.219
            },
            {
                "name":"gs_economy",
                "score":9.44
            }
        ]
    }
  },
  "device": {
    "ua": "Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/49.0.2623.112 Safari\/537.36",
    "osv": "",
    "os": "Unknown",
    "model": "",
    "make": "generic web browser",
    "js": 1,
    "ip": "67.188.74.221",
    "geo": {
      "zip": "93940",
      "type": 1,
      "region": "CA",
      "lon": -121.8406,
      "lat": 36.369904,
      "country": "US",
      "city": "Monterey"
    },
    "devicetype": 1,
    "connectiontype": 2
  },
  "cur": [
    "USD"
  ],
  "bcat": [
    "IAB23",
    "BSW2",
    "BSW10",
    "BSW4",
    "IAB26",
    "IAB25",
    "BSW1",
    "IAB24",
    "IAB25-3",
    "IAB7-42",
    "IAB9-9",
    "IAB17-18",
    "IAB7-28"
  ],
  "badv": [
    "ezmob.com"
  ],
  "at": 2
}
```

## Interpreting data enrichments in your bidder

Once the bid request is enriched the data must be discoverable within your bidder. 

## Reporting on data usage

Most pre-bid data enrichment companies operate an honesty system for the use of pre-bid data in targeting. If a campaign is using pre-bid data in its campaign targeting then [served impressions] [bids?] are chargeable by the data company.

As a safety check, Authenticated applies models to double check whether impressions have used enriched data in targeting. This data is only ever used if there is a discrepancy.

To see how much enriched data has been used in targeting then you can check by using the following:

```
curl -X POST \
'http://localhost:4000/api/data/stats'
-H 'Authorization: Bearer <enter your token here>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-d '{ "data.partners.id": 2, "stream_id": 8 }' \
```

### Parameters

FIELD | TYPE | DESCRIPTION
--- | --- | ---
partners.id | INTEGER | the id of the data partner
stream_id | INTEGER | the id of the stream
from | DATE | default is first day of this month
to | DATE | default is yesterday

A typical response would be:

```
{
   "data":[
      {
         "partner":"Grapeshot",
         "id":1,
         "from": "2016-09-01",
         "to": "2016-09-14",
         "win_count": 123,456
      }
   ]
}
```
