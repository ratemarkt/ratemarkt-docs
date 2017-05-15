# Getting Started

Welcome to Ratemarkt Client API.

## Introduction

Ratemarkt Client API is quite intuitive, predictable and very easy http based json API to make it very easy to get intgerated with Ratemarkt as a client.

It just requires a single API key in http headers to get authenticated and introduces only six end points in total to get all job done with ease.

## Location
Ratemarkt API is currently located at `api.ratemarkt.com` domain under `v1` directory which also denotes the current API version.
All calls require a secure http connection (`HTTPS`, `SSL`) and must be authenticated using an API key to get work.

Here is the base url for all API calls.

```
https://api.ratemarkt.com/v1/
```

For instance, you should call the url below for check hotels endpoint.

```
https://api.ratemarkt.com/v1/checkhotels
```

## Authentication

In order to get autheticated agains Ratemarkt API please see [Authentication](/api_docs/authentication.md) page. Once you get authenticated you will be able to access the resources below.

## Resources

* [Check Hotels](/api_docs/check_hotels.md) Get availabile hotels by a destination or multiple hotel id information.
* [Check Hotel](/api_docs/check_hotel.md) Single hotel availability with more recent data.
* [Check Rate](/api_docs/check_rate.md) Single rate availability with the most recent information by a rate key.
* [Book Rate](/api_docs/book_rate.md) Make a booking from the selected rate by using rate key.
* [Check Booking](/api_docs/check_booking.md) Query the booking status using either booking reference or client reference.
* [Cancel Booking](/api_docs/cancel_booking.md) Cancel refered booking when desired.

## Errors

To see how Ratemarkt API handles exceptional situations and errors please refer to our [Errors](/api_docs/errors.md) pages.