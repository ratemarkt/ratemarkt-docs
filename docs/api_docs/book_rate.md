## Introduction

Perform booking by providing occupancy and payment information for any selected rate specified by the rate key.

## Definition

```
POST https://api.ratemarkt.com/v1/bookrate
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
            <td><code>clientRef</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Unique transaction identifier defined by client.<br/><br/>It is required for avoiding dupe bookings or querying missing bookings</td>
        </tr>
        <tr>
            <td><code>holder</code></td>
            <td><code>object[Holder]</code></td>
            <td>yes</td>
            <td>Holder information who places the booking</td>
        </tr>
        <tr>
            <td><code>Holder.firstName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Holder's first name</td>
        </tr>
        <tr>
            <td><code>Holder.lastName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Holder's last name</td>
        </tr>
        <tr>
            <td><code>Holder.email</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Holder's email address</td>
        </tr>
        <tr>
            <td><code>Holder.phone</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Holder's phone number</td>
        </tr>
        <tr>
            <td><code>occupancies</code></td>
            <td><code>list[Occupancy]</code></td>
            <td>yes</td>
            <td>Information about the occupants those will accomodate at the booked rooms.</td>
        </tr>
        <tr>
            <td><code>Occupancy.occupants</code></td>
            <td><code>list[Occupant]</code></td>
            <td>yes</td>
            <td>
                List of <code>Occupant</code> objects.<br/><br/>
                The number of occupants can not be more the number of pax information of the matching room object.
                Each occupant should be declared by their name and age information.
            </td>
        </tr>
        <tr>
            <td><code>Occupant.firstName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Occupant's first name</td>
        </tr>
        <tr>
            <td><code>Occupant.lastName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Occupant's last name</td>
        </tr>
        <tr>
            <td><code>Occupant.age</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Occupant's age</td>
        </tr>
        <tr>
            <td><code>Occupant.occupantType</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>
                Type of occupant. <br/><br/>
                It can either be the value of <code>ADULT</code> or <code>CHILD</code>.
            </td>
        </tr>
        <tr>
            <td><code>Occupancy.room</code></td>
            <td><code>object[Room]</code></td>
            <td>yes</td>
            <td>Room object containing the only value of its sequence number</td>
        </tr>
        <tr>
            <td><code>Room.sequence</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Room's sequence number. It is required for matching occupancy information with a room</td>
        </tr>
        <tr>
            <td><code>creditCard</code></td>
            <td><code>object[CreditCard]</code></td>
            <td>no</td>
            <td>Credit card information used for either for <code>DIRECT</code> type rates or online payment required rates.</td>
        </tr>
        <tr>
            <td><code>CreditCard.firstName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Card holder's first name</td>
        </tr>
        <tr>
            <td><code>CreditCard.lastName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Card holder's last name</td>
        </tr>
        <tr>
            <td><code>CreditCard.number</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>16 digit credit card number</td>
        </tr>
        <tr>
            <td><code>CreditCard.year</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>4 digit year identifier. E.g 2025</td>
        </tr>
        <tr>
            <td><code>CreditCard.month</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>2 digit year identifier. E.g 12</td>
        </tr>
        <tr>
            <td><code>CreditCard.cvv</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Credit card verification number</td>
        </tr>
        <tr>
            <td><code>specialRequest</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Special requests asked by the holder</td>
        </tr>
    </tbody>
</table>

## Example Query Object

```json
{
  "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
  "clientRef": "qwerty123456",
  "holder": {
    "email": "johndoe@example.org",
    "firstName": "john",
    "lastName": "doe",
    "phone": "+415050000000"
  },
  "creditCard": {
    "firstName": "John",
    "lastName": "Doe",
    "number": "4111111111111111",
    "year": "2022",
    "month": "12",
    "cvv": "000"
  },
  "occupancy": [
    {
      "room": {
        "sequence": 1
      },
      "occupants": [
        {
          "firstName": "john",
          "lastName": "doe",
          "occupantType": "ADULT",
          "age": 35
        },
        {
          "firstName": "alice",
          "lastName": "wonder",
          "occupantType": "ADULT",
          "age": 33
        }
      ]
    }
  ]
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
        {! api_docs/_includes/booking_args.md !}
    </tbody>
</table>

## Example Result Object

```json
{
  "booking": {
    "status": "CONFIRMED",
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
    "boardType": "RO",
    "boardName": "Room Only",
    "cancellationPolicies": [
      {
        "amount": 174.13,
        "fromDate": "2017-07-19T23:59:00+03:00"
      }
    ],
    "total": 585.08,
    "currency": "EUR",
    "balance": 522.39,
    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
    "hotelName": "The Marmara Taksim",
    "destinationCode": "c36ca9",
    "destinationName": "istanbul",
    "countryCode": "TR",
    "nonrefundable": false,
    "cancellationCost": 0,
    "commission": null,
    "hotelRate": null,
    "hotelCurrency": null,
    "specialRequest": null,
    "remarks": "Check-in hour 15:00"
  }
}
```
