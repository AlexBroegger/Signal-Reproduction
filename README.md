# General idea of the Signal Reproduction

Create a signal with two known sinusoid voltages, use an ADC to feed into an FPGA, which implements a FFT. Using the internal DAC, reconstruct one of the sinusoids present in the measured voltage.

# Initial requirements

The main purpose of this mini-project, is to accurately repoduce sinusoidal signals, specifically represented by voltages. By reproduction, it is meant that the amplitude, and the frequency of the signal is accurately matched to the original component.

The idea is also to make it modular, meaning that any sinusoidal signal shall be able to be processed. Here, one limitation comes in. The FPGA (CMOD A7-35T) handling the processing, and the DAC, can only handle voltage levels of 0-3.3V. This means the input need to be stepped down, and then stepped up, before and after the FPGA. The FFT is a linear process, which means that multiplying the signal before and after, should theoretically not shift or alter the sinusoidal components. 

Another problem comes to mind when considering the modularity. Usually in ADCs, there is a trade off between resolution, and the sampling speed. This means it is important to recognize what the most important property is. It is also important to relate this to the possible downscaling of signals. If the voltage level is stepped down incorrectly, we can clip the signal, producing errors in the DFT. If we downscale the signal too much, we also lose detail, since a signal with a lower amplitude, and a fixed voltage regulation, means we 

It should be noted that the FPGA does include an internal ADC, but out of curiosity, it has been chosen that i will construct my own. 


# General system design

# Test

# Conclusion
