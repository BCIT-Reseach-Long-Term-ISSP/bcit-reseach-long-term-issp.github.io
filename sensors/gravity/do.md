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

Calibration: Single-point and two-point. 

Type: Analog 

Operational Range: 1 to 40 degrees C

Unit: % Saturation 

Range: 1% t0 100% Saturation 

Maintenance: ~1 Month

Life Expenctancy: 1 year 

---
## Calibration
The probe needs to be calibrated if being used for the first time. Also needs to be calibrated approximately every 6 months during use. There are two types of callibration. Single point and two-point

### Single Point Calibration
Single point calibration is suitable for when the temperature of the solution is stable. There are two ways to do single point calibration, exposing the wet probe to the air and immersing the probe in saturated dissolved oxygen water. 

#### Exposing wet probe to the air
1. Prepare the probe.
2. Dip the probe in water and shake off excess water.
3. Wave the probe in air.
4. Wait for the output voltage to stablize. Record the voltage. 

#### Immersing the probe in saturated dissolved oxygen water
1. Prepare the probe.
2. Prepared a cup of purified water and use one of the following methods.

  a. Use a stirrer or an eggbeater to continously stir for 10 minutes.

  b. Use an air pump to continously inflate the water for 10 minutes.

3. Stop stirring/beating/pumping.
4. Put the prob into the water.
5. Stir/beat/pump the water slowly to move the water while not creating any air bubbles.
6. Wait for the output voltage to stablize. Record the voltage. 


### Two Point Calibration 
Two point calibration is suitable for when the temperature flucates.

Prepare two cups of filtered water. Put one cup in the refrigerator to allow water to cool down and warm one cup up to below 40 degrees. 

For each cup of water, do the following:
1. Prepare the probe.
2. Use one of the following methods to saturate the the cup of water. 

    - Use a stirrer or an eggbeater to continously stir for 10 minutes.

    - Use an air pump to continously inflate the water for 10 minutes.
3. Stop stirring/beating/pumping.
4. Put the probe into the water.
5. Stir/beat/pump the water slowly to move the water while not creating any air bubbles.
6. Wait for the output voltage to stablize. Record the voltage. 


## Notes


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
