# General idea of the Signal Reproduction

Create a signal with two known sinusoid voltages, use an ADC to feed into an FPGA, which implements a FFT. Using the internal DAC, reconstruct one of the sinusoids present in the measured voltage.

# Initial requirements

The main purpose of this mini-project, is to accurately repoduce sinusoidal signals, specifically represented by voltages. By reproduction, it is meant that the amplitude, and the frequency of the signal is accurately matched to the original component.

The idea is also to make it modular, meaning that any sinusoidal signal shall be able to be processed. Here, one limitation comes in. The FPGA (CMOD A7-35T) handling the processing, and the DAC, can only handle voltage levels of 0-3.3V. This means the input need to be stepped down, and then stepped up, before and after the FPGA. The FFT is a linear process, which means that multiplying the signal before and after, should theoretically not shift or alter the sinusoidal components. 

Another problem comes to mind when considering the modularity. Usually in ADCs, there is a trade off between resolution, and the sampling speed. This means it is important to recognize what the most important property is. It is also important to relate this to the possible downscaling of signals. If the voltage level is stepped down incorrectly, we can clip the signal, producing errors in the DFT. If we downscale the signal too much, we also lose detail, since a signal with a lower amplitude, requires smaller voltage steps.

It should be noted that the FPGA does include an internal ADC, but out of curiosity, it has been chosen that i will construct my own.

The main things to consider, when handling the trade-offs for the ADC, is defining the range of signals we need to process, in relation to the properties of the DFT (Which will most likely be implemented as an FFT). The lab equipment that can be used for the project includes a 1 Hz - 50 MHz generator, with a $\pm 10 V$ range, and a 70 MHz oscilloscope. This means for practical reasons we are limited by the generator, meaning only signals in the frequency range 1 Hz - 50 MHz are initially considered.

With respect to the range, and the nyquist sampling theorem, we must sample at atleast 100 MHz. This is a problem, because this introduces the possibilty for aliasing, through noise components in the original signal. In fact we also know that the generator might produce small harmonic signals, when the transistors are pushed, and it becomes nonlinear (more theory coming soon). This means some of the noise is folded back, generating false frequencies. Therefore a filter is needed to quite harshly attenuate signals above 50 MHz. 
(Note: the cutoff-frequency can be shifted right by oversampling). 

At higher frequencies, implementation can be cumbersome, due to high-frequency parasitics such as inductances or capacitances in the implementation medium. For example, a bread board is not well suited for such high frequencies. Due to the project being an introduction to PCB and ADC design, some weight should be put on having a nicer learning experience.

## Conclusion of initial requirements





# General system design

# Test

# Conclusion
