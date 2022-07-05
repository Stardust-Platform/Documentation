---

title: Core API Reference
excerpt: Full API Reference to get a high level overview of all endpoints and their functionalities
category: STARDUST_APIS_ID
slug: core-api-reference
order: 1

---

### API Info

##### Host: https://core-api.stardust.gg/
##### Base Path: /v1
##### Example Endpoint: https://core-api.stardust.gg/v1/template/get

### Endpoints

#### [Template](docs.stardust.gg/v0.0.0/reference/template-endpoints)

| Method |                                             Endpoint                                             | Description                                                                           |
|:------:|:------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------- |
|  GET   |           [/template/get](https://docs.stardust.gg/v0.0.0/reference/get_template-get)            | Get the details of a Template                                                         |
|  GET   |       [/template/get-all](https://docs.stardust.gg/v0.0.0/reference/get_template-get-all)        | Get all Templates along with their details                                            |
|  GET   |         [/template/count](https://docs.stardust.gg/v0.0.0/reference/get_template-count)          | Get the total count of templates based on filter                                      |
|  GET   |         [/get-tokens](https://docs.stardust.gg/v0.0.0/reference/get_template-get-tokens)         | Get all the token instances of a given template                                       |
|  POST  |        [/template/create](https://docs.stardust.gg/v0.0.0/reference/post_template-create)        | Creates a new template from which tokens can be minted and issued                     |
|  POST  |   [/template/create-bulk](https://docs.stardust.gg/v0.0.0/reference/post_template-create-bulk)   | Creates multiple templates at the same time                                           | 
|  PUT   |        [/template/mutate](https://docs.stardust.gg/v0.0.0/reference/put_template-mutate)         | Updates existing metadata associated with the template or adds additional metadata    |
| DELETE |       [/template/remove](https://docs.stardust.gg/v0.0.0/reference/delete_template-remove)       | Removes a template from your game. NOTE: This will not remove currently minted tokens |
| DELETE | [/template/props-remove](https://docs.stardust.gg/v0.0.0/reference/delete_template-props-remove) | Removes selected metadata from a template                                             |

#### [Token](docs.stardust.gg/v0.0.0/reference/token-endpoints)

| Method | Endpoint                                                                                   | Description                                                                                                                                  |
| ------ | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | [/token/get](https://docs.stardust.gg/v0.0.0/reference/get_token-get)                      | Get the combined details of this token based on what it inherited from it's template and what was added at the time of mint with /token/mint |
| GET    | [/token/get-all](https://docs.stardust.gg/v0.0.0/reference/get_token-get-all)              | Get all tokens and their respective details. Expect a large paginated response                                                               |
| GET    | [/token/mint/get-all](https://docs.stardust.gg/v0.0.0/reference/get_token-mint-get-all)    | Return a list of players with the amount of tokens minted to them                                                                            |
| POST   | [/token/create](https://docs.stardust.gg/v0.0.0/reference/post_token-create)               | Adds a new token                                                                                                                             |
| POST   | [/token/mint](https://docs.stardust.gg/v0.0.0/reference/post_token-mint)                   | Mints a specified amount of a given token to a player                                                                                        |
| POST   | [/token/mint-bulk](https://docs.stardust.gg/v0.0.0/reference/post_token-mint-bulk)         | Mints a set of tokens at once to a player with each have their own respective amounts                                                        |
| POST   | [/token/burn](https://docs.stardust.gg/v0.0.0/reference/post_token-burn)                   | Removes a token from a players inventory and put's it back into circulation                                                                  |
| POST   | [/token/transfer](https://docs.stardust.gg/v0.0.0/reference/post_token-transfer)           | Transfers a set of tokens from one player to another                                                                                         |
| PUT    | [/token/mutate](https://docs.stardust.gg/v0.0.0/reference/put_token-mutate)                | Modifies the metadata on a given token                                                                                                       |
| DELETE | [/token/remove](https://docs.stardust.gg/v0.0.0/reference/delete_token-remove)             | Removes a token from circulation                                                                                                             |
| DELETE | [/token/props-remove](https://docs.stardust.gg/v0.0.0/reference/delete_token-props-remove) | Removes a metadata field on a given token                                                                                                                                             |

#### [Player](docs.stardust.gg/v0.0.0/reference/player-endpoints)
| Method |                                             Endpoint                                              | Description                                                                          |
|:------:|:-------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------ |
|  GET   |            [/player/count](https://docs.stardust.gg/v0.0.0/reference/get_player-count)            | Get the total count of players currently in your game                                |
|  GET   |  [/player/deposit-get-all](https://docs.stardust.gg/v0.0.0/reference/get_player-deposit-get-all)  | Get a list of all the deposits a players wallet has received from an outside address |
|  GET   |              [/player/get](https://docs.stardust.gg/v0.0.0/reference/get_player-get)              | Get the details of a certain player                                                  |
|  GET   |          [/player/get-all](https://docs.stardust.gg/v0.0.0/reference/get_player-get-all)          | Get all players and the details associated with each player                          |
|  GET   |           [/player/get-id](https://docs.stardust.gg/v0.0.0/reference/get_player-get-id)           | Get a players UUID by providing their UniqueID(email, username, number)              |
|  GET   |          [/player/get-ids](https://docs.stardust.gg/v0.0.0/reference/get_player-get-ids)          | Get all player UUIDS                                                                 |
|  GET   |    [/player/get-inventory](https://docs.stardust.gg/v0.0.0/reference/get_player-get-inventory)    | Get the inventory of all the tokens a player currently holds in their wallet         |
|  GET   |       [/player/wallet-get](https://docs.stardust.gg/v0.0.0/reference/get_player-wallet-get)       | Get the wallet information of a certain player                                       |
|  GET   | [/player/withdraw-get-all](https://docs.stardust.gg/v0.0.0/reference/get_player-withdraw-get-all) | Get a list of all the withdraws that have occurred from a players wallet             |
|  POST  |          [/player/create](https://docs.stardust.gg/v0.0.0/reference/post_player-create)           | Create a new player based on a UniqueID(email, username, number)                     |
|  POST  |      [/player/set-active](https://docs.stardust.gg/v0.0.0/reference/post_player-set-active)       | Set a player's status as active                                                      |
|  POST  |     [/player/player-withdraw](https://docs.stardust.gg/v0.0.0/reference/post_player-withdraw)     | Withdraw a token from a players wallet to send to an external wallet                 |
|  PUT   |           [/player/mutate](https://docs.stardust.gg/v0.0.0/reference/put_player-mutate)           | Update or add metadata associated with a given player                                |
| DELETE |         [/player/remove](https://docs.stardust.gg/v0.0.0/reference/delete_player-remove)          | Remove a player from the game                                                        |
| DELETE |   [/player/props-remove](https://docs.stardust.gg/v0.0.0/reference/delete_player-props-remove)    | Remove metadata associated with a given player                                                                                     |

#### Other Endpoints
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|  GET   |   [/game/get](https://docs.stardust.gg/v0.0.0/reference/get_game-get)   | Get the details of a given game            |
|  GET   |   [/health](https://docs.stardust.gg/v0.0.0/reference/get_health)   | Get the health Status of the Stardust Core API            |
|  GET   |   [/openapi](https://docs.stardust.gg/v0.0.0/reference/get_openapi)   | Get the OpenAPI information of the Stardust Core API            |

<!--

#### [Player](docs.stardust.gg/v0.0.0/reference/player-endpoints)
| Method | Endpoint | Description |
|:------:|:--------:|:----------- |
|        | []()         |             |

-->