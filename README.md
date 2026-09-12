# Code-Lab-2-Embedded
STM32 interactive light monitor using ADC, joystick, photoresistor, UART, debouncing, and hysteresis.

# COE411 Lab 2 - Analog Sensors and Interactive Light Monitor

## Project Description

This project uses an STM32 Nucleo-L476RG, a joystick, and a photoresistor to make an interactive light monitor.

The joystick X-axis is used to control the light threshold. The joystick button is used to switch the system between ARMED and DISARMED. The photoresistor measures the light level, and the onboard LED is used as the alarm.

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

When the system is ARMED, the light sensor value is compared with the threshold and the LED turns ON or OFF depending on the light level.

Debouncing is used so that one real button press is only detected once.

Hysteresis is used so that the LED does not keep switching ON and OFF when the light value is close to the threshold.

## UART Output

The system sends the following values through USART2:

- Light sensor value
- Threshold value
- System state
- Alarm state

Example:

LIGHT=2863 THR=1984 STATE=ARMED ALARM=OFF

## Debouncing

Debouncing makes the button more reliable because one physical press can quickly switch between HIGH and LOW more than once. The 250 ms lockout makes sure that one real press only changes the system state once.

## Hysteresis

Hysteresis makes the light alarm more reliable because the sensor value can move slightly up and down when it is close to the threshold. Using two different switching limits stops the LED from turning ON and OFF very quickly.

## Development Stages

The project was developed in three main stages.

### 1. Base ADC Readings

- Read the joystick values.
- Read the photoresistor value.
- Display the sensor readings through UART.

### 2. Interactive Monitor

- Added the threshold using joystick X.
- Added ARMED and DISARMED states.
- Added LED control.

### 3. Refinements

- Added button debouncing.
- Added hysteresis to make the LED more stable.
