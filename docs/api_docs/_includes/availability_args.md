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
    <td>Number of adults requested.</td>
</tr>
<tr>
    <td><code>Pax.childrenAges</code></td>
    <td><code>list[integer]</code></td>
    <td>yes</td>
    <td>List of children requested specified by their ages.</td>
</tr>
<tr>
    <td><code>currency</code></td>
    <td><code>string</code></td>
    <td>yes</td>
    <td>Three letter currency code (ISO-4217). **Please read the regarding note below.**</td>
</tr>
<tr>
    <td><code>nationality</code></td>
    <td><code>string</code></td>
    <td>yes</td>
    <td>Two letter country code (ISO 3166-1 alpha-2) for occupants passport nationality.</td>
</tr>