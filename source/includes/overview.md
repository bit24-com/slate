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

## Msg-Delivery Protocol Differences

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
`
### Current Instruments supported and their corresponding Symbol Enums

| Instrument Name | Symbol Enum |
| --------------- | ----------- |
| BTCUSD          | 1           |
| USDUSDT         | 2           |
| FLYUSDT         | 3           |
| BTCUSDT         | 4           |


## System Enums

### MESSAGE_TYPE

|           Field           |     Value(short)   |
| ------------------------- | ------------------ |
| ORDER_NEW                 |          1         |
| CANCEL_REPLACE            |                    |
| MARGIN_CANCEL_REPLACE     |                    |
| MARGIN_EXECUTE            |                    |
| ORDER_STATUS              |                    |
| ORDER_CANCEL              |                    |
| MARGIN_CANCEL             |                    |
| EXECUTION                 |                    |
| EXECUTION_PARTIAL         |                    |
| MARGIN_EXECUTION          |         10         |
| MARGIN_PARTIAL_EXECUTION  |                    |
| REJECT                    |                    |
| ORDER_REJECT              |                    |
| ORDER_ACK                 |                    |
| CANCELLED                 |         15         |
| REPLACED                  |                    |
| QUOTE_FILL                |                    |
| QUOTE_FILL_PARTIAL        |                    |
| MARGIN_REPLACED           |                    |
| CANCEL_REPLACE_REJECT     |         20         |
| INSTRUMENT                |                    |
| INSTRUMENT_REQUEST        |                    |
| RISK_REJECT               |                    |
| TOB_MSG                   |                    |
| THREE_LAYER_MD_MSG        |         25         |
| FIVE_LAYER_MD_MSG         |                    |
| TEN_LAYER_MD_MSG          |                    |
| TWENTY_LAYER_MD_MSG       |                    |
| THIRTY_LAYER_MD_MSG       |                    |
| EXEC_REPORT               |         30         |
| COLLATERAL_DATA           |                    |
| COLLATERAL_UPDATE_REQ     |                    |
| RISK_USER_SYMBOL          |                    |
| RISK_UPDATE_REQUEST       |                    |
| OPEN_ORDER_REQUEST        |         35         |
| CLIENT_LOGON              |                    |
| MD_SNAPSHOT               |                    |
| MD_SUBSCRIBE              |                    |

### UPDATE_TYPE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| NORMAL_UPDATE          |          1         |
| USER_REQUEST           |                    |
| UNSOLICITED            |                    |
| EXCHANGE_REQUEST       |                    |
| SNAPSHOT               |          1         |
| SNAPSHOT_START         |                    |
| SNAPSHOT_CONTINUATION  |                    |
| SNAPSHOT_FINISH        |                    |
| UPDATE                 |                    |
| POSS_DUP               |                    |


### ORD_TYPE

|          Field         |                         Value (short)                     |
| ---------------------- | --------------------------------------------------------- |
| LMT                    |                               1                           |
| MKT                    |                                                           |
| STOP_MKT               |                                                           |
| STOP_LMT               |                                                           |
| PEG                    |                                                           |
| HIDDEN                 |                                                           |
| PEG_HIDDEN             |                                                           |
| OCO                    |                                                           |
| ICE                    |                                                           |
| OCO_ICE                |                                                           |
| BRACKET                |                                                           |
| SNIPER_MKT             |                                                           |
| SNIPER_LIMIT           |                                                           |
| TSM                    | (TRAILING_STOP_MKT)                                       |
| TSL                    | (TRAILING_STOP_LMT)                                       |
| TPSL_MARKET            | (Has 3 prices associated with it, entry, profit and stop) |
| TPSL_LIMIT             | (Has 3 prices associated with it, entry, profit and stop) |


### ATTRIBUTE_TYPES

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| RESERVED_TYPE          |                    |
| HIDDEN_TYPE            |          1         |
| DISPLAY_TYPE           |                    |
| SIZEINCREMENT_TYPE     |                    |
| POST_TYPE              |                    |
| PRICEINCREMENT_TYPE    |                    |
| OFFSET_TYPE            |                    |
| STOP_MKT_TYPE          |                    |
| STOP_LMT_TYPE          |                    |
| PEG_TYPE               |                    |
| TSL_TYPE               |                    |
| TSM_TYPE               |                    |

### TIF

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| FOK                    |          1         |
| GTC                    |                    |
| IOC                    |                    |
| POO                    | (Make only)        |
| RED                    | (Reduce only)      |
| DAY                    |                    |


### SIDE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| BUY                    |          1         |
| SELL                   |                    |
| SELLSHORT              |                    |

### FEE_TYPE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| MAKE                   |          1         |
| TAKE                   |                    |

### SUBSCRIBE_TYPE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| TOB                    |          1         |
| THREELAYERS            |                    |
| FIVELAYERS             |                    |
| TENLAYERS              |                    |
| TWENTYLAYERS           |                    |
| THIRTYLAYERS           |                    |
| FOB_DATA               |                    |
| FLB_DATA               |                    |

### TRANSACTION_OFFSET

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| MESSAGE_TYPE_OFFSET    |           4        |
| ATTRIBUTE              |           6        |
| ACCOUNT                |           8        |
| ORDER_ID               |          12        |
| SYMBOL_ENUM            |          20        |
| ORDER_TYPE             |          22        |
| SYMBOL_TYPE            |          24        |
| BO_PRICE               |          26        |
| BO_SIDE                |          34        |
| BO_ORDER_QTY           |          36        |
| BO_TIME_IN_FORCE       |          44        |
| STOP_LIMIT_PRICE       |          46        |
| SYMBOL                 |          54        |
| ORIG_ORDER_ID          |          66        |
| BO_CANCEL_SHARES       |          74        |
| EXEC_ID                |          82        |
| EXEC_SHARES            |          90        |
| REMAINING_QUANTITY     |          98        |
| LIMIT_CROSS            |         106        |
| EXPIRATION_DATE        |         114        |
| TRADER_ID              |         126        |
| REJECT_REASON          |         132        |
| SENDING_TIME           |         134        |
| TRADING_SESSION_ID     |         142        |
| KEY                    |         146        |
| DISPLAY_SIZE           |         150        |
| REFRESH_SIZE           |         158        |
| LAYERS                 |         166        |
| SIZE_INCREMENT         |         168        |
| PRICE_INCREMENT        |         176        |
| PRICE_OFFSET           |         184        |
| BO_ORIGPRICE           |         192        |
| EXEC_PRICE             |         200        |
| MSG_SEQ_NUM            |         208        |
| TAKE_PROFIT_PRICE      |         216        |
| TRIGGER_TYPE           |         224        |
| ATTRIBUTES_TYPE        |         226        |

### LOGON_STATUS

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| FAILED                 |          1         |
| SUCCESSFUL             |                    |


### SYMBOL_VALUE_ENUM

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| BTCUSD                 |          1         |
| USDUSDT                |                    |
| FLYUSDT                |                    |
| BTCUSDT                |                    |

### BO_REJECT_CODE

|                          Field                       |     Value(short)   |
| ---------------------------------------------------- | ------------------ |
| ORDER_NOT_FOUND                                      |          1         |
| USER_NOT_FOUND                                       |                    |
| ACCOUNT_NOT_FOUND                                    |                    |
| INVALID_KEY                                          |                    |
| ACCOUNT_DISABLED                                     |                    |
| TRADING_SESSION_INVALID                              |                    |
| RISK_ACCOUNT_NOT_FOUND                               |                    |
| RISK_SYMBOL_NOT_FOUND                                |                    |
| MES_NOT_AVAILABLE_TRADING_DISABLED                   |                    |
| OES_NOT_AVAILABLE_TRADING_DISABLED                   |         10         |
| MDS_NOT_AVAILABLE_TRADING_DISABLED                   |                    |
| MSG_TYPE_INVALID                                     |                    |
| ORD_TYPE_INVALID                                     |                    |
| PRICE_INVALID                                        |                    |
| SIZE_INVALID                                         |                    |
| STOP_PRICE_INVALID                                   |                    |
| STOP_SIZE_INVALID                                    |                    |
| ORDER_SIDE_INVALID                                   |                    |
| ACCOUNT_INVALID                                      |                    |
| ORDERID_INVALID                                      |         20         |
| SENDING_TIME_INVALID                                 |                    |
| ORIG_PRICE_INVALID                                   |                    |
| ORIG_SIZE_INVALID                                    |                    |
| ICE_SIZEINCREMENT_TIMES_LAYERS_NOT_EQUAL_ORDQTY      |                    |
| ORIG_ORDER_ID_INVALID                                |                    |
| SYMBOL_ENUM_INVALID                                  |                    |
| SIZE_INCREMENT_INVALID                               |                    |
| PRICE_OFFSET_INVALID                                 |                    |
| PRICE_INCREMENT_INVALID                              |                    |
| EXCEEDED_MAX_LAYERS                                  |         30         |
| DISPLAY_SIZE_INVALID                                 |                    |
| REFRESH_SIZE_INVALID                                 |                    |
| INVALID_SECURITY_KEY                                 |                    |
| USER_ALREADY_LOGGED_IN                               |                    |
| INVALID_FIELD_VALUE                                  |                    |
| PERCENTAGE_MOVE_EXCEEDED_COOLING_OFF_PERIOD_IN_FORCE |                    |
| INSTRUMENT_WOULD_CAUSE_MARGIN_TO_BE_EXCEEDED         |                    |
| INSTRUMENT_MARGIN_EXCEEDED                           |                    |
| MARGIN_BUY_ORDER_CANCELLATION_IN_PROGRESS            |                    |
| MARGIN_SELL_ORDER_CANCELLATION_IN_PROGRESS           |                    |
| MARGIN_LONG_POSITION_LIQUIDATION_IN_PROGRESS         |                    |
| MARGIN_SHORT_POSITION_LIQUIDATION_IN_PROGRESS        |                    |
| OUTSTANDING_OPEN_REQUESTS_EXCEEDED                   |                    |
| NO_RISK_DATA                                         |                    |
| DUPLICATE_ORDER_ID                                   |                    |
| EXCEEDS_OPEN_ORDER_REQUESTS                          |                    |
| NOT_ENOUGH_EQUITY_TO_COMPLETE                        |                    |
| MATCHING_ENGINE_REJECTED                             |                    |
| NONE                                                 |                    |
| ACCEPTED                                             |                    |
| KEY_INVALID                                          |                    |
| MSG_SEQ_NUM_INVALID                                  |                    |
| USER_ALREADY_LGGGED_IN                               |                    |
| ORIG_ORDER_NOT_FOUND                                 |                    |
| INVALID_LOGON_TYPE                                   |                    |
| CANT_EXECUTE_AGAINST_EXCHANGE_ORDER                  |                    |
| NO_MARKET_MAKER_VOLUME                               |                    |


### BO_CONNECTION_PROTOCOL

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| API_BINARY_TRANSACTION |          1         |
| API_BINARY_TRADITIONAL |                    |
| API_WS_TRANSACTION     |                    |
| API_WS_TRADITIONAL     |                    |
| WEB                    |                    |


### STOP_TRIGGER

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| LAST_PRICE             |                    |
| INDEX                  |                    |
| MARK                   |                    |

### LOGON_TYPE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| LOGIN                  |          1         |
| LOGOUT                 |                    |

### REQUEST_TYPE

|          Field         |     Value(short)   |
| ---------------------- | ------------------ |
| ALL                    |          1         |
| SE                     |                    |

### ACCOUNT_TYPE

|          Field         |     Value(char)    |
| ---------------------- | ------------------ |
| BO_USER                |          B         |
| NORMAL_USER            |          N         |
| MM_USER                |          M         |
| EXCHANGE_USER          |          E         |

### COLLATERAL_ENUM

|          Field         |    Value(short)    |
| ---------------------- | ------------------ |
| BTC                    |          1         |
| USDT                   |                    |
| FLY                    |                    |
| USD                    |                    |

### BO_MSG_SIZE

|          Field          |    Value(short)    |
| ----------------------- | ------------------ |
| S_HEARTBEAT_TESTREQUEST |          6         |
| S_OPEN_ORDER_REQUEST    |         24         |
| S_INSTRUMENT_REQUEST    |         62         |
| S_INSTRUMENT            |         74         |
| S_RISK_USER_SYMBOL      |        161         |
| S_CLIENT_LOGON          |        143         |
| S_TRANSACTION           |        238         |
| S_TRANSACTBUF           |        330         |

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
11. SNIPER_LIMIT = 13,
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
