---
layout: default
title: Dissolved Oxygen
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/do
---

# Dissolved Oxygen Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Dissolved Oxygen sensor.

Name: Gravity: Analog Dissolved Oxygen Sensor / Meter Kit For Arduino
Link: https://www.dfrobot.com/product-1628.html
Calibration: Calibrated against air. Dip probe in water, and wave probe in air. 
Type: Analog 
Operational Range: 1 to 50 degrees C
Unit: % Saturation 
Range: 1% t0 100% Saturation 
Maintenance: ~1-2 Months
Life Expenctancy: 1 year 
---

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "do",          # string
  data_type: "%Sat",   # string -- percent saturation
  data_value:          # float
}
```
</div>

## JSON Analog

<div class="code-example" markdown="1">
```json
{
  name: "do",       # string
  data_type: "V",   # string -- Volts
  data_value:       # float
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
