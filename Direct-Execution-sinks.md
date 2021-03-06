## Browser JavaScript execution sinks
The following JavaScript functions parse strings as JavaScript. If it is possible to control, even partially, the vulnerable argument, then it is possible to execute JavaScript.

| *Function Name* | *Argument* | *Browser* | Example |
|-----------------|------------|-----------|---------|
| `eval` | first | *All* | eval("jsCode"+**usercontrolledVal** ) |
| `Function` | first if there's one, the last if >1 args | *All* | Function("jsCode"+**usercontrolledVal** ) ,<br><br> Function("arg","arg2","jsCode"+**usercontrolledVal** ) |
| `setTimeout` |  first <span title="if and only if">_IIF_</span> it is a string   | *All* | setTimeout("jsCode"+**usercontrolledVal** ,timeMs) |
| `setInterval` |  first <span title="if and only if">_IIF_</span> it is a string | *All* | setInterval("jsCode"+**usercontrolledVal** ,timMs) |
| `setImmediate` |  first <span title="if and only if">_IIF_</span> it is a string | *IE 10+* | `setImmediate`("jsCode"+**usercontrolledVal** ) |
| `execScript` |  first | *IE 6+* | execScript("jsCode"+**usercontrolledVal** ,"JScript") |
| `crypto.generateCRMFRequest` | 5th | *Firefox 2+* | crypto.generateCRMFRequest('CN=0',0,0,null,'jsCode'+**usercontrolledVal**,384,null,'rsa-dual-use') |
| `ScriptElement.src` | assignedValue | *All* | script.src =  **usercontrolledVal**  |
| `ScriptElement.text` | assignedValue | *Explorer* | script.text = 'jsCode'+**usercontrolledVal**  |
| `ScriptElement.textContent` | assignedValue | *All but IE<9* | script.textContent = 'jsCode'+**usercontrolledVal**  |
| `ScriptElement.innerText` | assignedValue | *All but Firefox* | script.innerText = 'jsCode'+**usercontrolledVal**  |
| anyTag.*onEventName* | assignedValue | *All* | anyTag.onclick = 'jsCode'+**usercontrolledVal**  |

(TBF)
