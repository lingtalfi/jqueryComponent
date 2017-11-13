Jquery component
====================
2017-11-13


Make sure your script is loaded only when jquery is ready.



Code
------------

Put this at the very top of your app.

```html
<script>
    window.jqueryComponent = {
        ready: function (callback) {
            if (window.jQuery) {
                callback();
            }
            else {
                document.addEventListener("DOMContentLoaded", function (event) {
                    $(document).ready(function () {
                        callback();
                    });
                });
            }
        }
    };
</script>


```

Then, anywhere after that, you can invoke the **jqueryComponent.ready** function 
like so:

```html
<script>
window.jqueryComponent.ready(function () {
    console.log("yeah");
});
</script>

```



The problem
---------------

There are basically two strategies when using jquery:

- either you include the jquery library at the top (in your head tag for instance)
- or you include the jquery library at the bottom (just before the closing body tag)


If you include jquery at the top, then all subsequent calls can be done like
this:

```js
$(document).ready(function () {
    console.log("standard jquery call");
});
```

However, if you include jquery at the bottom, the above call won't work,
because the dollar symbol is undefined.
Instead, you can work around like this:

```js
document.addEventListener("DOMContentLoaded", function (event) {
    $(document).ready(function () {
        console.log("now it works");
    });
});
```


However, if you refresh a portion of the page using a server side
pre-rendered html block, if your block contains the above code,
the inner js code (console.log) won't be executed, because the
DOMContentLoaded will not be fired again.


Hmm, so the solution is the code displayed at the top of this document,
which let us handle the 3 cases with the same approach:

```js
window.jqueryComponent.ready(function () {
    console.log("yeah");
});
```  






