---
layout: post
title:  "DOM click event.target vs event.currentTarget"
date:   2016-02-25 13:49:00 +0700
categories: DOM Javascript HTML 
---

`event.target` is an object that capture the event.
`event.currentTarget` is the object which a listener is attached.

Example:

```HTML
<div id="outer">
    <div id="inner">
    </div>
</div>
<script>
$('#outer').on('click', funciton(evt) {
        console.log(evt.currentTarget);
        console.log(evt.current);
    });
</script>
```

The currentTarget will be `#outer` and the target will be `#inner`.