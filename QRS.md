## EXP NO 06:	QRS COMPLEX DETECTION FROM ECG SIGNAL
## DATE :

## AIM
To analyze the ECG signal using MATLAB and extract important features such as heart rate, QRS complex, and waveform visualization.

## APPARATUS / SOFTWARE REQUIRED
Computer with MATLAB installed
Sample ECG signal file (.mat or .csv)
Biomedical Signal Processing Toolbox (if available)

## THEORY
The Electrocardiogram (ECG) is a bioelectrical signal that represents the electrical activity of the heart over time.
A typical ECG waveform consists of P-wave, QRS complex, and T-wave.
Analysis of ECG helps in detecting cardiac abnormalities such as arrhythmia and myocardial infarction.
Key parameters in ECG analysis include:
•	Heart rate (beats per minute)
•	R-R interval (time between successive R-peaks)
•	Amplitude of QRS complex
•	Signal filtering to remove baseline wander and noise

## ALGORITHM 
1.	Load the ECG signal into MATLAB.
2.	Plot the raw ECG signal to visualize waveform characteristics.
3.	Apply preprocessing filters:
o	Remove 50 Hz power-line noise using a notch filter.
o	Remove baseline drift using a high-pass filter (cutoff ≈ 0.5 Hz).
4.	Detect R-peaks using the Pan–Tompkins algorithm or MATLAB’s findpeaks() function.
5.	Compute heart rate from R-R intervals.
6.	Plot the filtered ECG with detected R-peaks.
7.	Display extracted parameters such as heart rate and number of beats.




## MATLAB Code:
% ECG Signal Analysis in MATLAB

% Step 1: Load the ECG signal
load('ecg.mat'); % or use your own ECG data
fs = 360; % Sampling frequency in Hz
t = (0:length(ecg)-1)/fs;

% Step 2: Plot the raw ECG signal
figure;
plot(t, ecg);
title('Raw ECG Signal');
xlabel('Time (s)');
ylabel('Amplitude (mV)');

% Step 3: Filter the signal (remove noise & baseline)
ecg_filt = bandpass(ecg, [0.5 40], fs);

% Step 4: Detect R-peaks
[~, locs_R] = findpeaks(ecg_filt, 'MinPeakHeight', 0.5, 'MinPeakDistance', 0.25*fs);

% Step 5: Calculate Heart Rate
RR_intervals = diff(locs_R)/fs; % in seconds
HR = 60 ./ RR_intervals; % in bpm
Avg_HR = mean(HR);

% Step 6: Plot filtered ECG with R-peaks
figure;
plot(t, ecg_filt); hold on;
plot(locs_R/fs, ecg_filt(locs_R), 'ro');
title(['Filtered ECG Signal with R-peaks | Avg HR = ', num2str(Avg_HR, '%.2f'), ' bpm']);
xlabel('Time (s)');
ylabel('Amplitude (mV)');
legend('Filtered ECG','R-peaks');

% Step 7: Display Results
disp(['Average Heart Rate = ', num2str(Avg_HR, '%.2f'), ' bpm']);

Sample Output:
•	ECG waveform plotted with identified R-peaks.
•	Display of average heart rate (e.g., Average Heart Rate = 76.45 bpm).
•	Clean, denoised ECG signal after filtering.

## OUTPUT
 


## RESULT:

The ECG signal was successfully analyzed using MATLAB.
The QRS complex was detected, and the average heart rate was computed accurately

