## EXP NO 05: 	DESIGN OF FIR FILTER USING RECTANGULAR WINDOWS 
## DATE :15.5.26

## AIM:

To design a linear phase FIR band stop filter to reject frequencies in the range 0.4π  to 0.65π rad/sec using rectangular window , by taking 7 samples of window sequence using matlab.
## ALGORITHM:
	Assign the variable for pass band ripple ,stop band ripple, pass band and stop band frequency
	Determine the order of filter using the required formula.
	Find the filter co-efficient b
	Assign the time and amplitude
	Plot the magnitude and phase angle for LPF.HPF,BPF&BSF.
	Give the x label and ylabel and title it.
## PROGRAM:
```
clc;
clear;
close all;

% Cutoff frequencies
Wc1 = 0.4*pi;
Wc2 = 0.65*pi;

% Filter length
N = 7;

Hd = zeros(1, N);

a = (N - 1)/2;

% Center coefficient
hna = 1 - ((Wc2 - Wc1)/pi);

% Compute impulse response
k = 1:((N - 1)/2);
n = k - 1 - ((N - 1)/2);

hd = (sin(Wc1*n) - sin(Wc2*n)) ./ (pi*n);

hn = hd;

% Complete impulse response
Hn = [hn hna fliplr(hn)];

% Frequency response
w = 0:pi/16:pi;

Hw1 = hna * exp(-1j*w*a);
Hw2 = 0;

for m = 1:a
    Hw3 = hn(m) * ...
        (exp(1j*w*(1-m)) + exp(-1j*w*(1-m+2*a)));

    Hw2 = Hw2 + Hw3;
end

Hw = Hw1 + Hw2;

% Magnitude response
H_mag = abs(Hw);

% Plot
plot(w/pi, H_mag, 'k');
grid on;

title('Magnitude Response', 'fontweight', 'b');
xlabel('Normalized Frequency, \omega/\pi', 'fontweight', 'b');
ylabel('Magnitude', 'fontweight', 'b');
```

## OUTPUT 
<img width="1392" height="559" alt="Screenshot 2026-06-04 085607" src="https://github.com/user-attachments/assets/feb1253f-38a9-4e4d-943f-4a08e5014c27" />


## RESULT
Thus the FIR filter with the given specifications was designed using rectangular windowing technique.
