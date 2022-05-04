# Atmega Audio Visualization

Real-Time Audio Visualization for the Atmega2560

Finished as the final project for ECE 372A at the University of Arizona.
Two libraries were used to significantly reduce developemnt time.

Hardware Used:
1. Analog Devices AD7920 12-bit ADC
2. WS2818B LED Strip

Libraries Used:
1. fix_fft Fast Fourier Transform library
2. Arduino SPI library

Project Design:
1. Audio input amplified by TL071 op-amp. Voltage divider used to properly sample AC audio with the AD7920 ADC.
2. AD7920 read through SPI to create 64 samples (roughly; error neglegible) at a sampling rate of 44.1kHz.
3. AD7920 12-bit value down-converted to 8-bits and fed into fix_fft library.
4. 8-bit real and imaginary value fix_fft output arrays used to compute frequency amplitudes.
5. Frequency amplitude array used to determine the brightness of 32 LED sections (64 samples / 2).
   Each section represents a specific frequency and they all have a unique color.
   Each section decreases in size as frequency it represents increases.
   These 32 sections are mirrored accross the center of the LED strip.
6. AVR assembly code used to "bit-bang" the final data to the WS2818B LEDS.
