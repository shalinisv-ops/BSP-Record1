## EXP NO:01	RADIX-2 DECIMATION-IN-FREQUENCY (DIF) FFT
## DATE :24.04.26
## AIM:
To implement the Radix-2 DIF FFT algorithm in MATLAB and analyze the frequency-domain representation of a given discrete-time sequence.
## Apparatus / Software Required:
MATLAB (any version supporting basic matrix operations)
Computer system
## Theory:
The Fast Fourier Transform (FFT) is an efficient algorithm to compute the Discrete Fourier Transform (DFT) of a sequence.
The Radix-2 Decimation-in-Frequency (DIF) algorithm works by successively breaking down the computation of the DFT into smaller DFTs using a divide-and-conquer approach.
DIF splits the input sequence in the frequency domain.
The butterfly structure is used to combine the results efficiently.
Twiddle factors WNk=e−j(2πk/N)W_N^k = e^{-j(2\pi k / N)}WNk=e−j(2πk/N) are used for complex multiplications.
## Algorithm:
Input: Sequence x(n) of length N (where N is a power of 2).
Check: If N is not a power of 2, zero-pad the sequence to the next power of 2.
Step 1: Apply the DIF decomposition — divide the sequence into even and odd index parts in-place.
Step 2: Multiply the odd terms with corresponding twiddle factors.
Step 3: Perform butterfly computation.
Step 4: Repeat recursively for smaller subsequences until size N=2N
Step 5: Apply bit-reversal reordering to get the final FFT output.
Output: Frequency-domain sequence X(k

## MATLAB CODE
```
clc;
clear;
close all;

% Input sequence
x = [1 2 3 4 5 6 7 8];
N = length(x);

% Number of stages
stages = log2(N);

% Initialize input
X = x;

% DIF FFT Computation
for stage = 1:stages
    
    step = 2^(stages-stage+1);
    half = step/2;
    
    for k = 0:half-1
        
        twiddle = exp(-1j*2*pi*k/step);
        
        for m = k+1:step:N
            
            temp = X(m) + X(m+half);
            diff = (X(m) - X(m+half)) * twiddle;
            
            X(m) = temp;
            X(m+half) = diff;
        end
    end
end

% Bit-reversal ordering at output
bitrev = bitrevorder(0:N-1) + 1;
X = X(bitrev);

% Display FFT output
disp('Frequency Domain Output X(k):');
disp(X);

% Magnitude and Phase
magX = abs(X);
phaseX = angle(X);

% Plotting
k = 0:N-1;

figure;

subplot(2,1,1);
stem(k, magX);
title('Magnitude Spectrum');
xlabel('Frequency Index k');
ylabel('|X(k)|');
grid on;

subplot(2,1,2);
stem(k, phaseX);
title('Phase Spectrum');
xlabel('Frequency Index k');
ylabel('Phase of X(k)');
grid on;
```


## OUTPUT

<img width="1390" height="562" alt="Screenshot 2026-06-04 090217" src="https://github.com/user-attachments/assets/926118e0-8b64-4266-8d8e-7d082acf1a70" />


## RESULT:
Thus,  Radix-2 Decimation-in-Frequency  (DIF) FFT algorithm was implemented using MATLAB.
.
 
