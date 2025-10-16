# UpdateContactByExternalIDResponse


## Fields

| Field                                                                     | Type                                                                      | Required                                                                  | Description                                                               |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `HTTPMeta`                                                                | [components.HTTPMetadata](../../models/components/httpmetadata.md)        | :heavy_check_mark:                                                        | N/A                                                                       |
| `ContactResponse`                                                         | [*components.ContactResponse](../../models/components/contactresponse.md) | :heavy_minus_sign:                                                        | The request was processed successfully (contact updated).                 |
| `ErrorResponse`                                                           | [*components.ErrorResponse](../../models/components/errorresponse.md)     | :heavy_minus_sign:                                                        | Invalid request.                                                          |
| `Headers`                                                                 | map[string][]*string*                                                     | :heavy_check_mark:                                                        | N/A                                                                       |