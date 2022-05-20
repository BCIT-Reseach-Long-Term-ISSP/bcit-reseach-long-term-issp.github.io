---
layout: default
title: PH
parent: Grove
grand_parent: Sensors
permalink: /docs/sensors/grove/ph
---

# PH Sensor
{: .no_toc }
## Grove
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A low cost PH sensor. The pH probe measures the hydrogen-ion activity in water-based solutions. 

Name: Grove - PH Sensor Kit (E-201C-Blue)

Link: https://www.seeedstudio.com/Grove-PH-Sensor-Kit-E-201C-Blue-p-4577.html

Calibration: Calibrated against 2 known buffer solutions 

Type: Analog 

Operational Range: 0 to 60 degrees C

Unit: N/A

Range: 1 to 14 

Maintenance: ~1 year

Life Expenctancy: 2 years 

---
## Maintenance 

The probe must be dipped into a buffer solution of pH 7 or distilled water between detecting different solutions.

The electrode can be soak in 4%HF for 3-5 seconds, rinsed with distilled water, then soaked in 3.3mol KCl. 

## Calibration 

Link: https://wiki.seeedstudio.com/Grove-PH-Sensor-kit/

### Materials 
#### Hardware
Grove-PH Sesnor kit
Seeeduino Lotus
2 solutions with known pH 

#### Software 
Arduino IDE

### Calibration Steps
1. Set up the Arduino.
2. Download the demo code from the link in the summary and paste the whole file into the root of the Arduino. 
3. Open the pH_meter_V1_1 with the Arduino IDE.
4. Flash the device. 
5. Place the probe in calibration solution A. Record the voltage.
6. Rinse the probe in distilled water.
7. Place the probe in calibration solution B. Record the voltage. 
8. The formula for k is (pH of solution A - ph of solution B)/(voltage of solution A - voltage of solution B)
9. The formula for Offset is [(pH of solution A + ph of solution B)-k(voltage of solution A + voltage of solution B)]/2
10. Change the Offset value in the code (line 10). 

## Notes
This sensor may not be submerged in liquid for a long period of time. 

When not in use, the probe should be in the sleeve with a solution of 3.3mol KCL.

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
