## Introduction

Cancels the selected booking by providing either booking reference or client reference.

If the cancellation complies to any cancellation policy rule, the specified amount of penalty will be deducted from the total refund amount of booking.

If the booking already is a nonredundable one, nothing will be refunded.

## Definition

```
POST https://api.ratemarkt.com/v1/cancelbooking
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
            <td><code>bookingRef</code></td>
            <td><code>string</code></td>
            <td>optional*</td>
            <td>Unique booking identifier</td>
        </tr>
        <tr>
            <td><code>clientRef</code></td>
            <td><code>string</code></td>
            <td>optional*</td>
            <td>Unique booking identifier defined by client</td>
        </tr>
    </tbody>
</table>

!!! note "About Optional* Arguments"
    You should provide either `bookingRef` or `clientRef` argument to get your query work.

## Example Query Object

```json
{
  "bookingRef": "7616be"
}
```

## Result Object

!!!tip "Result Object Hint"
    While [Book Rate][1] resource returns a `Booking` object, this resource also returns exactly the same `Booking` object.

    So you may want to reuse the same json parser logic in your client application.

[1]: /api_docs/book_rate.md

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
        {! api_docs/_includes/booking_args.md !}
    </tbody>
</table>

## Example Result Object

```json
{
  "booking": {
    "status": "CANCELLED",
    "bookingRef": "55cda9",
    "clientRef": "qwerty123456",
    "hotelCode": "d31d12",
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "holder": {
      "firstName": "john",
      "lastName": "doe",
      "email": "johndoe@example.org",
      "phone": "+415000000"
    },
    "occupancies": [
      {
        "occupants": [
          {
            "occupantType": "ADULT",
            "age": null,
            "firstName": "john",
            "lastName": "doe"
          },
          {
            "occupantType": "ADULT",
            "age": null,
            "firstName": "alice",
            "lastName": "wonder"
          }
        ],
        "room": {
          "numberOfAdults": 2,
          "numberOfChildren": 0,
          "roomDescription": "DOUBLE DELUXE CITY VIEW",
          "sequence": 1
        }
      }
    ],
    "creationDate": "2017-05-17T12:00:00Z",
    "rateType": "NET",
    "boardName": "ROOM ONLY",
    "cancellationPolicies": [
      {
        "amount": 174.13,
        "fromDate": "2017-07-19T23:59:00+03:00"
      }
    ],
    "total": 585.08,
    "currency": "EUR",
    "balance": 410.95,
    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
    "hotelName": "The Marmara Taksim",
    "destinationCode": "c36ca9",
    "destinationName": "istanbul",
    "countryCode": "TR",
    "nonrefundable": false,
    "cancellationCost": 174.13,
    "commission": null,
    "hotelRate": null,
    "hotelCurrency": null,
    "specialRequest": null,
    "remarks": "Check-in hour 15:00"
  }
}
```
