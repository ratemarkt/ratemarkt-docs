## Introduction

Check for single rate availability for a given rate key. This method is intended to provide the most recent availability data for any selected rate. You'd better check for a rate at least once just before proceeding to booking step.

If rate has gone at the time of query, client receives not available error.

## Definition

```
POST https://api.ratemarkt.com/v1/checkrate
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
            <td><code>rateKey</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Unique rate identifier</td>
        </tr>
    </tbody>
</table>

## Example Query Object

```json
{
    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]"
}
```
## Result Object


!!!tip "Result Object Hint"
    While [Check Hotel][1] resource returns a hotel object, this resource also returns exactly the same hotel object except it holds only a single rate object in `rates` field.

    So you may want to reuse the same json parser logic in your client application.

[1]: /api_docs/check_hotel.md

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

!!!note "Holding Single Rate "

    Note that the hotel object contains only a single rate object which is queried by the given rate key.

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
            }
        ]
    }
}
```