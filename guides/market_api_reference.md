---

title: Market API Reference
excerpt: Full API Reference to get a high level overview of all endpoints and their functionalities
category: STARDUST_APIS_ID
slug: market-api-reference
order: 2

---

### API Info

##### Host: https://marketplace-api.stardust.gg
##### Base Path: /v1
##### Example Endpoint: https://marketplace-api.stardust.gg/v1/buyable/get

### Endpoints


#### [Player](docs.stardust.gg/reference/player-endpoints-1)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/player/get](https://docs.stardust.gg/reference/get_player-get)   | Get Information about a Player |
|  GET   |   [/player/inventory-get](https://docs.stardust.gg/reference/get_inventory-player-get)   | Get a Player's inventory  |
|  GET   |   [/balance/get](https://docs.stardust.gg/reference/get_balance-get)   | Get Balance of Player |
|  POST  |   [/balance/give](https://docs.stardust.gg/reference/post_balance-give)   | Give Funds to be Added to a Player's Balance |


#### [Buyable](docs.stardust.gg/reference/buyable-endpoints-1)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/buyable-item/get-all](https://docs.stardust.gg/reference/get_buyable-item-get-all-1)   | Get the List of Game Buyables  |
|  GET   |   [/buyable/get](https://docs.stardust.gg/reference/get_buyable-get-1)   | Get a Buyable from a Game  |
|  GET   |   [/buyable/get-all](https://docs.stardust.gg/reference/get_buyable-get-all-1)   | Get the List of Game Buyables  |
|  POST  |   [/buyable/buy](https://docs.stardust.gg/reference/post_buyable-buy-1)   | Buys Some Amount of a Buyable   |


#### [Currency](docs.stardust.gg/reference/currency-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/lookup/currency/blockchain](https://docs.stardust.gg/reference/get_lookup-currency-blockchain)   | Get a List of Available Currencies  |
|  PUT   |   [/currency/withdraw](https://docs.stardust.gg/reference/put_currency-withdraw)   | Let's a Player Withdraw Currency from their Stardust Wallet  |


#### [Game](docs.stardust.gg/reference/game-endpoints-1)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/game/get](https://docs.stardust.gg/reference/get_game-get-1)   | Get Game Details from a Game ID  |
|  GET   |   [/game/get-all](https://docs.stardust.gg/reference/get_game-get-all-1)   | Get all Games with details |


#### [Player Login](docs.stardust.gg/reference/player-login-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/oauth2/invalidate-tokens](https://docs.stardust.gg/reference/get_oauth2-invalidate-tokens)   | Invalidate a player's oAuth2 tokens |
|  POST  |   [/oauth2/exchange-code-for-tokens](https://docs.stardust.gg/reference/post_oauth2-exchange-code-for-tokens)   | Exchange auth code for oAuth2 tokens  |
|  POST  |   [/oauth2/retrieve-new-tokens](https://docs.stardust.gg/reference/post_oauth2-retrieve-new-tokens)   | Retrieve (refresh) new oAuth2 tokens  |
|  POST  |   [/player/login](https://docs.stardust.gg/reference/post_player-login-1)   | Login a player to marketplace  |
|  POST  |   [/player/login-verify-code](https://docs.stardust.gg/reference/post_login-verify-code)   | Verify player login token and returns session information |
|  POST  |   [/player/register](https://docs.stardust.gg/reference/post_register)   | Login a player to marketplace |


#### [Order](docs.stardust.gg/reference/order-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/order/get](https://docs.stardust.gg/reference/get_order-get)   | Get Orders by ID(s) |
|  GET   |   [/order/get-all](https://docs.stardust.gg/reference/get_order-get-all)   | Get all orders (can filter by playerId) |
|  GET   |   [/order/search](https://docs.stardust.gg/reference/get_order-search)   | Search all orders with extensive filter and sort |
|  POST  |   [/order/buy](https://docs.stardust.gg/reference/post_order-buy)   |  Buy an Order |
|  POST  |   [/order/cancel](https://docs.stardust.gg/reference/post_order-cancel)   | Cancel an order |
|  POST  |   [/order/create](https://docs.stardust.gg/reference/post_order-create)   | Create an order |


#### [External Wallet](docs.stardust.gg/reference/external-wallet-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/player/external-wallet/get-all](https://docs.stardust.gg/reference/get_player-external-wallet-get-all)   |    Get players external wallets         |
|  GET   |   [/player/external-wallet/get-assets](https://docs.stardust.gg/reference/get_player-external-wallet-get-assets)   |  Get Players external wallet assets           |
|  POST  |   [/player/external-wallet/link](https://docs.stardust.gg/reference/post_player-external-wallet-link)   | Links an external wallet to a players Id to be used just like a stardust managed wallet |
| DELETE |   [/player/external-wallet/unlink](https://docs.stardust.gg/reference/delete_player-external-wallet-unlink)   |   Unlink an external wallet from player          |


#### [Statistics](docs.stardust.gg/reference/statistics-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/stats/collection-floor-get](https://docs.stardust.gg/reference/get_stats-collection-floor-get)   | Get collection floor Statistics  |
|  GET   |   [/stats/game-get](https://docs.stardust.gg/reference/get_stats-game-get)   |       Get Game Statistics        |
|  GET   |   [/stats/game-rankings-get](https://docs.stardust.gg/reference/get_stats-game-rankings-get)   |    Get Game Rankings Statistics         |
|  GET   |   [/stats/marketplace-get](https://docs.stardust.gg/reference/get_stats-marketplace-get)   |    Get marketplace Statistics         |
|  GET   |   [/stats/profit-loss-get](https://docs.stardust.gg/reference/get_stats-profit-loss-get)   |    Get Profit Loss Statistics         |


#### [Template](docs.stardust.gg/reference/template-endpoints-1)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/template/get](https://docs.stardust.gg/reference/get_template-get-1)   |     Get the details of an template id        |
|  GET   |   [/template/get-all](https://docs.stardust.gg/reference/get_template-get-all-1)   |  Get the details of the first 100 templates |
|  GET   |   [/templates/asks](https://docs.stardust.gg/reference/get_templates-asks)   | Returns the associated FT or NFT for the passed in template I |


#### [Token](docs.stardust.gg/reference/token-endpoints-1)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/token/get](https://docs.stardust.gg/reference/get_token-get-1)   |    Some of the details of this token are based upon the Template that it was created from (using token/mint)   |
|  GET   |   [/token/additional-get](https://docs.stardust.gg/reference/get_token-additional-get)   |      Gives back a token details as well as game blockchain details |
|  GET   |   [/token-get/format](https://docs.stardust.gg/reference/get_token-get-format)   |    Gets target specific data for token details         |


<!--

#### [Player](docs.stardust.gg/reference/player-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|        | []()         |             |

-->
