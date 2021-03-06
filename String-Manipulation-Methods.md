## Introduction
JavaScript has some string manipulation methods. It is important to identify their behaviour in order to understand how they treat specific characters.

## Details
### Native Encoding Methods
 * escape/unescape
 * encodeURI/decodeURI
 * encodeURIComponent/decodeURIComponent

### Encoding Differences
```js
for(i=0;i<256;i++){
var cc=String.fromCharCode(i);
var es=escape(cc),eu=encodeURI(cc),euc=encodeURIComponent(cc)
if( es!=eu |  es!=euc| eu!=euc)
console.log(cc+"["+i+"]= "+es+" "+eu+" "+euc);

}
```

|  Char |  `escape` |  `encodeURI` |  `encodeURIComponent`|
|-------|---------|------------|--------------------|
|  `!` (33) |  %21 |  ! |  ! |
|  `#` (35) |  %23 |  # |  %23 |
|  `$` (36) |  %24 |  $ |  %24 |
|  `&` (38) |  %26 |  & |  %26 |
|  `'` (39) |  %27 |  ' |  ' |
|  `(` (40) |  %28 |  ( |  ( |
|  `)` (41) |  %29 |  ) |  ) |
|  `*` (42) |  `*` |  `*` | `*` |
|  `+` (43) |  + |  + |  %2B |
|  `,` (44) |  %2C |  , |  %2C |
|  `-` (45) |  - |  - |  - |
|  `.` (46) |  . |  . |  . |
|  `/` (47) |  / |  / |  %2F |
|  `0` (48-57) |  0-9 |  0-9 |  0-9 |
|  `:` (58) |  %3A |  : |  %3A |
|  `;` (59) |  %3B |  ; |  %3B |
|  `=` (61) |  %3D |  = |  %3D |
|  `?` (63) |  %3F |  ? |  %3F |
|  `@` (64) |  @ |  @ |  %40 |
|  `A` (65-90) |  A-Z |  A-Z |  A-Z |
|  `_` (95) |  `_` |  `_` |  `_` |
|  `a` (97-122) |  a-z |  a-z |  a-z |
|  `~` (126) |  %7E |  ~ |  ~ |
|  `` (128) |  %80 |  %C2%80 |  %C2%80 |

### Decoding differences
```js
for(i=0;i<256;i++){
var cc=String.fromCharCode(i);
try{
var eu=decodeURI(escape(cc)),euc=decodeURIComponent(escape(cc))
if( eu!=euc)
console.log("|  `"+cc+"``[`"+i+") |  "+eu+" |  "+euc+ " | ");
}catch(e){console.log('ee :'+i)}
}
```

|  Char |  decodeURI |  decodeURIComponent|
|-------|------------|--------------------|
|  `#` (35) |  %23 |  # |
|  `$` (36) |  %24 |  $ |
|  `&` (38) |  %26 |  & |
|  `,` (44) |  %2C |  , |
|  `:` (58) |  %3A |  : |
|  `;` (59) |  %3B |  ; |
|  `=` (61) |  %3D |  = |
|  `?` (63) |  %3F |  ? |

for `i >= 128` exception is triggered

### decodeURI and decodeURIComponents triggers exception on malformed seq.
```js
console.log(decodeURI("%C3%D8"));
```
This behaviour could be exploited in cases such as:
```js
var locParameter = getFromQueryString("aParameter");
try{
 ...
 locParameter = encodeUriComponent(locParameter);
 ...
}catch(e){}
...
 document.write(locParameter);
...
```

where the tainted variable is overwritten with its encoded value and later used in a sink.

### RegExps
#### flag modifiers
 * `g` : *global flag*
 * `i` : *case insensitive*
 * `m` : *multi line*

#### Special Characters
 * `\s`
 * `\w`
 * `[` `]`
 * `(` `)`
