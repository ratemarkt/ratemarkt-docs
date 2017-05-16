# Authenitcation

##  Introduction

In order to get authenticated against Ratemarkt API you should first request an API Key from your Ratemarkt account holder.

!!! tip "How to Obtain an API Key"
    Please see [Client Accounts][1] at [User's Guide][2] section on how to create a client account to generate API Key tied to that account.

[1]: users_guides/client_accounts/index.md
[2]: users_guides/getting_started.md


!!! warning "Secure you API Keys"
    While the data on the network is transmitted over a secure connection to the Ratemarkt API servers, securing your API Keys in the wild is your own duty.

    Please take care of your API keys and keep' em in highly secure environments otherwise attackers would get benefit from your keys on behalf of you once they capture them.

Once you obtain an API Key, the rest is quite easy though. Just put your API Key into your http headers while you make request to Ratemarkt API to able to get authenticated.

### Example

```terminal

$ curl -H "Authorization: Bearer <YOUR_API_KEY_HERE>"\
    https://api.ratemarkt.com/v1/checkhotels" -d"<REQUEST_BODY_JSON>"

```
