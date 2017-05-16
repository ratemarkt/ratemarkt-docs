## Introduction

Check single hotel availability for any given date range and pax information. This method is intented to provide cacheless, most recent availability data for requested hotel. If the hotel has no any single rate for the query submitted, client receives not available error.

## Definition

```
POST https://api.ratemarkt.com/v1/checkhotel
```

## Query Object

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
            <td><code>hotelCode</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Unique hotel identifier</td>
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

## Example Query Objects

### Single room query for the specified hotel

```json
{
    "hotelCode": "d31d12",
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "paxes": [{
        "numberOfAdults": 2,
        "childrenAges": []
    }],
    "currency": "USD",
    "nationality": "US"
}
```

### Multi room query for the specified hotel

```json
{
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "currency": "USD",
    "hotelCode": "d31d12",
    "nationality": "US",
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
    ]
}
```

## Result Object

!!!tip "Result Object Hint"
    While [Check Hotels][1] resource returns a list of hotel objects, this resource returns a single hotel object using exactly the same attributes. So you may want to reuse the same json parser logic in your client application.

[1]: /api_docs/check_hotels.md

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
        {! api_docs/_includes/hotel.md !}
    </tbody>
</table>

## Example Result Objects

### Single Room Result Object

```json
{
    "hotel": {
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
}
```