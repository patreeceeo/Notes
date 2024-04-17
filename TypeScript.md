Tell the compiler about type declarations for a JavaScript file
```javascript
/// <reference types="path/to/types.d.ts" />
```

how to derive an object type that has the same keys but differently typed values:
```
type DerivedObject = {
	[<key name> in keyof OtherObject]: <value type>;
};
```

