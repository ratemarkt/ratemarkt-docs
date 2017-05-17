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
        {! api_docs/_includes/availability_args.md !}
    </tbody>
</table>

## Example Query Objects

### Single room query for the specified hotel

```json
{
  "hotelCode": "d31d12",
  "checkin": "2017-07-22",
  "checkout": "2017-07-25",
  "paxes": [
    {
      "numberOfAdults": 2,
      "childrenAges": []
    }
  ],
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
    While [Check Hotels][1] resource returns a list of <code>Hotel</code> objects, this resource returns a single hotel object using exactly the same attributes. So you may want to reuse the same json parser logic in your client application.

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
        {! api_docs/_includes/hotel_args.md !}
    </tbody>
</table>

## Example Result Objects

### Single Room Result Object

```json
{
  "hotel": {
    "hotelCode": "d31d12",
    "hotelName": "The Marmara Taksim",
    "destinationCode": "c36ca9",
    "destinationName": "istanbul",
    "countryCode": "TR",
    "rates": [
      {
        "rateType": "NET",
        "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[pNRg1w|2|0]]",
        "nonrefundable": false,
        "boardName": "ROOM ONLY",
        "rate": 555.21,
        "currency": "EUR",
        "rooms": [
          {
            "numberOfAdults": 2,
            "numberOfChildren": 0,
            "roomDescription": "DOUBLE CORNER CITY VIEW",
            "sequence": 1
          }
        ],
        "cancellationPolicies": [
          {
            "amount": 165.24,
            "fromDate": "2017-07-19T23:59:00+03:00"
          }
        ],
        "remarks": null,
        "commission": null,
        "hotelCurrency": null,
        "hotelRate": null
      },
      {
        "rateType": "NET",
        "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|5pyO3Q|[pNRg1w|2|0]]",
        "nonrefundable": false,
        "boardName": "BED AND BREAKFAST",
        "rate": 631.78,
        "currency": "EUR",
        "rooms": [
          {
            "numberOfAdults": 2,
            "numberOfChildren": 0,
            "roomDescription": "DOUBLE CORNER CITY VIEW",
            "sequence": 1
          }
        ],
        "cancellationPolicies": [
          {
            "amount": 188.03,
            "fromDate": "2017-07-19T23:59:00+03:00"
          }
        ],
        "remarks": null,
        "commission": null,
        "hotelCurrency": null,
        "hotelRate": null
      }
    ]
  }
}
```