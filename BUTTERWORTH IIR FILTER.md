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
clear all
clc

AP=0.707;					% Gain at passband edge frequency
AS=0.08;					% Gain at stop band edge frequency
PEF_D=0.2*pi;					% Passband edge digital frequency
SEF_D=0.4*pi;					% Stop band edge digital frequency
T=1;						% Sampling time
alpha_P=-20*log10(AP)				% Passband attenuation in dB
alpha_S=-20*log10(AS)				% Stop band attenuation in dB

PEF_A=(2/T)*tan((PEF_D/2)
SEF_A=(2/T)*tan((SEF_D/2)

[N,CF]=buttord(PEF_A,SEF_A,alpha_P,alpha_S,'s')        % Order and cutoff frequency

[Bn,An]=butter(N,,1,'s');				% Normalized Transfer Function
display('Normalized Transfer Function is,')
Hsn=tf(Bn,An)

[B,A]=butter(N,CF,'s');				% Unnormalized Transfer Function
display('Unnormalised Transfer Function is,')
Hs=tf(B,A)

[num,den]=bilinear(B,A,1/T);			
% Digital Transfer Function
display('Digital Transfer Function is,')
Hz=tf(num,den,T)

w=0:pi/16:pi;
display('Frequency Response is,')
Hw=freqz(num,den,w)				
% Frequency response
display('Magnitude Response is,')
Hw_mag=abs(Hw)				
% Magnitude response
plot(w/pi,Hw_mag,'k');grid;

title('Magnitude Response of Butterworth 3rd order Lowpass Filter','fontweight','b');
xlabel('Normalised frequency, \omega/\pi','fontweight','b');
ylabel('Magnitude','fontweight','b');
```

## OUTPUT
<img width="1388" height="590" alt="Screenshot 2026-06-04 082304" src="https://github.com/user-attachments/assets/53906b40-6e2a-4f84-889a-cc9047231043" />



 






## RESULT:

Thus, digital Butterworth IIR filter with the given specifications was designed using MatLab.
 
