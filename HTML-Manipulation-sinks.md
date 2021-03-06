## Browser JavaScript execution sinks
The following operations allow HTML manipulation. If it is possible to control, even partially, the vulnerable argument, then it is possible to manipulate, to some extent the HTML and consequently, gain control of the user interface or execute JavaScript using classic Cross Site Scripting attacks.

| *Sink* | *Argument* | *Browser* | Example | Note |
|--------|------------|-----------|---------|------|
| `document.write` | any | *All* | document.write("htmlString"+ **usercontrolledVal**) | |
| `document.writeln` | any | *All* | document.writeln("htmlString"+ **usercontrolledVal**) | |
| anyElement.innerHTML | assigned value | *All* | divEl.innerHTML = "htmlString"+ **usercontrolledVal** | |
| `Range.createContextualFragment` | first arg | *All* | range.createContextualFragment("htmlString"+ **usercontrolledVal** ) | |
| HTMLButton.value | assigned value | *Explorer* | buttonTag.value = "htmlString"+ **usercontrolledVal** | Equivalent to buttonTag.innerHTML assignment case  |


(TBF)
