---
layout: default
title: Dissolved Oxygen
parent: Atlas
grand_parent: Sensors
permalink: /docs/sensors/atlas/do/
---

# Dissolved Oxygen Sensor
{: .no_toc }
## Atlas
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

The dissolved oxygen probe reads the partial pressure of oxygen. 
The partial pressure of oxygen in the atmosphere is compared to the partial pressure of oxygen in the water, this is the percent satuartion method. 
 


Name: Gravity Analog Dissolved Oxygen Kit

Link: https://atlas-scientific.com/kits/gravity-analog-do-kit/ 

Calibration: Calibrated against air. Dip probe in water, and wave probe in air. 

Type: Analog 

Operational Range: 1 to 50 degrees C

Unit: % Saturation 

Range: 1% t0 100% Saturation 

Maintenance: ~6 Months

Life Expenctancy: 2.5 years 

---
## Maintenace 

Best practice is to replace the electrolyte solution and membrane cap every 6-12 months. 

When the electrolyte solution is depleted, the readings will be very low.

The membrane cap will need to be replaced if damaged, scratched, or ripped. 


Refilling the Electrolyte Solution:

Unscrew the membrane cap and pour out any remaining solution. Inject electrolyte solution into the membrane cap until it is filled to the top. Screw the membrance cap back. Rinse the probe with water. 


Cleaning:

The sides of the probe can be lightly brushed with a soft toothbrush. 
The membrane can be rinsed with a mild bleach solution.  


## Calibration 
There is no set schedule for recalibration. 

Best practice is to recallibrate every 6 months. 

To calibrate, 


## Percentage Saturation Equation

(Reading in water/Calibration value) * 100 = Percent Saturation

Calibration value is the reading in air.

## Note on the Units
This sensor is designed to read percent saturation only. Reading oxygen in mg/L is more complex and can not be done with this particular device. 

## Note on the default saturation
Default constant is 440 since that is the typical oxygen levels in air. 

## JSON 
## TBD
<!-- <div class="code-example" markdown="1">
```json
{
  name: "do",          # string
  data_type: "%Sat",   # string -- percent saturation
  data_value:          # float
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
