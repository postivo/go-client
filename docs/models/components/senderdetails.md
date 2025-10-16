# SenderDetails

Extended sender details.


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            | Example                                                |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `ID`                                                   | **int64*                                               | :heavy_minus_sign:                                     | Unique sender ID.                                      | 665                                                    |
| `Sender`                                               | [components.Sender](../../models/components/sender.md) | :heavy_check_mark:                                     | Sender data for the shipment.                          |                                                        |
| `Active`                                               | *bool*                                                 | :heavy_check_mark:                                     | Indicates whether the sender is active.                | true                                                   |
| `Default`                                              | *bool*                                                 | :heavy_check_mark:                                     | Indicates whether this is the default sender.          | true                                                   |