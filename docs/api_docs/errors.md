## Introduction

Ratemarkt API might raise errors in certain cases.

In order to distinguish different return types, Ratemarkt uses conventional HTTP status codes mapped to certain circumstances.

As the HTTP standard stated, all successful queries return HTTP status 20X with the desired result object in JSON format.
For any unsuccessful result, Ratemarkt again tries to map the error to the most relevant HTTP status with an explanatory `Error` object in response body using JSON format.

## Error Object

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
            <td><code>errorCode</code></td>
            <td><code>integer</code></td>
            <td>no</td>
            <td>Predefined error code. Refer to error status reference.</td>
        </tr>
        <tr>
            <td><code>errorMessage</code></td>
            <td><code>string</code></td>
            <td>no</td>
            <td>Explanatory error description</td>
        </tr>
        <tr>
            <td><code>errorCode</code></td>
            <td><code>integer</code></td>
            <td>yes</td>
            <td>More detailed information about the error if available.</td>
        </tr>
    </tbody>
</table>

## Example Error Object

```json
HTTP1/1 410 Gone

{
  "errorCode": 41000,
  "message": "Not available error",
  "detail": "Requested rate is no longer available"
}
```

## Error Reference

<table>
    <colgroup>
        <col width="15%">
        <col width="15%">
        <col width="35%">
        <col width="35%">
    </colgroup>
    <thead>
        <tr>
            <th>HTTP Status Code</th>
            <th>Error Code</th>
            <th>Description</th>
            <th>Resolution</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>400</code></td>
            <td><code>4000</code></td>
            <td>Validation Error</td>
            <td>Check your query object and fix arguments if needed according to relevant <code>Query</code> Object reference</td>
        </tr>
        <tr>
            <td><code>401</code></td>
            <td><code>40100</code></td>
            <td>Authentication Error</td>
            <td>No valid API key provided.</td>
        </tr>
        <tr>
            <td><code>403</code></td>
            <td><code>40300</code></td>
            <td>Authorization Error</td>
            <td>You're not permitted to access to the requested resource. Try with an authorized API key.</td>
        </tr>
        <tr>
            <td><code>404</code></td>
            <td><code>40400</code></td>
            <td>Not Found Error</td>
            <td>Requested resource does not exists. Check your API resource url.</td>
        </tr>
        <tr>
            <td><code>409</code></td>
            <td><code>40900</code></td>
            <td>Illegal State Error</td>
            <td>Some conflict occured. Please consult to detail message for further resolution.</td>
        </tr>
        <tr>
            <td><code>410</code></td>
            <td><code>41000</code></td>
            <td>Not Available Error</td>
            <td>Requested hotel or rate no more available. Try another one or change your date range or pax infromation.</td>
        </tr>
        <tr>
            <td><code>429</code></td>
            <td><code>42900</code></td>
            <td>Rate Limit Exceeded Error</td>
            <td>You have limited number of API access within a certain amount of time. Reduce your number of API access.</td>
        </tr>
        <tr>
            <td><code>500</code></td>
            <td><code>50000</code></td>
            <td>System Error</td>
            <td>Consult to detail message for further resolution.</td>
        </tr>
        <tr>
            <td><code>500</code></td>
            <td><code>51000</code></td>
            <td>Payment Error</td>
            <td>Payment could not be received. Try another payment option or provide another payment data.</td>
        </tr>
        <tr>
            <td><code>503</code></td>
            <td><code>50300</code></td>
            <td>Service Unavailable Error</td>
            <td>Unknown system error occured. Consult to detail message for further resolution.</td>
        </tr>
    </tbody>
</table>
