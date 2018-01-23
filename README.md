# Introduction to Pulse Width Modulation (PWM)

## Objective

The objective of this lab is a learn the basics of an example that uses Pulse Width Modulation to control the brightness intensity of an LED.

## Setup the Rotary Angle Sensor
## Hardware requirements

### Grove\*

Module | Pin
--- | ---
Rotary Angle Sensor | A0
LED | D3

![](./images/action.png) Connect **Grove Rotary Angle Sensor** to analog pin **A0** of the Grove Base Shield.

![](./images/action.png) Connect **Grove LED** to digital pin **D3** of the Grove Base Shield.

# PWM - Pulse Width Modulation

PWM stands for (Pulse Width Modulation)[https://en.wikipedia.org/wiki/Pulse-width_modulation]. The idea is that digital signal can attenuate power/intensity by varying the amount of time they are ON or OFF. For example, if an LED is turning ON 1000 times per second, the human eye will perceive it as always ON. However, if it cycles between ON and OFF 100 times per second, then we will still perceive it as always ON _but only half as bright_.

The reason is that 1000 times per second is much faster than the human eye can perceive. However, if half of the time it is OFF then only 1/2 of light be emitted by the LED.

Let's see this in action.

# A Caution about PWM Pins
Not every Digital GPIO pin on the Up2 board is able to use PWM. Be sure that you are on **D3** and not a different PIN.

## PWM using the Arduino API
Create a new project
```c
// Setup instructions
// A2 - Grove Rotary Angle Sensor
// D3 - LED
#define SUBPLATFORM_OFFSET 512
#define KNOB_PIN SUBPLATFORM_OFFSET + 2
#define LED_PIN SUBPLATFORM_OFFSET + 3

mraa_pwm_context pwm;
mraa_aio_context aio;

// The setup function runs once when
// you press reset or power the board.
void setup() {
  mraa_add_subplatform(MRAA_GROVEPI, "0");

  // A2 rotary
  aio = mraa_aio_init(KNOB_PIN);

  // D3 LED (supports PWM)
  pwm = mraa_pwm_init(LED_PIN);

  // Initialize the serial monitor
  DebugSerial.begin(115200);
}

// The loop function runs continuously
void loop() {
  mraa_pwm_write(pwm, mraa_aio_read(aio)/1023.0);
  //DebugSerial.println(mraa_get_version());
  delay(1);  // Wait for 1 millisecond
}
```

This program will get the raw value from the rotary angle sensor, a number between 0 and 1023, and normalize it by dividing it by 1023 then the PWM write cycle is set to this value, a number between 0 and 1.

If the PWM duty cycle is set to 0.5 or 50% then the LED will be ON about half of the time and off half of the time. However, the change to ON from OFF and back happens so quickly that the light appears to be a half intensity.

# Lab Answers
Find the (complete solution to this lab)[https://create.arduino.cc/editor/danielholmlund/6b857743-df59-4877-8d9a-32b24f21143b/preview] in the Arduino Create environment.

https://create.arduino.cc/editor/danielholmlund/6b857743-df59-4877-8d9a-32b24f21143b/preview

## Additional resources
Information, community forums, articles, tutorials and more can be found at the [Intel Developer Zone](https://software.intel.com/iot).

For reference code for any sensor/actuator from the Grove* IoT Commercial Developer Kit, visit [https://software.intel.com/en-us/iot/hardware/sensors](https://software.intel.com/en-us/iot/hardware/sensors)
