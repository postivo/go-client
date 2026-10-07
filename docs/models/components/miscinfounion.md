# MiscInfoUnion


## Supported Types

### MiscInfo

```go
miscInfoUnion := components.CreateMiscInfoUnionMiscInfo(components.MiscInfo{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch miscInfoUnion.Type {
	case components.MiscInfoUnionTypeMiscInfo:
		// miscInfoUnion.MiscInfo is populated
}
```
