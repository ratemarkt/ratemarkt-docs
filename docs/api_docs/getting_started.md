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

| Name                                          | Resource Url         | Description                                                                 |
| --------------------------------------------- | -------------------- | --------------------------------------------------------------------------- |
| [Check Hotels](/api_docs/check_hotels.md)     | `/v1/checkhotels`    | Get availabile hotels by using a destination id or multiple hotel ids.      |
| [Check Hotel](/api_docs/check_hotel.md)       | `/v1/checkhotel`     | Single hotel availability for more recent data.                             |
| [Check Rate](/api_docs/check_rate.md)         | `/v1/checkrate`      | Single rate availability with the most recent data.                         |
| [Book Rate](/api_docs/book_rate.md)           | `/v1/bookrate`       | Make a booking from a selected rate by using its rate key.                  |
| [Check Booking](/api_docs/check_booking.md)   | `/v1/checkbooking`   | Query the booking status using either booking reference or client reference.|
| [Cancel Booking](/api_docs/cancel_booking.md) | `/v1/cancelbooking`  | Cancel refered booking when desired.                                        |

## Errors

To see how Ratemarkt API handles exceptional situations and errors please refer to our [Errors](/api_docs/errors.md) pages.

## Client Libraries

Are you looking for a client library for your favorite programming language?
Then you should take a look at our [Client Libraries](/api_docs/client_libraries.md) section .



