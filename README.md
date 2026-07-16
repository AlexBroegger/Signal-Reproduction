# General idea of the Signal Reproduction

Create a signal with two known sinusoid voltages, use an ADC to feed into an FPGA, which implements a FFT. Using the internal DAC, reconstruct one of the sinusoids present in the measured voltage.

![imageblock](https://github.com/AlexBroegger/Signal-Reproduction/blob/main/FIGS/blockdiagram.png)

From the figure, it can be seen that we have a voluntary sinusoid voltage source. The voltage source is fed into the ADC, which converts it into a digital reconstruction of the analogue sinusoids. This makes it possible to process it on the FPGA, which will be running a discrete version Fourier Transform. The FPGA will then, using its internal DAC, output one or both of the sinusoid components present in the original signal. 

# Initial requirements and problem analysis

The main purpose of this mini-project, is to accurately repoduce sinusoidal signals, specifically represented by voltages. By reproduction, it is meant that the amplitude, and the frequency of the signal is accurately matched to the original component.

The idea is also to make it modular, meaning that any sinusoidal signal shall be able to be processed. Here, one limitation comes in. The FPGA (CMOD A7-35T) handling the processing, and the DAC, can only handle voltage levels of 0-3.3V. This means the input need to be stepped down, and then stepped up, before and after the FPGA. The FFT is a linear process, which means that multiplying the signal before and after, should theoretically not shift or alter the sinusoidal components. 

Another problem comes to mind when considering the modularity. Usually in ADCs, there is a trade off between resolution, and the sampling speed. This means it is important to recognize what the most important property is. It is also important to relate this to the possible downscaling of signals. If the voltage level is stepped down incorrectly, we can clip the signal, producing errors in the DFT. If we downscale the signal too much, we also lose detail, since a signal with a lower amplitude, requires smaller voltage steps (Because the FPGA's 3.3V logic fixes the ADC step size, scaling the input down only uses fewer ADC levels, reducing effective resolution and worsening signal-to-noise ratio.).

It should be noted that the FPGA does include an internal ADC, but out of curiosity, it has been chosen that i will construct my own.

The main things to consider, when handling the trade-offs for the ADC, is defining the range of signals we need to process, in relation to the properties of the DFT (Which will most likely be implemented as an FFT). The lab equipment that can be used for the project includes a 1 Hz - 50 MHz generator, with a $\pm 10 V$ range, and a 70 MHz oscilloscope. This means for practical reasons we are limited by the generator, meaning only signals in the frequency range 1 Hz - 50 MHz are initially considered.

With respect to the range, and the nyquist sampling theorem, we must sample at atleast 100 MHz. This is a problem, because this introduces the possibilty for aliasing, through noise components in the original signal. In fact we also know that the generator might produce small harmonic signals, when the transistors are pushed, and it becomes nonlinear (more theory coming soon). This means some of the noise is folded back, generating false frequencies. Therefore a filter is needed to quite harshly attenuate signals above 50 MHz. 
(Note: the cutoff-frequency can be shifted right by oversampling). 

At higher frequencies, implementation can be cumbersome, due to high-frequency parasitics such as inductances or capacitances in the implementation medium. For example, a bread board is not well suited for such high frequencies. Due to the project being an introduction to PCB and ADC design, some weight should be put on having a nicer learning experience.

For the DFT, the main concerns are primarily how accurate we want the frequency bins to be, or what size they should have. The bin size is defined as $f_s/N$, where N is number of samples. The number of samples we obtain is limited by how much memory we have on our FPGA. The FPGA has 50 BRAMs, with 36 Kb each. 

Another concern of the DFT, is smearing. If our sampling doesnt exactly contain the number of samples, smearing of the edges occurs, which means we get fake frequencies to account for the cutoff. This is because an assumption of the DFT is that we have a periodic signal, if we instead dont produce this, it creates errors. It's kind of like having the shutter on a camera open for too long, it will create a blurry image.

## Conclusion of initial requirements





# General system design

# Test

# Conclusion
