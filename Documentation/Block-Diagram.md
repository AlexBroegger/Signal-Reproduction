The general idea for the total system is shown. The individual blocks will later be expanded upon.

![imageblock](https://github.com/AlexBroegger/Signal-Reproduction/blob/main/FIGS/blockdiagram.png)

From the figure, it can be seen that we have a voluntary sinusoid voltage source. The voltage source is fed into the ADC, which converts it into a digital reconstruction of the analogue sinusoids. This makes it possible to process it on the FPGA, which will be running a discrete version Fourier Transform. The FPGA will then, using its internal DAC, output one or both of the sinusoid components present in the original signal. 
