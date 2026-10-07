# CallbackUnion


## Supported Types

### Callback

```go
callbackUnion := components.CreateCallbackUnionCallback(components.Callback{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch callbackUnion.Type {
	case components.CallbackUnionTypeCallback:
		// callbackUnion.Callback is populated
}
```
