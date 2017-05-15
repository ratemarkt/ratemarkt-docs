# Getting Started

Welcome to Ratemarkt Client API.

Ratemarkt Client API is very intuitive, predictable and simple HTTP based REST-like Json API to make it very easy to get intgerated to Ratemarkt as a client. It just requires single API Key in http request headers and introduces only six end points in total to get all job done with ease.

## Location
Ratemarkt API is currently located at `api.ratemarkt.com` domain under `v1` directory which  denotes the current API version.
All API calls require a secure http connection (`HTTPS` over `SSL`) and must be authenticated using an API Key to get work.

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

