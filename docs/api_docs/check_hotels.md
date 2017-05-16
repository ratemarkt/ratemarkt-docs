# Check Hotels

## Introduction

You can perform an overall availability query for hotels by using either a destination or a list of selected hotels within the selected arrival and departure dates for a number of paxes.

### Definition

```
POST https://api.ratemarkt.com/v1/checkhotels
```

### Arguments

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
            <td><code>String</code></td>
            <td>optional*</td>
            <td>Destination code.</td>
        </tr>
        <tr>
            <td><code>hotelCodes</code></td>
            <td><code>List[String]</code></td>
            <td>optional*</td>
            <td>List of hotel codes.</td>
        </tr>
        <tr>
            <td><code>checkin</code></td>
            <td><code>String</code></td>
            <td>yes</td>
            <td>ISO 8601 formatted date string. Eg. 2017-11-12</td>
        </tr>
        <tr>
            <td><code>checkout</code></td>
            <td><code>String</code></td>
            <td>yes</td>
            <td>ISO 8601 formatted date string. Eg. 2017-11-15</td>
        </tr>
        <tr>
            <td><code>paxes</code></td>
            <td><code>List[Pax]</code></td>
            <td>yes</td>
            <td>List of pax objects. Each pax object corresponds to a room. Multi room queries need more than one pax object.</td>
        </tr>
        <tr>
            <td><code>Pax.numberOfAdults</code></td>
            <td><code>Integer</code></td>
            <td>yes</td>
            <td>Number of adults for the specified room.</td>
        </tr>
        <tr>
            <td><code>Pax.childrenAges</code></td>
            <td><code>List[Integer]</code></td>
            <td>yes</td>
            <td>List of children ages for the specified room.</td>
        </tr>
        <tr>
            <td><code>currency</code></td>
            <td><code>String</code></td>
            <td>yes</td>
            <td>Three letter currency code (ISO-4217). Only USD, EUR and GBP currencies are supported at the moment.</td>
        </tr>
        <tr>
            <td><code>nationality</code></td>
            <td><code>String</code></td>
            <td>yes</td>
            <td>Two letter country code (ISO 3166-1 alpha-2) for occupants passport nationality.</td>
        </tr>
    </tbody>
</table>

!!! warning "Optional* Arguments"
    You should provide either one of `destinationCode` argument or `hotelCodes` argument to get your availability query work.

## Example Requests

### Single room query for certain hotels

```terminal
$ curl -X POST https://api.ratemarkt.com/v1/checkhotels -d'{
    "hotelCodes": ["d31d12", "69af45", "984767"],
    "checkin": "2017-07-22",
    "checkout": "2017-07-25",
    "paxes": [{
        "numberOfAdults": 2,
        "childrenAges": []
    }],
    "currency": "USD",
    "nationality": "US"
}'
```

### Multi room query for a certain destination

```terminal
$ curl -X POST https://api.ratemarkt.com/v1/checkhotels -d'{
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
}'
```