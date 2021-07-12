# Overview

Welcome to Black Ocean. Black Ocean offers a diverse array of connection protocols and messaging protocols.

## Connection Protocols

1.  REST (HTTP)
2.  Websockets
3.  TCP/IP

## Messaging Protocols

1.  REST
2.  JSON
3.  Google Protobuf's
4.  Black Ocean's Proprietary Binary Protocol

## Difference between messages through the various delivery protocols

Once the data has been extracted from the socket buffer, the messages themselves have no differences. JSON over TCP/IP is the same as JSON over websockets. The only protocol with a real difference is REST but fortunately, there is only one delivery mechanism for it. Therefore since every user has their own way of reading data from the socket buffer, we will not delve into that area. Instead, this document is intended to explain how to parse the data which was received irregardless of the delivery mechanism be it TCP/IP or Websockets.

## Message Headers

Most messages in the Black Ocean messaging protocols have a header preceeding the message. Message headers increase throughput by preventing the processing of data until a full message is received. The message headers also clearly define the message type received which adds efficiency in the processing of incoming data. The different message headers will be explained in the appropriate Messaging Protocol Sections. In Black Oceans messaging protocols, there are two ways to identify the message received, one from the afore mentioned header and the other is from the message itself. The message types in the header are listed below:

### Char message types

1. BOClientLogon = 'H'
2. BORiskUpdateRequest = 'w'
3. BORiskUserSymbol = 'N'
4. BOInstrumentRequest = 'Y'
5. BOInstrument = 'Q'
6. BOOpenOrderRequest = 'e'
7. BOCollateralUpdateReq = 'f'
8. BOCollateralData = 'h'
9. BOTransaction = 'T'

## Symbol Enums

Symbol Enums are replacements for the character based instrument name to a short integer. Symbols Enums are included in almost all Black Ocean messages pertaining to orders, risk management and reporting. Symbol Enums are used to replace hashing functions necessary to ﬁnd either orders, instrument data or risk information normally associated with instruments in most other trading systems. It is essential they be included in the messages which require them. Failure to include them will result in a reject of the message and wrong symbol Enums will result in undeﬁned behavior. Amer the login is complete, the user can send a BOInstrumentRequest message to the OES (Order Entry Server) and will receive back a BOInstrument message which contains all information for each instrument including the symbol name and the symbol Enum for that symbol name. The BOInstrumentRequest and BOInstrument messages will be covered in detail in a subsequent section.

### Current Instruments supported and their corresponding Symbol Enums

| Instrument Name | Symbol Enum |
| --------------- | ----------- |
| BTCUSD          | 1           |
| USDUSDT         | 2           |
| FLYUSDT         | 3           |
| BTCUSDT         | 4           |

## Order Types

Black Ocean offers the most complete set of order types in the crypto market including TRUE ICE orders. ICE orders allow the user to place up to 10 orders at a specified price offset per layer and a specified size at that price layer which move as the market moves. Black Ocean also offers Hidden orders, peg orders, hidden peg orders and display and refresh attributes for most order types. The complete list of order types is as follows:

### Current Order Types:

1.  LMT = 1,
2.  MKT = 2,
3.  STOP_MKT = 3,
4.  STOP_LMT = 4,
5.  PEG = 5,
6.  HIDDEN = 6,
7.  PEG_HIDDEN = 7,
8.  OCO = 8,
9.  ICE = 9,
10. SNIPER_MKT = 12,
11. SNIPER_LIMIT 13,
12. TSM = 14, // TRAILING_STOP_MKT
13. TSL = 15 // TRAILING_STOP_LMT

### Message Types

1.           ORDER_NEW = 1,
2.           CANCEL_REPLACE = 2,
3.           MARGIN_CANCEL_REPLACE = 3,
4.           MARGIN_EXECUTE = 4,
5.           ORDER_STATUS = 5,
6.           ORDER_CANCEL = 6,
7.           MARGIN_CANCEL = 7,
8.           EXECUTION = 8,
9.           EXECUTION_PARTIAL = 9,
10.         MARGIN_EXECUTION = 10,
11.         MARGIN_PARTIAL_EXECUTION = 11,
12.         REJECT = 12,
13.         ORDER_REJECT = 13,
14.         ORDER_ACK = 14,
15.         CANCELLED = 15,
16.         REPLACED = 16,
17.         QUOTE_FILL = 17,
18.         QUOTE_FILL_PARTIAL = 18,
19.         MARGIN_REPLACED = 19,
20.         CANCEL_REPLACE_REJECT = ,
21.         INSTRUMENT = 21,
22.         INSTRUMENT_REQUEST = 22,
23.         RISK_REJECT = 23,
24.         TOB_MSG = 24,
25.         THREE_LAYER_MD_MSG = 25,
26.         FIVE_LAYER_MD_MSG = 26,
27.         TEN_LAYER_MD_MSG = 27,
28.         TWENTY_LAYER_MD_MSG = 28,
29.         THIRTY_LAYER_MD_MSG = 29,
30.         EXEC_REPORT = 30,
31.         COLLATERAL_DATA = 31,
32.         COLLATERAL_UPDATE_REQ = 32,
33.         RISK_USER_SYMBOL = 33,
34.         RISK_UPDATE_REQUEST = 34,
35.         OPEN_ORDER_REQUEST = 35,
36.         CLIENT_LOGON = 36,
37.         MD_SNAPSHOT = 37,
38.         MD_SUBSCRIBE = 38,
