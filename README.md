# Wavelength Division Multiplexing (WDM) Simulation

## Aim 
To simulate a WDM system using Python and analyze channel separation and insertion loss.

## Apparatus/Software Required
	Python (NumPy)
	Google Colab or Jupyter Notebook

## Theory
	WDM allows multiple optical signals at different wavelengths to be transmitted simultaneously over a single fiber.
	Channel spacing determines spectral efficiency and crosstalk.
	Insertion loss is the reduction in signal power due to multiplexing/demultiplexing.

## Formula:
"Insertion Loss (dB)"=P_in-P_out
"Channel Spacing"=Δλ

## 1
## Setup Environment
Info
Prepare Python environment for simulation.
	Import NumPy and Matplotlib
	Define channel wavelengths and powers

## 2
## Define WDM Parameters
Specify input wavelengths and powers.
Example: λ = [1550, 1552, 1554] nm, Pin = -2 dBm
	Choose 3 channels
	Assign equal input power

## 3
## Calculate Output Power
Simulate insertion loss for each channel.
Insertion Loss = Pin - Pout
	Assume ~1 dB loss per channel
	Compute Pout

## 4
## Plot WDM Spectrum
Visualize channel separation.
	Use Matplotlib to plot wavelength vs power
	Label each channel peak

## 5
## Analyze Results
Success
Interpret the simulation output.
	Channels separated with ~1–2 dB insertion loss
	Verify spacing Δλ = 2 nm

## Sample Output
 <img width="623" height="478" alt="image" src="https://github.com/user-attachments/assets/7569e8ec-3417-4669-b37b-06029f87655a" />

 <img width="677" height="466" alt="image" src="https://github.com/user-attachments/assets/e937804f-b55d-4de9-ab1e-155e6bd01d8e" />

 <img width="652" height="456" alt="image" src="https://github.com/user-attachments/assets/d22a7a99-0cd4-439e-b49b-b9dde93ab78b" />

## Python Code 
```
import numpy as np
import matplotlib.pyplot as plt

# WDM settings
channels = 5
center_wavelength = 1550
width = 0.2
x = np.linspace(1545, 1555, 2000)

# Function to generate WDM signal
def generate_signal(spacing):
    signal = []
    wavelengths = []

    for i in range(channels):
        wl = center_wavelength + (i - 2) * spacing
        wavelengths.append(wl)

        power = np.exp(-0.5 * ((x - wl) / width) ** 2)
        signal.append(power)

    return wavelengths, signal

# Graph 1: Individual channels
wl, signals = generate_signal(0.8)

plt.figure(figsize=(8, 4))
for i, power in enumerate(signals):
    plt.plot(x, power, '--', label=f'Channel {i+1}')

plt.xlabel('Wavelength (nm)')
plt.ylabel('Power')
plt.title('Individual WDM Channels')
plt.legend()
plt.grid()
plt.show()

# Graph 2: Combined WDM signal
combined = np.sum(signals, axis=0)

plt.figure(figsize=(8, 4))
plt.plot(x, combined)
plt.xlabel('Wavelength (nm)')
plt.ylabel('Power')
plt.title('Multiplexed WDM Signal')
plt.grid()
plt.show()

# Graph 3: Compare channel spacing
plt.figure(figsize=(8, 4))

for spacing in [0.2, 0.8, 1.6]:
    wl, signals = generate_signal(spacing)
    combined = np.sum(signals, axis=0)

    plt.plot(x, combined, label=f'Spacing = {spacing} nm')

plt.xlabel('Wavelength (nm)')
plt.ylabel('Power')
plt.title('Effect of Channel Spacing in WDM')
plt.legend()
plt.grid()
plt.show()

# Insertion loss calculation
input_power = -2
loss = 1
output_power = input_power - loss

print("WDM Simulation Results")
print("----------------------")
print("Number of channels:", channels)
print("Center wavelength:", center_wavelength, "nm")
print("Input power:", input_power, "dBm")
print("Insertion loss:", loss, "dB")
print("Output power:", output_power, "dBm")
print("Channel spacings: 0.2, 0.8, 1.6 nm")
```

## Output
<img width="691" height="393" alt="image" src="https://github.com/user-attachments/assets/5a80a233-e060-48c4-add7-a89b279e41ef" />
<img width="691" height="393" alt="image" src="https://github.com/user-attachments/assets/58a640e9-6ea5-4309-b94c-2eec55e3e423" />
<img width="691" height="393" alt="image" src="https://github.com/user-attachments/assets/4d8483ae-1b90-4d4c-bdc1-9d446f7ffcdf" />




## Result 
The WDM system was successfully simulated using Python. Multiple optical signals with different wavelengths were multiplexed into a single optical channel and separated at the receiver.
