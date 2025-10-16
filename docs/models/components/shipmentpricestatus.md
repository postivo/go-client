# ShipmentPriceStatus

Shipment processing status.


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            | Example                                                |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `Error`                                                | **bool*                                                | :heavy_minus_sign:                                     | Indicates whether an error occurred during processing. | false                                                  |
| `Code`                                                 | **string*                                              | :heavy_minus_sign:                                     | Status code.                                           | SENT                                                   |
| `Description`                                          | **string*                                              | :heavy_minus_sign:                                     | Status description.                                    | Przekazano do wysyłki                                  |
| `Date`                                                 | [*time.Time](https://pkg.go.dev/time#Time)             | :heavy_minus_sign:                                     | Status timestamp (UTC).                                | 2024-06-01T16:22:07Z                                   |