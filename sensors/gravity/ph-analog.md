---
layout: default
title: PH Sensor
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/ph/
---

# Analog PH Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A PH sensor.

Name: Gravity: Analog pH Sensor/Meter Kit V2

Link: https://www.dfrobot.com/product-1782.html

Calibration: Calibrated against buffer solutions provided in the kit. 

Type: Analog 

Operational Range: 5 to 60 degrees C

Unit: N/A

Range: 1 to 14 

Life Expenctancy: ~0.5 year 

---
## Maintenance

### Calibration
There is no set schedule for calibrating. The length of time between calibration is determined by how often the probe is used. It is typically done once a month. More if needed. 


## Note
It is not recommended to submerge the probe in the measuring liquid for long periods of time. 

The probe should be rinsed and cleaned with distilled water, then placed back into the protective sleeve along with a solution of 3M KCl for storage. 

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "ph",       # string
  data_type: "pH",  # string
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
