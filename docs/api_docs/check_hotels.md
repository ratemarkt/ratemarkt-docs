# Check Hotels

## Introduction

You can check for hotels available for any provided date range and pax information by specifying either a destination code or a list of hotel codes.

This resource is the first and the only required step before performing any booking but it is not the preferable way of doing because of higher probability of availability errors at the booking step.

!!! warning "Beware of Availability Errors"
    We strongly recommend using [Check Hotel][1] and [Check Rate][2] resources for retrieving the most recent availability and price information for hotels to prevent availability failures at the time of booking.

Because of higher amount of traffic populated on this step, most suppliers and Ratemarkt itself by nature serves the most of the availability information from cache storages.
Serving from cache storages may cause outdated data being served and can be misleading for clients at the time of booking.

So it is highly recommended using further availability resources such as [Check Hotel][1] and [Check Rate][2] before proceeding to booking step in order to prevent booking failures caused by availability errors.

[1]: /api_docs/check_hotel.md
[2]: /api_docs/check_rate.md

### Definition

```
POST https://api.ratemarkt.com/v1/checkhotels
```

### Query Object

<table>
    <colgroup>
        <col width="20%">
        <col width="20%">
        <col width="20%">
        <col width="40%">
    </colgroup>
    <thead>
        <tr>
            <th>Argument</th>
            <th>Type</th>
            <th>Required</th>
            <th width="33%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>destinationCode</code></td>
            <td><code>string</code></td>
            <td>optional*</td>
            <td>Destination code.</td>
        </tr>
        <tr>
            <td><code>hotelCodes</code></td>
            <td><code>list[string]</code></td>
            <td>optional*</td>
            <td>List of hotel codes.</td>
        </tr>
        <tr>
            <td><code>checkin</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>checkout</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-15</td>
        </tr>
        <tr>
            <td><code>paxes</code></td>
            <td><code>list[Pax]</code></td>
            <td>yes</td>
            <td>List of pax objects. Each pax object corresponds to a room. Multi room queries need more than one pax object.</td>
        </tr>
        <tr>
            <td><code>Pax.numberOfAdults</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Number of adults for the specified room.</td>
        </tr>
        <tr>
            <td><code>Pax.childrenAges</code></td>
            <td><code>list[integer]</code></td>
            <td>yes</td>
            <td>List of children ages for the specified room.</td>
        </tr>
        <tr>
            <td><code>currency</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Three letter currency code (ISO-4217). Only USD, EUR and GBP currencies are supported at the moment.</td>
        </tr>
        <tr>
            <td><code>nationality</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Two letter country code (ISO 3166-1 alpha-2) for occupants passport nationality.</td>
        </tr>
    </tbody>
</table>

!!! note "About Optional* Arguments"
    You should provide either `destinationCode` or `hotelCodes` argument to get your availability query work.

!!! warning "Beware of Destination Based Queries"
    Some popular travel destinations contain huge amount of hotels thus your queries may take much longer time then expected.

    We strongly recommend hotel list based queries so that you can perform your queries for only the hotels you interested in and get back corresponding results in much shorter times rather than retrieving a bulk.


## Example Query Objects

### Single room query for certain hotels

```json
{
    "hotelCodes": [
        "d31d12",
        "69af45",
        "984767"
    ],
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "paxes": [
        {
            "childrenAges": [],
            "numberOfAdults": 2
        }
    ],
    "currency": "USD",
    "nationality": "US"
}
```

### Multi room query for a certain destination

```json
{
    "destinationCode": "d31d12",
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",   
    "paxes": [
        {
            "childrenAges": [],
            "numberOfAdults": 1
        },
        {
            "childrenAges": [
                3,
                5
            ],
            "numberOfAdults": 2
        }
    ],
    "currency": "USD",
    "nationality": "US"
}
```

## Result Object

<table>
    <colgroup>
        <col width="20%">
        <col width="25%">
        <col width="5%">
        <col width="50%">
    </colgroup>
    <thead>
        <tr>
            <th>Argument</th>
            <th>Type</th>
            <th>Nullable</th>
            <th width="33%">Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>hotels</code></td>
            <td><code>list[Hotel]</code></td>
            <td>no</td>
            <td>List of available hotels</td>
        </tr>
        {! api_docs/_includes/hotel.md !}
    </tbody>
</table>

## Example Result Objects

### Single Room Result Object

```json
{
    "hotels": [
        {
            "countryCode": "TR",
            "destinationCode": "c36ca9",
            "destinationName": "istanbul",
            "hotelCode": "d31d12",
            "hotelName": "The Marmara Taksim",
            "rates": [
                {
                    "boardName": "ROOM ONLY",
                    "cancellationPolicies": [
                        {
                            "amount": 146.78,
                            "fromDate": "2017-07-19T23:59:00+03:00"
                        }
                    ],
                    "commission": null,
                    "currency": "EUR",
                    "hotelCurrency": null,
                    "hotelRate": null,
                    "nonrefundable": false,
                    "rate": 493.18,
                    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
                    "rateType": "NET",
                    "remarks": null,
                    "rooms": [
                        {
                            "numberOfAdults": 2,
                            "numberOfChildren": 0,
                            "roomDescription": "DOUBLE DELUXE CITY VIEW",
                            "sequence": 1
                        }
                    ]
                },
                {
                    "boardName": "ROOM ONLY",
                    "cancellationPolicies": [
                        {
                            "amount": 174.13,
                            "fromDate": "2017-07-19T23:59:00+03:00"
                        }
                    ],
                    "commission": null,
                    "currency": "EUR",
                    "hotelCurrency": null,
                    "hotelRate": null,
                    "nonrefundable": false,
                    "rate": 585.08,
                    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
                    "rateType": "NET",
                    "remarks": null,
                    "rooms": [
                        {
                            "numberOfAdults": 2,
                            "numberOfChildren": 0,
                            "roomDescription": "DOUBLE DELUXE CITY VIEW",
                            "sequence": 1
                        }
                    ]
                },
                {
                    "boardName": "BED AND BREAKFAST",
                    "cancellationPolicies": [
                        {
                            "amount": 175.94,
                            "fromDate": "2017-07-19T23:59:00+03:00"
                        }
                    ],
                    "commission": null,
                    "currency": "EUR",
                    "hotelCurrency": null,
                    "hotelRate": null,
                    "nonrefundable": false,
                    "rate": 591.19,
                    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|5pyO3Q|[jVOYrg|2|0]]",
                    "rateType": "NET",
                    "remarks": null,
                    "rooms": [
                        {
                            "numberOfAdults": 2,
                            "numberOfChildren": 0,
                            "roomDescription": "DOUBLE DELUXE CITY VIEW",
                            "sequence": 1
                        }
                    ]
                }
            ]
        }
    ]
}
```