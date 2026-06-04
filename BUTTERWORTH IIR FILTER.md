## EXP NO:03	DESIGN OF DIGITAL BUTTERWORTH IIR FILTER 
## DATE :
## AIM:

To design a digital Butterworth filter using bilinear method satisfying the constraints using matlab. Assume T=1 sec

		          0.707 ≤│H(w)│≤ 1.0        ; 0 ≤w ≤ 0.2 π
                                             │H(w)│≤  0.08     ; 0.4π ≤ w ≤ π

## ALGORITHM:
	Start the matlab software
	Assign the variable for pass band ripple ,stop band ripple, pass band and stopband frequency
	Determine the order of filter using the required formula.
	Find the filter co-efficient a and b
	Assign the time and amplitude
	Plot the magnitude and phase angle.
	Give the x label and ylabel and title it
	Save and run the program

## PROGRAM:
```
clc;
clear;
close all;

% Specifications
AP = 0.707;          
AS = 0.08;           
PEF_D = 0.2*pi;      
SEF_D = 0.4*pi;      
T = 1;               

% Passband and stopband attenuation in dB
alpha_P = -20*log10(AP);
alpha_S = -20*log10(AS);

% Prewarping of digital frequencies
PEF_A = (2/T) * tan(PEF_D/2);
SEF_A = (2/T) * tan(SEF_D/2);

% Find filter order and cutoff frequency
[N, CF] = buttord(PEF_A, SEF_A, alpha_P, alpha_S, 's');

% Normalized Transfer Function
[Bn, An] = butter(N, 1, 's');
Hsn = tf(Bn, An)

% Unnormalized Transfer Function
[B, A] = butter(N, CF, 's');
Hs = tf(B, A)

% Bilinear Transformation
[num, den] = bilinear(B, A, 1/T);

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

title('Magnitude Response of Butterworth Lowpass Filter');
xlabel('Normalized Frequency (\omega/\pi)');
ylabel('Magnitude');
```

## OUTPUT
<img width="1388" height="590" alt="Screenshot 2026-06-04 082304" src="https://github.com/user-attachments/assets/53906b40-6e2a-4f84-889a-cc9047231043" />



 






## RESULT:

Thus, digital Butterworth IIR filter with the given specifications was designed using MatLab.
 
