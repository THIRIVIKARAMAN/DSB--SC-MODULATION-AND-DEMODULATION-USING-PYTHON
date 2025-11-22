# DSB--SC-MODULATION-AND-DEMODULATION-USING-PYTHON

__AIM__:

To generate a Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab), transmit it (optionally add noise), and recover the message using coherent (synchronous) demodulation with a low-pass filter. Observe time and frequency domain waveforms and measure demodulation performance

__APPARATUS REQUIRED__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

__Theory__:

DSB-SC signal: s(t) = m(t) · cos(2πf_c t)
Coherent demodulation: multiply received s(t) by a synchronized carrier cos(2πf_c t) then low-pass filter (LPF) to remove double-frequency components:

r(t) = s(t)·cos(2πf_c t) = m(t)·cos²(2πf_c t) = 0.5 m(t) + 0.5 m(t)·cos(4πf_c t)
LPF extracts 0.5·m(t) → scale by 2 to recover m(t).

__Procedure__:

1) Import libraries and set parameters
2) Define message and carrier signals
3) Generate DSB-SC signal (modulation)
4) View spectra (FFT) of message and DSB-SC
5) (Optional) Add noise
6) Coherent demodulation (multiply by synchronized carrier)
7) Low-pass filter to recover message
__Program__:
~~~
import numpy as np
import matplotlib.pyplot as plt

Ac = 37.2
fc = 8000

Am = 18.6
fm = 800

fs = 80000

# Time vector
t = np.arange(0, 2/fm, 1/fs)

# Angular frequencies
Wm = 2 * np.pi * fm
Wc = 2 * np.pi * fc

# Message signal (sine)
Em = Am * np.sin(Wm * t)

# Carrier signal (sine)
Ec = Ac * np.sin(Wc * t)

# DSB-SC using trigonometric identity
Edsbsc = ((Am / 2) * np.cos((Wc - Wm) * t)) - ((Am / 2) * np.cos((Wc + Wm) * t))

# Plotting
plt.figure(figsize=(10, 6))

plt.subplot(3, 1, 1)
plt.plot(t, Em)
plt.title("Message Signal (Em)")
plt.grid()

plt.subplot(3, 1, 2)
plt.plot(t, Ec)
plt.title("Carrier Signal (Ec)")
plt.grid()

plt.subplot(3, 1, 3)
plt.plot(t, Edsbsc)
plt.title("DSB-SC Signal (Edsbsc)")
plt.grid()

plt.tight_layout()
plt.show()
~~~
 __Tabulation__:
![WhatsApp Image 2025-11-22 at 08 35 46_220cf006](https://github.com/user-attachments/assets/f110fa8d-00da-4f7b-898b-b31975413d0f)

 __Calculation__:
![WhatsApp Image 2025-11-22 at 08 35 46_d58c0785](https://github.com/user-attachments/assets/f7866ff5-a6fe-4119-9101-1f9acb20b60a)

__Output__:
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/6b5dd575-eeba-4601-8998-ab830f40325f" />


__Result__:
