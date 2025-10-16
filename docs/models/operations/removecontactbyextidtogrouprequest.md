# RemoveContactByExtIDToGroupRequest


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `ExtID`                                                       | *string*                                                      | :heavy_check_mark:                                            | External (custom) ID of the contact to detach from the group. | my-id-1                                                       |
| `GroupID`                                                     | *int64*                                                       | :heavy_check_mark:                                            | Group `id` to detach from the contact.                        | 656                                                           |