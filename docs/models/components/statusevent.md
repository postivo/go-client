# StatusEvent

Single shipment status event.


## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               | Example                                                   |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `UniqueID`                                                | **int64*                                                  | :heavy_minus_sign:                                        | Unique status event ID.                                   | 778656                                                    |
| `Type`                                                    | **string*                                                 | :heavy_minus_sign:                                        | Event type: `OK` (regular) or `EX` (exception/irregular). | OK                                                        |
| `Code`                                                    | **string*                                                 | :heavy_minus_sign:                                        | Status event code.                                        | ACCEPTED                                                  |
| `Name`                                                    | **string*                                                 | :heavy_minus_sign:                                        | Status event description.                                 | Przesyłka przyjęta do realizacji                          |
| `Details`                                                 | **string*                                                 | :heavy_minus_sign:                                        | Status event details (for EXTERNAL status codes).         | Przyjęcie do Punktu Dystrybucyjnego                       |
| `Date`                                                    | [*time.Time](https://pkg.go.dev/time#Time)                | :heavy_minus_sign:                                        | Status event timestamp (UTC).                             | 2024-06-01T12:00:00Z                                      |