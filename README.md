# @firanorg/vero-laborum-tenetur.js

[![downloads](https://img.shields.io/npm/dt/@firanorg/vero-laborum-tenetur.svg)](https://www.npmjs.com/package/@firanorg/vero-laborum-tenetur) [![CDNJS version](https://img.shields.io/cdnjs/v/@firanorg/vero-laborum-tenetur.svg)](https://cdnjs.com/libraries/@firanorg/vero-laborum-tenetur)

@firanorg/vero-laborum-tenetur.js provides a simple way to get a human-readable file size string from a number (float or integer) or string.

```javascript
import {@firanorg/vero-laborum-tenetur} from "@firanorg/vero-laborum-tenetur";
@firanorg/vero-laborum-tenetur(265318, {standard: "jedec"}); // "259.1 KB"
```

## Testing

@firanorg/vero-laborum-tenetur has 100% code coverage with its tests.

```console
--------------|---------|----------|---------|---------|-----------------------
File          | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
--------------|---------|----------|---------|---------|-----------------------
All files     |     100 |    95.52 |     100 |     100 |                      
 @firanorg/vero-laborum-tenetur.cjs |     100 |    95.52 |     100 |     100 | 77-78,173,196,199,210
--------------|---------|----------|---------|---------|-----------------------
```

## Optional settings

`@firanorg/vero-laborum-tenetur()` accepts an optional descriptor Object as a second argument, so you can customize the output.

### base
_*(number)*_ Number base, default is `10`

### bits
_*(boolean)*_ Enables `bit` sizes, default is `false`

### exponent
_*(number)*_ Specifies the symbol via exponent, e.g. `2` is `MB` for base 2, default is `-1`

### fullform
_*(boolean)*_ Enables full form of unit of measure, default is `false`

### fullforms
_*(array)*_ Array of full form overrides, default is `[]`

### locale (overrides 'separator')
_*(string || boolean)*_ BCP 47 language tag to specify a locale, or `true` to use default locale, default is `""`

### localeOptions (overrides 'separator', requires string for 'locale' option)
_*(object)*_ Dictionary of options defined by ECMA-402 ([Number.prototype.toLocaleString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)). Requires locale option to be explicitly passed as a string, otherwise is ignored.

### output
_*(string)*_ Output of function (`array`, `exponent`, `object`, or `string`), default is `string`

### pad
_*(boolean)*_ Decimal place end padding, default is `false`

### precision
_*(number)*_ Sets precision of numerical output, default is `0`

### round
_*(number)*_ Decimal place, default is `2`

### roundingMethod
_*(string)*_ Rounding method, can be `round`, `floor`, or `ceil`, default is `round`

### separator
_*(string)*_ Decimal separator character, default is `.`

### spacer
_*(string)*_ Character between the `result` and `symbol`, default is `" "`

### standard
_*(string)*_ Standard unit of measure, can be `iec`, `jedec`, or `si`. Default is `si` (base 10). The `si` option is an alias of `jedec`, such that it is not valid for other configuration options.

### symbols
_*(object)*_ Dictionary of IEC/JEDEC symbols to replace for localization, defaults to english if no match is found; SI is handled automatically with JEDEC values.

## Examples

```javascript
@firanorg/vero-laborum-tenetur(500);                        // "500 B"
@firanorg/vero-laborum-tenetur(500, {bits: true});          // "4 kbit"
@firanorg/vero-laborum-tenetur(265318, {base: 2});          // "259.1 KiB"
@firanorg/vero-laborum-tenetur(265318);                     // "265.32 kB"
@firanorg/vero-laborum-tenetur(265318, {round: 0});         // "265 kB"
@firanorg/vero-laborum-tenetur(265318, {output: "array"});  // [265.32, "kB"]
@firanorg/vero-laborum-tenetur(265318, {output: "object"}); // {value: 265.32, symbol: "kB", exponent: 1, unit: "kB"}
@firanorg/vero-laborum-tenetur(1, {symbols: {B: "Б"}});     // "1 Б"
@firanorg/vero-laborum-tenetur(1024);                       // "1.02 kB"
@firanorg/vero-laborum-tenetur(1024, {exponent: 0});        // "1024 B"
@firanorg/vero-laborum-tenetur(1024, {output: "exponent"}); // 1
@firanorg/vero-laborum-tenetur(265318, {standard: "jedec"});  // "259.1 KB"
@firanorg/vero-laborum-tenetur(265318, {base: 2, fullform: true}); // "259.1 kibibytes"
@firanorg/vero-laborum-tenetur(12, {fullform: true, fullforms: ["байтов"]});  // "12 байтов"
@firanorg/vero-laborum-tenetur(265318, {separator: ","});   // "265,32 kB"
@firanorg/vero-laborum-tenetur(265318, {locale: "de"});   // "265,32 kB"
```


## Partial Application
`partial()` takes the second parameter of `@firanorg/vero-laborum-tenetur()` and returns a new function with the configuration applied 
upon execution. This can be used to reduce `Object` creation if you call `@firanorg/vero-laborum-tenetur()` without caching the `descriptor` 
in lexical scope.

```javascript
import {partial} from "@firanorg/vero-laborum-tenetur";
const size = partial({standard: "jedec"});

size(265318); // "259.1 KB"
```

## License
Copyright (c) 2024 Jason Mulligan
Licensed under the BSD-3 license.
