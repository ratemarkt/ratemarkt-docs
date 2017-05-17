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
            <td>Holder' s first name</td>
        </tr>
        <tr>
            <td><code>Holder.lastName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Holder' s last name</td>
        </tr>
        <tr>
            <td><code>Holder.email</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Holder' s email address</td>
        </tr>
        <tr>
            <td><code>Holder.phone</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Holder' s phone number</td>
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
                List of Occupant objects.<br/><br/>
                The number of occupants can not be more the number of pax information of the matching room object.
                Each occupant should be declared by their name and age information.
            </td>
        </tr>
        <tr>
            <td><code>Occupant.firstName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Occupant' s first name</td>
        </tr>
        <tr>
            <td><code>Occupant.lastName</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Occupant' s last name</td>
        </tr>
        <tr>
            <td><code>Occupant.age</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Occupant' s age</td>
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
            <td><code>Room.roomSequence</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Room's sequence number. It is required for matching occupancy information with a room</td>
        </tr>
    </tbody>
</table>

## Example Query Object

### Book a single room

```json
{
  "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
  "clientRef": "200",
  "holder": {
    "email": "johndoe@example.org",
    "firstName": "john",
    "lastName": "doe",
    "phone": "+415050000000"
  },
  "occupancy": [
    {
      "room": {
        "roomSequence": 1
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
        <col width="20%">
        <col width="20%">
        <col width="40%">
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
            <td><code>status</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>
                Flag indicating the current status of the booking. Available values are:
                <ul>
                    <li><code>IDLE</code>: Booking record created but not even processed.</li>
                    <li><code>CONFIRMED</code>: Booking confirmed and payment processed successfully.</li>
                    <li><code>FAILED</code>: Booking failed because of an error.</li>
                    <li><code>CANCELED</code>: Booking cancelled successfully.</li>
                    <li><code>CANCELLATION_FAILED</code>: Cancellation attempt failed because of an error.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><code>bookingRef</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique booking identifier</td>
        </tr>
        <tr>
            <td><code>clientRef</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique booking identifier issued by the client</td>
        </tr>
        <tr>
            <td><code>rateKey</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique rate identifier</td>
        </tr>
    </tbody>
</table>

## Example Result Object

```json
{
  "booking": {
    "status": "CONFIRMED",
    "bookingRef": "316591",
    "clientRef": "qwerty123456",
    "hotel": {
      "hotelCode": "d31d12",
      "hotelName": "The Marmara Taksim",
      "destinationCode": "c36ca9",
      "destinationName": "istanbul",
      "countryCode": "TR",
      "rates": [
        {
          "rateType": "NET",
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
          "nonrefundable": false,
          "boardName": "ROOM ONLY",
          "rate": 493.18,
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
              "amount": 146.78,
              "fromDate": "2017-07-19T23:59:00+03:00"
            }
          ],
          "remarks": "CONTRACT VALID FOR JUNIOR ROOM TYPES .  Check-in hour 15:00 - .",
          "commission": null,
          "hotelCurrency": null,
          "hotelRate": null
        }
      ]
    },
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "nationality": "us",
    "holder": {
      "firstName": "john",
      "lastName": "doe",
      "email": "johndoe@example.org",
      "phone": "+415050000000"
    },
    "occupancy": [
      {
        "occupants": [
          {
            "occupantType": "ADULT",
            "age": 35,
            "firstName": "john",
            "lastName": "doe"
          },
          {
            "occupantType": "ADULT",
            "age": 33,
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
    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
    "rateType": "NET",
    "boardName": "ROOM ONLY",
    "nonrefundable": false,
    "cancellationPolicies": [
      {
        "amount": 146.78,
        "fromDate": "2017-07-19T23:59:00+03:00"
      }
    ],
    "total": 493.18,
    "currency": "EUR",
    "balance": 440.34,
    "cancellationCost": 0,
    "commission": null,
    "hotelRate": null,
    "hotelCurrency": null,
    "specialRequest": null,
    "remarks": "Check-in hour 15:00 – . . CONTRACT VALID FOR JUNIOR ROOM TYPES"
  }
}
```