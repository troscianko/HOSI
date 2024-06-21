# HOSI: Hyperspectral open source imager

_Developed by Jolyon Troscianko_

The hyperspectral open-source imaging system (HOSI) is an innovative and low-cost solution for collecting full-field hyperspectral data. The system uses a Hamamatsu C12880MA micro spectrometer to take single-point measurements, together with a motorised gimbal for spatial control. The hardware uses off-the-shelf components and 3D printed parts, costing around £350 in total. The system can run directly from a computer or smartphone with a graphical user interface, making it highly portable and user-friendly.

The HOSI system can take panoramic hyperspectral images that meet the difficult requirements of ALAN research, sensitive to low light around 0.001 cd.m-2, across 320-880nm range with spectral resolution of ~9nm (FWHM) and spatial resolution of ~0.2 degrees. The independent exposure of each pixel also allows for an extremely wide dynamic range that can encompass typical natural and artificially illuminated scenes, with sample night-time scans achieving peak-to-peak dynamic ranges of >50,000:1.

This system's adaptability, cost-effectiveness, and open-source nature position it as a valuable tool for researchers investigating the complex relationships between light, environment, behaviour, ecology, and biodiversity, with further potential uses in many other fields.

![image](https://github.com/troscianko/HOSI/assets/53558556/4d4276ba-5631-4520-91a5-47eb7aa20279)
_Figure 1. 3D parts and wiring. a) Photograph of a HOSI unit in the field, running from a smartphone. b): 3D assembly; c): parts arranged for 3D printing; d): wiring diagram and required wire lengths. GND (ground) is the shared negative voltage, VIN is the 5v output from the Arduino that is delivered via the USB cable. Note that the spectrometer should be connected to the Arduino’s regulated 5v output (as shown), not VIN that has a slightly lower voltage due to a protective diode in the Arduino._

![image](https://github.com/troscianko/HOSI/assets/53558556/87a651ab-8789-4f20-8afc-353179778cec)
_Figure 2. Graphical user interface (GUI) layout, showing the available functions and a scan of butterflies. The spectrum shows a selection from a patch of wing that appears black to human vision, but has a UV peak visible to many other animals. This scene was illuminated by an Exo-Terra Sunray lamp._

![image](https://github.com/troscianko/HOSI/assets/53558556/f7853201-a29d-4b70-b86d-b44d9c76a2da)
_Figure 3. Example hyperspectral scan of Falmouth (UK) docks at night. a): panoramic photograph of the scene; b): HOSI’s hyperspectral RGB preview image; c): radiance plots created by the HOSI GUI at chosen pixels (x-axis: wavelength [nm]; y-axis: linear radiance Le [W.sr-1.m-2.nm-1]). These spectra illustrate how individual light sources can be identified and compared. The highest spectral peak in the brightest pixel of this hyperspectral image is approximately 50,000 times higher than the peak in the darkest pixel. The full dynamic range (highest peak to lowest trough) is considerably greater, and can be maximised further with longer exposure times to reduce noise._


**Description of HOSI file output format** (each scan generates a .csv file and .png image):
_First line:_
'h' denotes start of raw data from HOSI, unit #, pan left limit, pan right limit, pan resolution steps-per-scan, tilt lower limit, tilt upper limit, tilt resolution (steps-per-scan), maximum integration time (microseconds), boxcar spectral pooling value, delay between dark measurement repeats (milliseconds)

_Second line onwards:_
pan location (steps), tilt location (steps), measurement type (0=dark measurement, 1=light measurement, 2=initialisation exposure), integration time (microseconds), number of wavelength bins reaching saturation point, spectral count data (288 comma-delineated measurements unless a boxcar>1 is used)

'x' denotes end of raw data

Following this, a table of processed, calibrated _Le_ values are shown, together with wavelengths, and pan/tilt locations. Note that this table uses the calibration data present when the raw file was generated.
