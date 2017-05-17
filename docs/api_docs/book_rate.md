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
            <td><code>Room.roomSequence</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>Room's sequence number. It is required for matching occupancy information with a room</td>
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
            <td><code>Result.booking</code></td>
            <td><code>object[Booking]</code></td>
            <td>no</td>
            <td>Booking object</td>
        </tr>
        <tr>
            <td><code>Booking.status</code></td>
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
            <td><code>Booking.bookingRef</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique booking identifier</td>
        </tr>
        <tr>
            <td><code>Booking.clientRef</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique booking identifier issued by the client</td>
        </tr>
        <tr>
            <td><code>Booking.rateKey</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique rate identifier</td>
        </tr>
        <tr>
            <td><code>Booking.hotelCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique hotel identifier</td>
        </tr>
        <tr>
            <td><code>Booking.hotelName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Hotel name</td>
        </tr>
        <tr>
            <td><code>Booking.destinationCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique destination identifier</td>
        </tr>
        <tr>
            <td><code>Booking.destinationName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Destination name</td>
        </tr>
        <tr>
            <td><code>Booking.countryCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Two letter country code (ISO 3166-1 alpha-2)</td>
        </tr>
        <tr>
            <td><code>Booking.checkin</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>Booking.checkout</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>Booking.holder</code></td>
            <td><code>object[Holder]</code></td>
            <td>no</td>
            <td>Holder object contains information who places the booking</td>
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
            <td><code>Booking.occupancies</code></td>
            <td><code>list[Occupancy]</code></td>
            <td>no</td>
            <td>Occupancy object contains information of individual occupants who will accomodate in the specified room.</td>
        </tr>
        <tr>
            <td><code>Occupancy.occupants</code></td>
            <td><code>list[Occupant]</code></td>
            <td>no</td>
            <td>List of <code>Occupant</code> objects contains information about personal occupant information.</td>
        </tr>
        <tr>
            <td><code>Occupant.occupantType</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Occupant type. Value can be either <code>ADULT</code> or <code>CHILD</code></td>
        </tr>
        <tr>
            <td><code>Occupant.firstName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Occupant's first name</td>
        </tr>
        <tr>
            <td><code>Occupant.lastName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Occupant's last name</td>
        </tr>
        <tr>
            <td><code>Occupant.age</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Occupant's age</td>
        </tr>
        <tr>
            <td><code>room</code></td>
            <td><code>object[Room]</code></td>
            <td>no</td>
            <td>Room object</td>
        </tr>
        <tr>
            <td><code>Room.numberOfAdults</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Number of adults can fit into the room</td>
        </tr>
        <tr>
            <td><code>Room.childrenAges</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Children with specified ages can be accepted for this room.</td>
        </tr>
        <tr>
            <td><code>Room.roomDescription</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Room description describing the type of room.</td>
        </tr>
        <tr>
            <td><code>Room.roomSequence</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Identifies the selected room for specified occupants.</td>
        </tr>
        <tr>
            <td><code>Booking.creationDate</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Offset date time string in <code>YYYY-MM-DDThh:mmTZD</code> (ISO 8601) format indicating when the booking made.</td>
        </tr>
        <tr>
            <td><code>Booking.total</code></td>
            <td><code>decimal</code></td>
            <td>no</td>
            <td>Total amount of booked rate in specified currency in <code>Booking.currency</code> field</td>
        </tr>
        <tr>
            <td><code>Booking.currency</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Two letter country code (ISO 3166-1 alpha-2) of the amount for booked rate.</td>
        </tr>
        <tr>
            <td><code>Booking.cancellationCost</code></td>
            <td><code>decimal</code></td>
            <td>yes</td>
            <td>Charged penalty amount when the booking is cancelled. If no penalty charged, this value should be <code>0.00</code></td>
        </tr>
        <tr>
            <td><code>Booking.balance</code></td>
            <td><code>decimal</code></td>
            <td>no</td>
            <td>
                if booking cancelled and any penalty applied, this field indicates the final amount after the penalty amount deducted from total amount.
                If booking is not cancelled this field should be equal to <code>Booking.total</code> amount.
            </td>
        </tr>
        <tr>
            <td><code>Booking.specialRequest</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Special requests asked by the holder</td>
        </tr>
        <tr>
            <td><code>Booking.rateKey</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique identifier of the booked rate. Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.rateType</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Type of booked rate. Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.boardName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Boarding type of booked rate. Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.nonrefundable</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Flag indicating wheter the booking is refundable or not.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.cancellationPolicies</code></td>
            <td><code>list[CancellationPolicy]</code></td>
            <td>no</td>
            <td>List of <code>CancellationPolicy</code> objects.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.commission</code></td>
            <td><code>decimal</code></td>
            <td>yes</td>
            <td>Amount of comission specified for commissionable rates.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.hotelRate</code></td>
            <td><code>decimal</code></td>
            <td>yes</td>
            <td>Total amount of booking should be payed at hotel.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.hotelCurrency</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Currency value for <code>Booking.hotelRate</code>.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
        <tr>
            <td><code>Booking.remarks</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Comments from hotelier related to your booking.<br/><br/>Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
        </tr>
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
    "boardName": "ROOM ONLY",
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
