---
layout: default
title: Water Flow
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/water-flow/
---

# Water Flow Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

The Gravity Water Flow sensor meansures the rate of a liquid flowing thorugh it. 

Name: Gravity: Water Flow Sensor (1/2") For Arduino

Link: https://www.dfrobot.com/product-1517.html

Type: Analog 

Operational Range: 1 to 120 degrees C

Unit: L/min

---

## Notes 
This sensor must be installed vertically.

This sensor can not be tilted no more than 5 degrees.
## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "wf",          # string
  data_type: "L/s",    # string -- microsiemens/centimeter
  data_value:          # float
}
```
</div>

<!-- {% highlight markdown %}
```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```
{% endhighlight %} -->

<!-- --- -->

<!-- ## Code blocks with rendered examples

To demonstrate front end code, sometimes it's useful to show a rendered example of that code. After including the styles from your project that you'll need to show the rendering, you can use a `<div>` with the `code-example` class, followed by the code block syntax. If you want to render your output with Markdown instead of HTML, use the `markdown="1"` attribute to tell Jekyll that the code you are rendering will be in Markdown format... This is about to get meta...

<div class="code-example" markdown="1">

<div class="code-example" markdown="1">

[Link button](http://example.com/){: .btn }

</div>
```markdown
[Link button](http://example.com/){: .btn }
```

</div>
{% highlight markdown %}
<div class="code-example" markdown="1">

[Link button](http://example.com/){: .btn }

</div>
```markdown
[Link button](http://example.com/){: .btn }
```
{% endhighlight %} -->
