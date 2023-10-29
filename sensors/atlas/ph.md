---
layout: default
title: PH
parent: Atlas
grand_parent: Sensors
permalink: /docs/sensors/atlas/ph/
---

# PH Sensor
{: .no_toc }
## Atlas
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

The Atlas pH (potential of Hydrogen) probe measures the hydrogen ion activity in a liquid.
At the tip of a pH probe is a glass membrane. This glass membrane permits hydrogen
ions from the liquid being measured to defuse into the outer layer of the glass, while
larger ions remain in the solution. The difference in the concentration of hydrogen ions
(outside the probe vs. inside the probe) creates a VERY small current. This current is
proportional to the concentration of hydrogen ions in the liquid being measured.

[More Info](https://files.atlas-scientific.com/pH_EZO_Datasheet.pdf)


Name: pH Kit

Link: https://atlas-scientific.com/kits/ph-kit/  

Calibration: Calibrated against buffer solutions provided in the kit

Type: Analog 

Operational Range: -55 to 99 degrees C

Unit: N/A

Range: 1 to 14 

Maintenance: ~1 year

Life Expenctancy: 2.5 years 

---

## Maintenance

### Cleaning

Soft coatings can be removed with stiring the probe in water or rinsing with a squeeze bottle. 
Harder coatings can be cleaned by stiring the probe in a light bleach solution. 

### Reconditioning
Reconditioning is required when the probe has been stored incorrectly or when the probe has dried out. 
The manufactuer recommends their [pH probe reconditioning kit](https://atlas-scientific.com/calibration-solutions/ph-probe-reconditioning-kit/)

## Calibration
There is no set schedule for recalibration. If the probe is being used in an environment with weak levels of acids and bases, the best practice is to recallibrate every 6 months. If the prove is being used in an environment with strong acids and bases, the best practice is to recallibrate monthly. 

Note: the calibration solution is no long suitable after 20 minutes and needs to be disposed of.

## Notes
When placing probe in water, gently tap the sensor to ensure there are no air bubbles trapped in the prob

## JSON 
#### Publish Topic: device/reading/sensor/ph
<div class="code-example" markdown="1">

```json
{
  value:       # float
}
```
</div>

#### Subscribe Topic: device/config/sensor/ph
<div class="code-example" markdown="1">

```json
{
  state:          # binary
}
```
</div>

## TBD
<!-- <div class="code-example" markdown="1">
```json
{
  name: "ph",       # string
  data_type: "pH",  # string
  data_value:       # float
}
```
</div> -->

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
