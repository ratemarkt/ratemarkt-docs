## Introduction

Check bookings placed between two dates and by their status.

## Definition

```
POST https://api.ratemarkt.com/v1/checkbookings
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
            <td><code>fromDate</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>toDate</code></td>
            <td><code>string</code></td>
            <td>yes</td>
            <td><code>YYYY-MM-DD</code> (ISO 8601) formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>status</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>If not provided all statuses will be retrieved. Possible values
                are <code>CONFIRMED</code>, <code>CANCELLED</code> and
                <code>FAILED</code></td>
        </tr>
    </tbody>
</table>

!!! warning "Duration between dates"
    Duration between <code>fromDate</code> to <code>toDate</code> is restricted to 30 days at maximum.


## Example Query Object

```json
{
    "fromDate": "2018-01-01",
    "toDate": "2018-01-10",
    "status": "CONFIRMED"
}
```

## Result Object

!!!tip "Result Object Hint"
    While [Book Rate][1] resource returns a `Booking` object, this resource also returns exactly the same `Booking` object as list.

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
        <tr>
            <td><code>bookings</code></td>
            <td><code>list[Booking]</code></td>
            <td>no</td>
            <td>List of <code>Booking</code> objects.</td>
        </tr>
        {! api_docs/_includes/booking_args.md !}
    </tbody>
</table>

## Example Result Object

```json
{
    "bookings": [
        {
            "bookingRef": "4087b2",
            "status": "CONFIRMED",
            "total": 709.28,
            "currency": "USD",
            "hotelCode": "11a5e2",
            "checkin": "2018-03-21",
            "checkout": "2018-03-25",
            "holder": {
                "firstName": "John",
                "lastName": "Doe",
                "email": null,
                "phone": null
            },
            "creationDate": "2018-01-09T23:59:43.088134Z",
            "cancellationPolicies": [
                {
                    "amount": 709.28,
                    "fromDate": "2018-03-17T00:00:00Z"
                }
            ],
            "nonrefundable": false,
            "clientRef": "CRL-QZVIEFLSNRHHM4L5",
            "rateType": "NET",
            "occupancies": [
                {
                    "occupants": [
                        {
                            "occupantType": "ADULT",
                            "age": 30,
                            "firstName": "John",
                            "lastName": "Doe"
                        }
                    ],
                    "room": {
                        "numberOfAdults": 1,
                        "childrenAges": [],
                        "roomDescription": "Single",
                        "sequence": 1
                    }
                }
            ],
            "balance": 709.28,
            "boardType": "RO",
            "boardName": "Room Only",
            "rateKey": "[RMs|4|EUR|ca|[[1|[]]]]~[AOz-8w|EaXi|NET|0|RO|[Z3dCAQ|1|[]]]",
            "hotelName": "B Ocean Resort",
            "destinationCode": "10c967",
            "destinationName": "Fort Lauderdale",
            "countryCode": "US",
            "cancellationCost": null,
            "commission": null,
            "hotelRate": null,
            "hotelCurrency": null,
            "specialRequest": "",
            "remarks": "",
            "meta": null
        },
        {
            "bookingRef": "abbca9",
            "status": "FAILED",
            "total": 1536.35,
            "currency": "USD",
            "hotelCode": "10d1bd",
            "checkin": "2018-08-04",
            "checkout": "2018-08-09",
            "holder": {
                "firstName": "Mary",
                "lastName": "Moyes",
                "email": null,
                "phone": null
            },
            "creationDate": "2018-01-09T21:29:08.537106Z",
            "cancellationPolicies": [
                {
                    "amount": 1536.35,
                    "fromDate": "2018-01-08T21:29:08.35Z"
                }
            ],
            "nonrefundable": true,
            "clientRef": "CRL-UNONHKXF4IGSAHYL",
            "rateType": "NET",
            "occupancies": [
                {
                    "occupants": [
                        {
                            "occupantType": "ADULT",
                            "age": 30,
                            "firstName": "Diana",
                            "lastName": "Bauke"
                        },
                        {
                            "occupantType": "ADULT",
                            "age": 30,
                            "firstName": "Mary",
                            "lastName": "Moyes"
                        }
                    ],
                    "room": {
                        "numberOfAdults": 2,
                        "childrenAges": [],
                        "roomDescription": "Double",
                        "sequence": 1
                    }
                }
            ],
            "balance": 1536.35,
            "boardType": "RO",
            "boardName": "Room Only",
            "rateKey": "[RVM|5|EUR|us|[[2|[]]]]~[AOz-8w|ENG9|NET|1|RO|[98iC/A|2|[]]]",
            "hotelName": "Fraser Suites Edinburgh",
            "destinationCode": "10b373",
            "destinationName": "Edinburgh",
            "countryCode": "GB",
            "cancellationCost": null,
            "commission": null,
            "hotelRate": null,
            "hotelCurrency": null,
            "specialRequest": null,
            "remarks": "<b>Fees</b> . The following fees and deposits are charged by the property at time of service, check-in, or check-out.   Fee for continental breakfast: GBP 10.00 per person (approximately)                              The above list may not be comprehensive. Fees and deposits may not include tax and are subject to change. <b>Mandatory Fees and Taxes</b> . You'll be asked to pay the following charges at the property: Deposit: GBP 50 per stay We have included all charges provided to us by the property. However, charges can vary, for example, based on length of stay or the room you book. Extra-person charges may apply and vary depending on property policy. . Government-issued photo identification and a credit card or cash deposit are required at check-in for incidental charges. . Special requests are subject to availability upon check-in and may incur additional charges. Special requests cannot be guaranteed. . 1 Double Bed. 248 sq feet (23 sq meters). . <b>Internet</b> - Free WiFi .  <b>Entertainment</b> - LCD television, digital channels, and iPod dock. <b>Food & Drink</b> - Kitchenette with refrigerator, microwave, dishwasher, and cookware/dishware. <b>Sleep</b> - Egyptian cotton linens and a pillow menu . <b>Bathroom</b> - Private bathroom, designer toiletries, and a shower/tub combination with a rainfall showerhead. <b>Practical</b> - Laptop-compatible safe, iron/ironing board, and desk. <b>Comfort</b> - Daily housekeeping. Smoking/Non Smoking. &nbsp;",
            "meta": null
        },
        {
            "bookingRef": "3759a3",
            "status": "CONFIRMED",
            "total": 389.69,
            "currency": "USD",
            "hotelCode": "12052f",
            "checkin": "2018-01-15",
            "checkout": "2018-01-19",
            "holder": {
                "firstName": "Dany",
                "lastName": "Pryde",
                "email": null,
                "phone": null
            },
            "creationDate": "2018-01-09T21:14:19.298893Z",
            "cancellationPolicies": [
                {
                    "amount": 389.69,
                    "fromDate": "2018-01-11T00:00:00Z"
                }
            ],
            "nonrefundable": false,
            "clientRef": "CRL-DWKRYZLPFFBZTRUM",
            "rateType": "NET",
            "occupancies": [
                {
                    "occupants": [
                        {
                            "occupantType": "ADULT",
                            "age": 30,
                            "firstName": "Dany",
                            "lastName": "Pryde a"
                        },
                        {
                            "occupantType": "ADULT",
                            "age": 30,
                            "firstName": "Dany",
                            "lastName": "Pryde"
                        }
                    ],
                    "room": {
                        "numberOfAdults": 2,
                        "childrenAges": [],
                        "roomDescription": "Double",
                        "sequence": 1
                    }
                }
            ],
            "balance": 389.69,
            "boardType": "RO",
            "boardName": "Room Only",
            "rateKey": "[RIo|4|USD|us|[[2|[]]]]~[AOz-8w|EgUv|NET|0|RO|[98iC/A|2|[]]]",
            "hotelName": "Hilton Garden Inn Washington DC/US Capitol",
            "destinationCode": "118f52",
            "destinationName": "Washington",
            "countryCode": "US",
            "cancellationCost": null,
            "commission": null,
            "hotelRate": null,
            "hotelCurrency": null,
            "specialRequest": "",
            "remarks": "",
            "meta": null
        }
    ]
}
```
