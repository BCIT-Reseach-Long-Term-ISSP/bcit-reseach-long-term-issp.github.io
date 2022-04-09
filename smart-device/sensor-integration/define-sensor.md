---
layout: default
title: Add Sensor
parent: Sensor Integration
grand_parent: Smart Device
---

# How to Define a Sensor



This section provides an overview of how to define a new sensor for use in the smart device.

It should be noted that there is much to improve upon in the current design.
As of now (April 8, 2022) the project has been sidelined, and will resume sometime
in May, 2022. Thus, it is reasonable to assume that significant changes will be made
in the coming months.

In the code-design's current state, any one of the existing sensor objects
can be easily copied and modified to support another sensor with only minor changes. 
This comes with the exception that such a sensor derives its values from means of
analog measurement - like the existing sensors in the project already.

The Sensor source prototypes, structures, and function should first be presented in 
order to get a more thorough understanding of the current design before moving forward...

```c
/**
 * Generic function pointer for Analog/Digital read.
 */
typedef float (* Measure) (void *);


/**
 * Generic function pointer for Analog/Digital conversion
 * to sensor specific value. (e.g. pH, Turbidity, etc.)
 */
typedef float (* Convert) (void *);


/**
 * Known types of sensors for the smart-device
 * as of Mar. 31, 2022.
 */
enum sensor_type
{
    PH,
    TURB,
    DO,
    EC,
    TDS,
    W_PRESSURE,
    TEMP
};


/**
 * Sensor object.
 *
 * @property pin:           Analog/Digital input pin the sensor is connected to.
 * @property sensor_type    Sensor type (specified by enum sensor_type).
 * @property scale-factor   Value applied to the s_value for calibration.
 * @property value_s        Converted sensor-specific reading.
 * @property value_adc      Value returned from the ADC reading.
 * @property sensor_type    Converted value from ADC.
 */
typedef struct sensor * Sensor;
struct sensor
{
    int pin;
    float value;
    float value_adc;
    float scale_factor;
    unsigned int type;

    Measure measure;
    Convert convert;
};


/**
 * Initialize Sensor object.
 *
 * Initializes sensor object, allocating necessary
 * memory and setting all other values to 0.
 *
 * If function fails to allocate memory,
 * NULL is returned.
 *
 * @param sensor_type   Sensor type specified by enum sensor_type
 * @param pin           Connected analog input pin.
 * @return Pointer to Sensor object.
 */
Sensor sensor_init(int pin);


/**
 * Destroy Sensor object.
 *
 * Destroys a Sensor object, freeing
 * any allocated memory and setting all
 * remaining values to 0 or NULL.
 *
 * @param sensor
 */
void sensor_destroy(Sensor sensor);


/**
 * Take a measurement with a Sensor object.
 *
 * Takes a measure from an initialized sensor
 * at the analog pin specified by the sensor's
 * <pin> attribute.
 *
 * Stores the measured value from the analog
 * or digital input.
 *
 * @param sensor    A sensor object.
 * @return Measured value in volts.
 */
float measure(void * this);
```

If one wishes to add a new sensor, they must only pass the designated
analog or digital input pin and an argument to <strong>sensor_init()</strong>.
This function will allocate the necessary memory and initialize all remaining
variables - returning a pointer to the newly created <strong>Sensor</strong> object.

Once the Sensor has been initialized, the implementer must assign an analog/digital
read function to the Sensor member function ( <strong>sensor->measure()</strong> ).
Additionally, a **Convert()** function should be passed that can be used to apply
a conversion from the **sensor->value_adc** to a "real-world" value related to
the actual type of sensor being used. Both of these functions accepts a generic
pointer (void *) and return a float - with the difference in names existing only
for semantic purposes.

The following example is provided for use in creating a sensor that measures
unicorn hair  (_smidgens/quepite<sup>2</sup>_).

```c
#define PIN_UNICORN_HAIR 1

int main()
{
    float value_adc, value_s;
    Sensor * sensor;
    
    /* Initialize the sensor with designated input pin */
    sensor = init_sensor(PIN_UNICORN_HAIR);
    
    /* Assign measure() member function to some existing read function. */
    sensor->measure = (Measure) my_analog_read_func;  // cast to Measure func. type.
    
    /* Assign convert() member function to some existing conversion function. */
    sensor->convert = (Convert) convert_smidgens;  // cast to Convert func. type.
    
    /* Run measure function */
    value_adc = sensor->measure(sensor);
    printf("Value is also stored in the object: %f\n", sensor->value_adc);
    
    /* Run convert function */
    sensor->convert(sensor);
    printf("Value is also stored in the object: %f\n", sensor->value_s);
    
    return 0;
}
```

{: .fs-6 .fw-300 }