## EXP NO: 02	RADIX-2 DECIMATION IN TIME FFT  
## DATE :2.05.26
## Aim:
To implement the Radix-2 Decimation-in-Time (DIT) Fast Fourier Transform (FFT) algorithm in MATLAB and analyze the frequency-domain representation of a given discrete-time sequence..
## Requirements:
MATLAB software
Understanding of DFT, FFT, and Radix-2 algorithms
# Theory
The Fast Fourier Transform (FFT) is an efficient algorithm for computing the Discrete Fourier Transform (DFT) and its inverse.
The Radix-2 DIT FFT is applicable when the number of input samples N is a power of two. It works by:
Splitting the input sequence into even and odd-indexed samples.
Computing smaller DFTs recursively.
Combining the results using butterfly computations.
## ALGORITHM
•  Start the program.
•  Define the input sequence x(n) and length N (must be a power of 2).
•  Perform bit reversal of the input sequence indices.
•  Implement the Radix-2 DIT FFT butterfly computation:•  
Break the sequence into smaller parts (divide).
Combine results stage by stage (conquer).
•  Compute the magnitude and phase from the FFT output.
•  Plot:  
Input sequence (time domain)
Magnitude spectrum
Phase spectrum
•  Stop the program.
## MATLAB CODE
```
clc;
clear;
close all;

% Input sequence
x = [1 2 3 4 5 6 7 8];
x_original = x;   % Store original sequence

N = length(x);

% Check if N is power of 2
if mod(log2(N),1) ~= 0
    error('Length of input must be a power of 2');
end

% Bit reversal ordering
n = 0:N-1;
bitrev_index = bitrevorder(n+1);
x = x(bitrev_index);

% FFT Computation (Radix-2 DIT)
stages = log2(N);
X = x;

for stage = 1:stages
    
    m = 2^stage;
    half_m = m/2;
    Wm = exp(-1j*2*pi/m);

    for k = 0:(N/m - 1)
        
        for j = 0:half_m-1
            
            t = (Wm^j) * X(k*m + j + half_m + 1);
            u = X(k*m + j + 1);

            X(k*m + j + 1) = u + t;
            X(k*m + j + half_m + 1) = u - t;
        end
    end
end

% Display FFT output
disp('Frequency Domain Output X(k):');
disp(X);

% Magnitude and phase
magX = abs(X);
phaseX = angle(X);

% Plotting
figure;

subplot(3,1,1);
stem(0:N-1, x_original, 'filled');
xlabel('n');
ylabel('Amplitude');
title('Input Sequence (Time Domain)');
grid on;

subplot(3,1,2);
stem(0:N-1, magX, 'filled');
xlabel('k');
ylabel('|X(k)|');
title('Magnitude Spectrum');
grid on;

subplot(3,1,3);
stem(0:N-1, phaseX, 'filled');
xlabel('k');
ylabel('Phase (radians)');
title('Phase Spectrum');
grid on;
```

## OUTPUT
 <img width="1387" height="568" alt="Screenshot 2026-06-04 090837" src="https://github.com/user-attachments/assets/237b0c7e-75be-41a0-ac24-791135689e68" />



## RESULT:
Thus,  Radix-2 Decimation-in-Time  (DIT) FFT algorithm was implemented using MATLAB
