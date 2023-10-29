---
layout: default
title: Electrical Conductivity
parent: Atlas
grand_parent: Sensors
permalink: /docs/sensors/atlas/ec/
---

# Electrical Conductivity Sensor
{: .no_toc }
## Atlas
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

An electrical conductivity sensor measures the electrical conductivity in a solution.
Inside the probe, there are two electrodes positioned opposite from eachother. An AC voltage is applied to the electrodes which causes cations to move to the negatively charged eletrode and the anion to move to the positively charged eletrode. 
The more free electrolutes the liquid contains, the higher the electrical conductivity. 
It works by measuring electrical current of the solution between two graphite plates. 

[More Info](https://files.atlas-scientific.com/EC_EZO_Datasheet.pdf)

Name: Conductivity K 0.1 Kit 

Link: https://atlas-scientific.com/kits/conductivity-k-0-1-kit/

Calibration: Calibrated against buffer solutions provided in the kit

Type: Analog 

Operational Range: 1 to 50 degrees C

Unit: µs

Range: 0.07µS/cm to 50,000µS/cm

Maintenance: ~6 Months

Life Expenctancy: 2.5 years 

---
## Maintenance

### Cleaning:

For soft coatings, the probe can be cleaning by light brushing. 

For hard coatings, the recommended method is using the [cleaner from Atlas Science] (https://atlas-scientific.com/calibration-solutions/e-c-probe-cleaner/) 

## Calibration 
The grpahite plates in this sensor do not go bad, nor do they change. No additional calibration is needed after initial calibration.

## Operational Tips
The entried conducting area must be submerged in order to get accurate readings. 

![Diagram](/sensors/assests/ec_probe_submerged.jpg)

## JSON
Publish Topic: device/reading/sensor/cond
<div class="code-example" markdown="1">

```json
{
  value:           # float
}
```
</div>

Subscribe Topic: device/config/sensor/cond
<div class="code-example" markdown="1">

```json
{
  state:          # binary
}
```
</div>

## TBD

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
