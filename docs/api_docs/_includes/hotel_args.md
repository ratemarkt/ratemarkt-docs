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
    <td>Hotel name</td>
</tr>
<tr>
    <td><code>Hotel.destinationCode</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Unique destination identifier</td>
</tr>
<tr>
    <td><code>Hotel.destinationName</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Destination name</td>
</tr>
<tr>
    <td><code>Hotel.countryCode</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Two letter country code (ISO 3166-1 alpha-2)</td>
</tr>
<tr>
    <td><code>Hotel.rates</code></td>
    <td><code>list[Rate]</code></td>
    <td>no</td>
    <td>List of <code>Rate</code> objects. Each rate corresponds to a hotel room combined with a service level which means a bookable product with a price for each hotel.</td>
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
    <td><code>Rate.boardType</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Board type code of the rate. Possible value are<br/>
        <ul>
            <li><code>RO</code>: <span>Room Only</span></li>
            <li><code>BB</code>: <span>Bed And Breakfast</span></li>
            <li><code>HB</code>: <span>Half Board</span></li>
            <li><code>FB</code>: <span>Full Board</span></li>
            <li><code>AI</code>: <span>All Inclusive</span></li>
        </ul>
    </td>
</tr>
<tr>
    <td><code>Rate.boardName</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Board type name of the rate. See <code>Rate.boardType</code> field for possible values.</td>
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
        List of <code>Room</code> objects.
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
    <td><code>Room.sequence</code></td>
    <td><code>integer</code></td>
    <td>no</td>
    <td>Room sequence identifier which is useful at the time of booking in order to specify which occupant set will be matched with which room.</td>
</tr>
<tr>
    <td><code>Rate.cancellationPolicies</code></td>
    <td><code>list[CancellationPolicy]</code></td>
    <td>yes</td>
    <td>
        List of <code>CancellationPolicy</code> objects.<br/><br/>
        Cancellation policies indicates the amount of penalty charged and deducted from the total refund amount of the booking at the time of cancellation performed after the specified date and time.<br/><br/>
        Please note that, the value can be <code>null</code> since not all the suppliers provide this data on <code>Check Hotels</code> step. In these cases, you should use <code>Check Rate</code> end point accordingly to able to retrieve cancellation policies.
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