# Introduction to Pulse Width Modulation (PWM)

## Objective

During the first step in this lab, you will compare a small analog program using the Arduino APIs to an program using the UPM Grove Temperature libary.

You will write code in C to connect a rotary angle sensor using upm library and printing the values to the serial monitor.

## Setup the Rotary Angle Sensor
## Hardware requirements

### Grove\*

Module | Pin
--- | ---
Rotary Angle Sensor | A0
LED | D3

![](./images/action.png) Connect **Grove Rotary Angle Sensor** to analog pin **A0** of the Grove Base Shield.

![](./images/action.png) Connect **Grove LED** to digital pin **D3** of the Grove Base Shield.

## PWM using the Arduino API
Create a new project
```c
//#include "mraa-dynamic.h"
//#include "mraa.h"


// Setup instructions
// A2 - Grove Rotary Angle Sensor
// D3 - LED

mraa_pwm_context pwm;
mraa_aio_context aio;

// the setup function runs once when you press reset or power the board
void setup() {
  mraa_add_subplatform(MRAA_GROVEPI, "0");

  aio = mraa_aio_init(514); //A2 rotary
  pwm = mraa_pwm_init(515); //D3 LED (supports PWM)
  DebugSerial.begin(115200);
}

// the loop function runs over and over again forever
void loop() {
  mraa_pwm_write(pwm, mraa_aio_read(aio)/1023.0);
  DebugSerial.println(mraa_get_version());
  delay(50);                       // wait for a second
}
```

This program will get the raw value from the sensor and display it as a number between 0 and 1023.  

There are a number of additional examples available for reference as [how-to-code-samples](https://github.com/intel-iot-devkit/how-to-code-samples) on Github.

## Additional resources

Information, community forums, articles, tutorials and more can be found at the [Intel Developer Zone](https://software.intel.com/iot).

For reference code for any sensor/actuator from the Grove* IoT Commercial Developer Kit, visit [https://software.intel.com/en-us/iot/hardware/sensors](https://software.intel.com/en-us/iot/hardware/sensors)
