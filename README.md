# COE411 Lab 2 - Analog Sensors and Interactive Light Monitor

## Project Description

This project uses an STM32 Nucleo-L476RG, a joystick, and a photoresistor to make an interactive light monitoring system.

The joystick X-axis is used to control the light threshold. The joystick button is used to switch the system between ARMED and DISARMED.

The photoresistor measures the light level, and the onboard LED is used as the alarm.

The system also sends the current values through USART2 so they can be seen on a serial terminal.

## Hardware Used

- STM32 Nucleo-L476RG
- Joystick module
- Photoresistor module
- Breadboard
- Jumper wires

## Connections

- Joystick VRx -> PA0 / ADC1_IN5
- Joystick VRy -> PA1 / ADC1_IN6
- Photoresistor analog output -> PA4 / ADC1_IN9
- Joystick switch -> PB6
- Onboard LED LD2 -> PA5
- USART2 TX -> PA2
- USART2 RX -> PA3
- All modules are powered using 3.3 V
- All components use the same GND

## How the System Works

The STM32 reads the joystick and photoresistor using ADC1.

The joystick X value is used to set a threshold between 0 and 4095.

When the joystick button is pressed, the system changes between ARMED and DISARMED.

When the system is DISARMED, the LED stays OFF.

When the system is ARMED, the light sensor value is compared with the threshold.

Depending on the light level and the selected threshold, the LED turns ON or OFF.

The system also uses debouncing and hysteresis to make the behavior more stable.

## UART Output

The system sends the following values through USART2:

- Light sensor value
- Threshold value
- System state
- Alarm state

Example:

LIGHT=2863 THR=1984 STATE=ARMED ALARM=OFF

## Debouncing

Debouncing makes the button more reliable because one physical button press can quickly switch between HIGH and LOW multiple times.

The 250 ms lockout makes sure that one real button press only changes the system state once.

Without debouncing, one button press could be detected as multiple presses.

## Hysteresis

Hysteresis makes the light alarm more reliable because the sensor value can slightly move up and down when it is close to the threshold.

Two different switching limits are used around the threshold.

This stops the LED from turning ON and OFF very quickly when the light value is close to the threshold.

## Development Stages

The project was developed in three main stages.

### 1. Base ADC Readings

- Read the joystick X value.
- Read the joystick Y value.
- Read the photoresistor value.
- Display the readings through UART.

### 2. Interactive Monitor

- Added threshold control using joystick X.
- Added ARMED and DISARMED states.
- Added joystick button control.
- Added LED alarm control.
- Added UART output for the threshold and system state.

### 3. Refinements

- Added button debouncing.
- Added hysteresis.
- Added alarm state to the UART output.
- Improved the stability of the system.
