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
    <td><code>Room.sequence</code></td>
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
    <td><code>Booking.boardType</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Board type code of booked rate. Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
</tr>
<tr>
    <td><code>Booking.boardName</code></td>
    <td><code>string</code></td>
    <td>no</td>
    <td>Board type name of booked rate. Refer to <a href="/api_docs/check_rate/">Check Rate</a> documentation for further information.</td>
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