Cryptoclock uses websockets to connect to our servers for data and configuration.

## Endpoint

Main url for our service is

    wss://ticker.cryptoclock.net

We also have staging environment with latest software for testing purposes

    wss://ticker.staging.cryptoclock.net

## Subscription paths

You can use path in stucture *source/pair* to subscribe for data.

Eg.

    $ telsocket wss://ticker.cryptoclock.net/bitfinex/BTCUSD

## Welcome message

After successfull handshake, server sends welcome message

    ; Welcome client bc353109-5aba-42cf-a62a-4651e04fad43

This message includes device's UUID. It is generated upon every connection unless you specify your own UUID.

## UUID

Every device has it's own UUID, which is used for web configuration and custom subscriptons identification. UUID is generated on every device factory reset.

You can specify your UUID while connecting to websocket server.

Eg.

    $ telsocket wss://ticker.cryptoclock.net/bitfinex/BTCUSD?uuid=bc353109-5aba-42cf-a62a-4651e04fad43

## Data

Websocket servers sends two types of data.

First is ticker data. It is sent as plain number.

Second is aditional data. Aditional data line is prefixed with semicolon *;*

## Aditional data

### HB
Server sends periodicaly heartbeat message.

Eg.

    ;HB

### ATH
Upon connect, server sends this pair all time high value. This is used for graphical notification on tickers.

Eg.

    ;ATH=17251

### MSG
User can send one time message to its device. Message is dispayed on display

Eg.

    ;MSG this is my device

## Device authentication

Device can be configured via https://www.cryptoclock.net web interface. To do this, you need to authenticate the device.

Device sends *;OTP_REQ* to server, server replies with numeric value in *;OTP=* message. Device then displays this one time password on display and user enters it into website. Successul OTP entry is notified via *;OTP_ACK* message.

Eg.

    > ;OTP_REQ
    < ;OTP=507127
    < ;HB
    < ;HB
    < ;OTP_ACK
