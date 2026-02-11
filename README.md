# STM32F4_SPECTRUM_WS2812

General architecture:
	• Take an audio sample into an ADC and run an FFT on the sample.
	• Use the FFT results and convert them into spectrum for an LED.
	• Convert them into duty cycles for a PWM.
	• Output them through a digital output for a string of LEDs.

[AUDIO INPUT]→[ADC]→[FFT]→[LED DATA CONVERSION]→[DIGITAL OUTPUT]→[LEDS]

Using an STM32F405, the ADC reads into a DMA buffer.

When complete, it copies to an array and flags for the FFT to be conducted using the array data. 

The MCU then runs the FFT. 

The output of the FFT is then put through a windowMean program the that reassigns the data from the FFT size to the quantity of LEDs. 

Once complete, each LED now has a color and brightness associated/assigned. This is done with 3 colors (GRB) and a brightness of 0-255. 

The LED data color and brightness data has to be converted into specific LED communication data that is then transmitted via the digital output.
<img width="747" height="338" alt="image" src="https://github.com/user-attachments/assets/c8d58b69-4be9-4dcc-81b7-7e28ac320fd6" />
