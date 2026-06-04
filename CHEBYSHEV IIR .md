## EXP NO: 4	DESIGN OF DIGITAL CHEBYSHEV IIR FILTER

## DATE :

## AIM:

To design a digital Chebyshev filter using bilinear method satisfying the constraints using matlab. Assume T=1 sec

0.8 ≤│H(w)│≤ 1.0               ; 0 ≤w ≤ 0.2 π
                                                      │H(w)│≤  0.2              ; 0.32 ≤ w ≤ π

## ALGORITHM:
	Start the  matlab software
	Assign the variable for pass band ripple ,stop band ripple, pass band and stop band frequency
	Determine the order of filter using the required formula.
	Find the filter co-efficient a and b
	Assign the time and amplitude
	Plot the magnitude and phaseangle.
	Give the x labe land ylabel and title it
	Save and run the program.

## PROGRAM:
```
clc;
clear;
close all;

% Specifications
AP = 0.8;              % Gain at passband edge frequency
AS = 0.2;              % Gain at stopband edge frequency
PEF_D = 0.2*pi;        % Passband edge digital frequency
SEF_D = 0.32*pi;       % Stopband edge digital frequency
T = 1;                 % Sampling time

% Passband and stopband attenuation in dB
alpha_P = -20*log10(AP);
alpha_S = -20*log10(AS);

% Prewarping of digital frequencies
PEF_A = (2/T) * tan(PEF_D/2);
SEF_A = (2/T) * tan(SEF_D/2);

% Find filter order and cutoff frequency
[N, CF] = cheb1ord(PEF_A, SEF_A, alpha_P, alpha_S, 's');

% Normalized Transfer Function
[Bn, An] = cheby1(N, alpha_P, 1, 's');
Hsn = tf(Bn, An)

% Unnormalized Transfer Function
[B, A] = cheby1(N, alpha_P, CF, 's');
Hs = tf(B, A)

% Impulse Invariant Transformation
[num, den] = impinvar(B, A, 1/T);

% Digital Transfer Function
Hz = tf(num, den, -1)

% Frequency Response
w = 0:pi/16:pi;
Hw = freqz(num, den, w);

% Magnitude Response
Hw_mag = abs(Hw);

% Plot
plot(w/pi, Hw_mag, 'k');
grid on;

title('Magnitude Response of Chebyshev Lowpass Filter');
xlabel('Normalized Frequency (\omega/\pi)');
ylabel('Magnitude');
```
## OUTPUT

<img width="1393" height="571" alt="Screenshot 2026-06-04 085321" src="https://github.com/user-attachments/assets/04e2e211-22a2-4d4f-8d3f-a278d2d1dc1b" />




##  RESULT:

Thus,the digital Chebyshev filter with the given specifications was designed using MatLab.
 
