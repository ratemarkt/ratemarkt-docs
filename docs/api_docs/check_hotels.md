# Check Hotels

## Introduction

You can perform an overall availability query for hotels by using either a destination or a list of selected hotels within the selected arrival and departure dates for a number of paxes.

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

!!! warning "About Optional* Arguments"
    You should provide either one of `destinationCode` argument or `hotelCodes` argument to get your availability query work.

!!! danger "Beware Destination Based Queries"
    Some popular travel destinations contain huge amount of hotels thus your queries may take much longer time then expected.

    We strongly recommend hotel list based queries so that you can perform your queries for only the hotels you interested in and get back corresponding results in much shorter times rather than receiving a bulk.


## Example Query Objects

### Single room query for certain hotels

```json
{
    "hotelCodes": ["d31d12", "69af45", "984767"],
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

### Multi room query for a certain destination

```json
{
    "destinationCode": "d31d12",
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "paxes": [{
        "numberOfAdults": 1,
        "childrenAges": []
    }, {
        "numberOfAdults": 2,
        "childrenAges": [3, 5]
    }],
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
        <tr>
            <td><code>Hotel.hotelCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique hotel identifier</td>
        </tr>
        <tr>
            <td><code>Hotel.hotelName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Name of the hotel</td>
        </tr>
        <tr>
            <td><code>Hotel.destinationCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique destination identifier of the hotel</td>
        </tr>
        <tr>
            <td><code>Hotel.destinationName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Name of the destination</td>
        </tr>
        <tr>
            <td><code>Hotel.countryCode</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Two letter country code (ISO 3166-1 alpha-2) of the hotel</td>
        </tr>
        <tr>
            <td><code>Hotel.rates</code></td>
            <td><code>list[Rate]</code></td>
            <td>no</td>
            <td>List of rate objects. Each rate corresponds to a hotel room combined with a service level which means a bookable product with a price for each hotel.</td>
        </tr>
        <tr>
            <td><code>Rate.rateType</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Type of the rate. There are three types:
                <ul>
                    <li><code>NET</code>: This type of rate can be selled by applying any margin on top of it.</li>
                    <li><code>SALE</code>: Commissionable rate which should be selled exactly at the given rate.</li>
                    <li><code>DIRECT</code>: Commissionable rate which the amount is payed directly to the hotelier by the occupants at the time of arrival. </li>
                </ul>
                For commissionable rates, the amount of commission for the merchant is denoted at <code>Rate.commission</code> field.
            </td>
        </tr>
        <tr>
            <td><code>Rate.rateKey</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Unique identifier for each rate.</td>
        </tr>
        <tr>
            <td><code>Rate.nonrefundable</code></td>
            <td><code>boolean</code></td>
            <td>yes</td>
            <td>
                Flag denoting whether the rate is refundable or not. It means that if any nonrefundable rate is booked, cancellation of that booking won't be refunded in any cases.<br/><br/>
                Value can be <code>null</code> in some cases so please refer to the corresponding <code>Rate.cancellation_policies</code> field for that rate for money refunding policy at the time of cancellation.
            </td>
        </tr>
        <tr>
            <td><code>Rate.boardName</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Boarding type of the rate. It can be any arbitrary identifier depending on corresponding hotel's boarding policy.</td>
        </tr>
        <tr>
            <td><code>Rate.rate</code></td>
            <td><code>decimal</code></td>
            <td>no</td>
            <td>Total amount of the rate at given currency specified in <code>Rate.currency</code> field.</td>
        </tr>
        <tr>
            <td><code>Rate.currency</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Three letter currency code (ISO-4217) of the total amount for the rate specified in <code>Rate.rate</code> field</td>
        </tr>
        <tr>
            <td><code>Rate.rooms</code></td>
            <td><code>list[Room]</code></td>
            <td>no</td>
            <td>
                List of room objects.<br/><br/>
                <strong>Please not that the number of rooms are not guaranteed to match the number of pax objects specified in <u>multi-pax</u> queries.</strong><br/><br/>
                Some rates might return single room separately to conform the number of paxes specified in the query while some might return multi rooms per rate.<br/></br/>
                <strong>If you choose separate rates for your multi pax query you should perform individual bookings for each of those rates separately.</strong>
            </td>
        </tr>
        <tr>
            <td><code>Room.numberOfAdults</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Maximum number of adults can fit into this room</td>
        </tr>
        <tr>
            <td><code>Room.childrenAges</code></td>
            <td><code>list[integer]</code></td>
            <td>no</td>
            <td>Children with specified ages can be accepted for this room.</td>
        </tr>
        <tr>
            <td><code>Room.roomDescription</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Any arbitrary description for this room which the hotelier specified.</td>
        </tr>
        <tr>
            <td><code>Room.roomSequence</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Room sequence identifier which is useful at the time of booking in order to specify which occupant set will be matched with which room.</td>
        </tr>
        <tr>
            <td><code>Rate.cancellationPolicies</code></td>
            <td><code>list[CancellationPolicy]</code></td>
            <td>no</td>
            <td>
                List of CancellationPolicy objects.<br/><br/>
                Cancellation policies indicates the amount of penalty charged and deducted from the total refund amount of the booking at the time of cancellation performed after the specified date and time.
            </td>
        </tr>
        <tr>
            <td><code>CancellationPolicy.amount</code></td>
            <td><code>decimal</code></td>
            <td>no</td>
            <td>Penalty amount in rate's currency specified in <code>Rate.currency</code> field</td>
        </tr>
        <tr>
            <td><code>CancellationPolicy.fromDate</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Offset date time string in <code>YYYY-MM-DDThh:mmTZD</code> (ISO 8601) format indicating from when the polciy applied.</td>
        </tr>
        <tr>
            <td><code>Rate.remarks</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Any comments, warnings or policies applied by the hotel displayed here if available.</td>
        </tr>
        <tr>
            <td><code>Rate.commission</code></td>
            <td><code>decimal</code></td>
            <td>yes</td>
            <td>Amount of comission specified for commissionable rates.</td>
        </tr>
        <tr>
            <td><code>Rate.hotelRate</code></td>
            <td><code>decimal</code></td>
            <td>yes</td>
            <td>
                Total amount of rate in hotelier's currency specified in <code>hotelCurrency</code> field which will be payed to the hotelier by the occupants at the time of arrival.
                This field should not be <code>null</code> when the <code>Rate.rateType</code> is <code>DIRECT</code>
            </td>
        </tr>
        <tr>
            <td><code>Rate.hotelCurrency</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td>Three letter currency code (ISO-4217) of the total amount for the hotel rate specified in <code>Rate.hotelRate</code> field</td>
        </tr>
    </tbody>
</table>

## Example Result Object

### Single Room Result Object

```json
{
  "hotels": [
    {
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
          "remarks": null,
          "commission": null,
          "hotelCurrency": null,
          "hotelRate": null
        },
        {
          "rateType": "NET",
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]",
          "nonrefundable": false,
          "boardName": "ROOM ONLY",
          "rate": 585.08,
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
              "amount": 174.13,
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
          "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|5pyO3Q|[jVOYrg|2|0]]",
          "nonrefundable": false,
          "boardName": "BED AND BREAKFAST",
          "rate": 591.19,
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
              "amount": 175.95,
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