# STM32F4_SPECTRUM_WS2812

Major shout out, credit to, and recognition of, Tony DiCola for his work in the Adafruit Spectrum Project and to Lars Boegild Thomsen for his tutorial on using WS2812 on the STM32.

Other credit for informative tutorials that provided excellent resources are ControllersTech, Phil's Lab, and STM. 

This project takes the Spectrum Project, removes it from the Ardunio Framework, modifies parts of it, then develops it for the STM32F405. The audio and LED drivers needed to be developed. To make this as fun and efficient as possible, it then uses the DMA and Timers so that the processor does as little as possible and has plenty of idle time.

General architecture:
	• Take an audio sample into an ADC and run an FFT on the sample.
	• Use the FFT results and convert them into spectrum for an LED.
	• Convert them into duty cycles for a PWM.
	• Output them through a digital output for a string of LEDs.

[AUDIO INPUT]→[ADC]→[DMA]→[FFT]→[LED DATA CONVERSION]→[DMA]→[DIGITAL OUTPUT]→[LEDS]

Using an STM32F405, the ADC reads into a DMA buffer.

When complete, it copies to an array and flags for the FFT to be conducted using the array data. 

The MCU then runs the FFT. 

The output of the FFT is then put through a windowMean program the that reassigns the data from the FFT size to the quantity of LEDs. 

Once complete, each LED now has a color and brightness associated/assigned. This is done with 3 colors (GRB) and a brightness of 0-255. 

The LED data color and brightness data has to be converted into specific LED communication data.

This is sent to the DMA and then then transmitted via the digital output to the WS2812 (LED).
