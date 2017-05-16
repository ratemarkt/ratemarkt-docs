# Getting Started

Welcome to Ratemarkt Client API :heart:

## Introduction

Ratemarkt Client API is a quite intuitive HTTP based JSON API designed to make it very easy to get integrated with Ratemarkt as a client.

It just requires a single API key put in HTTP headers to get authenticated and introduces only a few resources in total to get all the job done with ease.

## Location
Ratemarkt API is currently located at `api.ratemarkt.com` domain under `v1` directory of which the directory name also denotes the current API version you use.

Any API call requires a secure `HTTPS` connection (`HTTP` over `SSL`) and must be authenticated by using an API key to get granted for API resources.

Here is the base url for any API call.

```
https://api.ratemarkt.com/v1/
```

For instance, you should call the url below for check hotels endpoint.

```
https://api.ratemarkt.com/v1/checkhotels
```

## Authentication

In order to get autheticated against Ratemarkt API please see [Authentication](/api_docs/authentication.md) page. Once you get authenticated you will be able to access the resources below.

## Resources

All the API resources below accepts a JSON query object via HTTP post method for the sake of simplicity.

<table>
    <colgroup>
        <col width="20%">
        <col width="20%">
        <col width="60%">
    </colgroup>
    <thead>
        <tr>
            <th>Name</th>
            <th>Resource Path</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="/api_docs/check_hotels/" >Check Hotels</a></td>
            <td><code>/checkhotels</code></td>
            <td>Get availabile hotels by using a destination id or a list of hotel codes.</td>
        </tr>
        <tr>
            <td><a href="/api_docs/check_hotel/" >Check Hotel</a></td>
            <td><code>/checkhotel</code></td>
            <td>Single hotel availability for more recent data.</td>
        </tr>
        <tr>
            <td><a href="/api_docs/check_rate" >Check Rate</a></td>
            <td><code>/checkrate</code></td>
            <td>Single rate availability with the most recent data.</td>
        </tr>
        <tr>
            <td><a href="/api_docs/book_rate/" >Book Rate</a></td>
            <td><code>/bookrate</code></td>
            <td>Make a booking from a selected rate by using its rate key.</td>
        </tr>
        <tr>
            <td><a href="/api_docs/check_booking/" >Check Booking</a></td>
            <td><code>/checkbooking</code></td>
            <td>Query the booking status using either booking reference or client reference.</td>
        </tr>
        <tr>
            <td><a href="/api_docs/cancel_booking/" >Cancel Booking</a></td>
            <td><code>/cancelbooking</code></td>
            <td>Cancel refered booking when desired.</td>
        </tr>
    </tbody>
</table>

## Errors

To see how Ratemarkt API handles exceptional situations and errors please refer to our [Errors](/api_docs/errors.md) pages.

## Client Libraries

Are you looking for a client library for your favorite programming language?
Then you should take a look at our [Client Libraries](/api_docs/client_libraries.md) section .



