# AddSenderResponse


## Fields

| Field                                                                 | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `HTTPMeta`                                                            | [components.HTTPMetadata](../../models/components/httpmetadata.md)    | :heavy_check_mark:                                                    | N/A                                                                   |
| `SenderDetails`                                                       | [*components.SenderDetails](../../models/components/senderdetails.md) | :heavy_minus_sign:                                                    | The request was processed successfully (sender created).              |
| `Headers`                                                             | map[string][]`string`                                                 | :heavy_check_mark:                                                    | N/A                                                                   |