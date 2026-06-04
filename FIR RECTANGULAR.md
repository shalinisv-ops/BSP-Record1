## EXP NO 05: 	DESIGN OF FIR FILTER USING RECTANGULAR WINDOWS 
## DATE :

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

Clear all
Clc
Wc1 = .4*pi;
Wc2 = .65*pi;

N=7

Hd = zeros(1,N);
a = (N-1)/2;
Hna = 1-((wc2-wc1)/pi;

K=1:1:((N-1)/2);
n = k-1-((N-1)/2);
hd(k) = (sin(wc1*n) - sin (wc2*n))./(pi*n);
hn(k) = hd(k);
Hn = [hn hna]

a = (N-1)/2;
w = 0:pi/16:pi;

Hw1=hna*exp(-j*w*a);
Hw2=0;
For m=1:1:a
Hw3=hn(m)*((exp(j*w*(1-m))) + (exp(-j*w*(1-m+2*a))));
Hw2= Hw2+Hw3;

End
Hw=Hw2+Hw3

H_mag=abs(Hw)
Plot(w/pi,H_mag, ‘k’); grid;
Title(‘Magnitude response’, ‘font weight’ , ‘b’);
xlabel(‘Normalised frequency,\omega/\pi’, ‘font weight’, ‘b’);
ylabel (‘Magnitude’, ‘font weight’, ‘b’);

## OUTPUT 

## RESULT
Thus the FIR filter with the given specifications was designed using rectangular windowing technique.
