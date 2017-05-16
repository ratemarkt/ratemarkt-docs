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
    "clientRef": "172",
    "holder": {
        "email": "eltonjohn@example.org",
        "firstName": "mark",
        "lastName": "john",
        "phone": "+415050000000"
    },
    "occupancy": [
        {
            "occupants": [
                {
                    "age": 35,
                    "firstName": "mark",
                    "lastName": "john",
                    "occupantType": "ADULT"
                },
                {
                    "age": 33,
                    "firstName": "bob",
                    "lastName": "larry",
                    "occupantType": "ADULT"
                }
            ],
            "room": {
                "roomSequence": 1
            }
        }
    ],
    "rateKey": "[Q9k|3|USD|US|[[2|[]]]]_[AJ62Fw|ANMdEg|NET|0|Prabrg|[jVOYrg|2|0]]"
}
```