# ShipmentDetailsStatus

Shipment processing status.


## Fields

| Field                                                           | Type                                                            | Required                                                        | Description                                                     | Example                                                         |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| `Error`                                                         | **bool*                                                         | :heavy_minus_sign:                                              | Indicates whether an error occurred during shipment processing. | false                                                           |
| `Code`                                                          | **string*                                                       | :heavy_minus_sign:                                              | Shipment status code.                                           | SENT                                                            |
| `Name`                                                          | **string*                                                       | :heavy_minus_sign:                                              | Shipment status description.                                    | Przekazano do wysyłki                                           |
| `Date`                                                          | [*time.Time](https://pkg.go.dev/time#Time)                      | :heavy_minus_sign:                                              | Date and time of the shipment status change (UTC).              | 2024-06-01T16:22:07Z                                            |