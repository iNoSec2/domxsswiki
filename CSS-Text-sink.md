## Details
Setting a CSSStyleDeclaration by using unescaped input could be dangerous. It is mostly browser specific. The following table shows Javascript based attacks.

|*Tag* | *Browser* | *Version*  | * `CssText` attack vector* | *Impact* | *Limitations/Notes* |
|------|-----------|------------|----------------------------|----------|---------------------|
| `*`  | Opera  | 10.63 | `-o-link:'javascript:alert(1)';-o-link-source:current` | Js Exec with user click | User Interaction |
| `*` | Firefox | 3.x.x/4.x |  `-moz-binding:url(//vi.ct.im/page?par=val#checkbox);` | Js Exec | only on same site - SOP compliance - so a XML Inj or upload is needed. Content-type: text/xml or application/xml (? - to be confirmed)  |
| `*` | IE | 7/8 |  `a:expression(write(1))` | Js Exec | ?  |
