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
        {! api_docs/_includes/availability_args.md !}
    </tbody>
</table>

!!! note "About Optional* Arguments"
    You should provide either `destinationCode` or `hotelCodes` argument to get your availability query work.

!!! warning "Beware of Destination Based Queries"
    Some popular travel destinations contain huge amount of hotels thus your queries may take much longer time then expected.

    We strongly recommend hotel list based queries so that you can perform your queries for only the hotels you interested in and get back corresponding results in much shorter times rather than retrieving a bulk.


## Example Query Object

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
        {! api_docs/_includes/hotel_args.md !}
    </tbody>
</table>

## Example Result Object

```json
{
  "hotels": [
    {
      "hotelCode": "69af45",
      "hotelName": "The Marmara Pera",
      "destinationCode": "c36ca9",
      "destinationName": "istanbul",
      "countryCode": "TR",
      "rates": [
        {
          "rateType": "NET",
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[APS74Q|aa9F|NET|0|NWv9zw|[BugWBw|2|0]]",
          "nonrefundable": true,
          "boardName": "Room Only",
          "rate": 165.83,
          "currency": "USD",
          "rooms": [
            {
              "numberOfAdults": 2,
              "numberOfChildren": 0,
              "roomDescription": "Superior",
              "sequence": 1
            }
          ],
          "cancellationPolicies": [],
          "remarks": null,
          "commission": null,
          "hotelCurrency": null,
          "hotelRate": null
        },
        {
          "rateType": "NET",
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[APS74Q|aa9F|NET|0|NWv9zw|[F108yA|2|0]]",
          "nonrefundable": false,
          "boardName": "Room Only",
          "rate": 189.52,
          "currency": "USD",
          "rooms": [
            {
              "numberOfAdults": 2,
              "numberOfChildren": 0,
              "roomDescription": "Leisure Superior",
              "sequence": 1
            }
          ],
          "cancellationPolicies": [],
          "remarks": null,
          "commission": null,
          "hotelCurrency": null,
          "hotelRate": null
        }
      ]
    },
    {
      "hotelCode": "d31d12",
      "hotelName": "The Marmara Taksim",
      "destinationCode": "c36ca9",
      "destinationName": "istanbul",
      "countryCode": "TR",
      "rates": [
        {
          "rateType": "NET",
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|5pyO3Q|[jVOYrg|2|0]]",
          "nonrefundable": false,
          "boardName": "BED AND BREAKFAST",
          "rate": 689.24,
          "currency": "EUR",
          "rooms": [
            {
              "numberOfAdults": 2,
              "numberOfChildren": 0,
              "roomDescription": "DOUBLE DELUXE CITY VIEW",
              "sequence": 1
            }
          ],
          "cancellationPolicies": [
            {
              "amount": 205.13,
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
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[Jn1lQw|2|0]]",
          "nonrefundable": false,
          "boardName": "ROOM ONLY",
          "rate": 676.97,
          "currency": "EUR",
          "rooms": [
            {
              "numberOfAdults": 2,
              "numberOfChildren": 0,
              "roomDescription": "DOUBLE DELUXE SEA VIEW",
              "sequence": 1
            }
          ],
          "cancellationPolicies": [
            {
              "amount": 201.48,
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
  ]
}
```