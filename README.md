# camelcase-keys-safe

Safely convert object keys to camelCase recursively with circular reference protection, deep traversal, and robust error handling.

### Simple usage: 
``` JavaScript
import camelCaseSafe from 'camelcase-keys-safe';

var camelGotHumps = camelCaseSafe({'test-1':123, 'test-2':{'test-3:':{'test-four':132}}});

//{ test1: 123, test2: { 'test3:': { testFour: 132 } } }
console.log(camelGotHumps);
```
### Works with Arrays too:
``` JavaScript
var anotherCamelWithTheHump = camelCaseSafe({
	'test-1': 123,
	'test-Two': [{
		'test-three': {
			'test-FOUR': [{'test-five':[{testSix:{'test-seven':8}}]}]
		}
	}]
});

//{"test1":123,"testTwo":[{"testThree":{"testFOUR":[{"testFive":[{"testSix":{"testSeven":8}}]}]}}]}
console.log(JSON.stringify(anotherCamelWithTheHump));
```

### Handles Circular References Safely:
``` JavaScript
// Create an object with circular reference
const obj = { 'user-name': 'John', 'user-data': {} };
obj['user-data'].parent = obj; // Circular reference!

// This would cause infinite loops with regular recursive functions
// But camelCaseSafe handles it gracefully
const safeResult = camelCaseSafe(obj);
console.log(safeResult);
// { userName: 'John', userData: { parent: [Circular] } }
```
## Features

- ✅ **Circular Reference Protection**: Uses WeakMap caching to prevent infinite loops
- ✅ **Deep Traversal**: Recursively processes nested objects and arrays
- ✅ **Type Safety**: Preserves Date objects and other special types
- ✅ **Array Support**: Handles arrays containing objects
- ✅ **Performance Optimized**: Efficient caching mechanism
- ✅ **Zero Dependencies**: Only depends on `map-obj` for core functionality

## Installation

```bash
npm install camelcase-keys-safe
```

## More information on internal modules
[map-obj](https://www.npmjs.com/package/map-obj) // TODO

## Contributing
Simply make a pr with details on your bug and tests.
