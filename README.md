# Macro 1862

The CDP1862C was the colour generator IC used in the RCA COSMAC VIP and related systems including the VP590 colour board. This project creates a drop-in discrete logic replacement for the original CDP1862C using modern CMOS components, allowing failed or unavailable chips to be replaced without modifying the host hardware.

The replacement replicates the CDP1862C's core functions:

Crystal oscillator at 7.159090MHz generating the NTSC colour subcarrier frequency
Phase generation producing four quadrature phases (0°/90°/180°/270°) at 3.58MHz for colour encoding
Colour latch capturing the 3-bit RGB pixel data (RED/GREEN/BLUE) from the CDP1802 DMA bus
Chroma encode gating the correct subcarrier phase for each foreground colour — Red at 90°, Green and Blue at 270°
Luminance decode driving the VP590 mixing matrix resistors to set brightness for each colour
Colorburst generation gating the 180° phase during the back porch of each horizontal sync pulse
Background colour cycling through Blue, Black, Green and Red using a 2-bit binary counter clocked during the background region
CLK_OUT at 1.789MHz (7.159MHz ÷ 4) returned to the CDP1802 for display timing

The design is built around a single ATF22V10C PLD (U7) handling all chroma and luminance decode logic, supported by standard 74HC logic for oscillator, phase generation, colour latching, burst gating and background counter functions. The PLD is programmed using equations derived from David S. Madole's DSM1862 project, adapted by Costas Skordis for this implementation.

The complete design fits on a 24-pin DIP footprint compatible with the original CDP1862C socket, requiring no modification to the VP590 board.





