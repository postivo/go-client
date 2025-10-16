# Callback

Per-shipment callback configuration. When set, overrides the global callback defined in the user account.


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      | Example                                                          |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `URL`                                                            | *string*                                                         | :heavy_check_mark:                                               | Callback target URL.                                             | https://example.com/callback                                     |
| `UserToken`                                                      | **string*                                                        | :heavy_minus_sign:                                               | Bearer token to include in callback requests for authentication. | 75gh28hugjy8gfv6...                                              |