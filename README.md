NIR (SWIR) pixel
======

NIR (SWIR) pixel is designed to be a low-cost detection tool for detection and power measurement of free-space optical beam of 1100nm-1650nm wavelengths (adjustable by using different detectors). Using an array of pixels a similar functionality to phosphorous IR indicator cards is implemented, but operational also in bright environments. As every pixel also provides a measurement output, optical power per pixel can be observed and used to deduct the beam shape.

### Design overview
NIR pixel uses PIN-TIA integrated photo-detectors in TO46 enclosure generally used in SFP fibre optical modules, currently using low-cost YPC3418-X-44 (155M InGaAs PIN-TIA) detectors with better then -38dBm sensitivity. The signal from the TIA is amplified by [ONET4201PA](http://www.ti.com/lit/ds/symlink/onet4201pa.pdf) optical amplifier with separate LOS and RSSI outputs. With a resistor one can determine when the LOS signal is asserted, showing the detection level with a simple on-board LED diode. The RSSI output can be measured and the optical power per pixel measured.

### Optics

Aperture of the PIN-TIA detector is a 1mm ball-lens and can be used without additional optics used with stable mounting for high resolution measurements, however only with sufficient optical amplitude. As this is generally not useful, version 1 is a 3x3 pixel array of detectors. Since the pixel density is limited by TO46 package size, the design can be extended with a 3D printed mount and 7mm(6mm lens area) plastic convex lenses (PMMA,f=6.47mm). Over the 1100nm-1650nm spectrum we can assume about 70%-80% transmissivity.

Detector without the lens has area 0.79mm^2 and -38dBm=0.16uW sensitivity, corresponding to 0.2uW/mm^2 sensitivity.
Detector with the lens of 6mm diameter lens area, 80% transmissivity has then 28.3mm^2 area, corresponding to 0.0045uW/mm^2 sensitivity.

An IR indicator card in the given wavelength range may have sensitivity in the range of 3uW/cm^2=0.03uW/mm^2. The sensitivity of the NIR pixel is thus an order of magnitude better and observable in daylight, assuming optical noise floor being sufficiently low. Alternatively an IR filter must be used.

### Version 1 setup
First version of the NIR pixel is a barebone module with only the PIN-TIA and amplifier per pixel on a 3x3 board. Every pixel has GND, RSSI and VCC pins, GND being common for all the pixels. Using jumper wires pixels are connected to TI Tiva C Launchpad running Energia written code for measuring the power per pixel and either sending it via USB serial to computer or with HC-05 bluetooth-serial module. A simple Processing script color-codes the power and displays it on the screen. This rough prototype confirms the system is useful and now needs to be integrated/optimized.

OpenSCAD designed 3D printable mounting block for lenses and detectors is built to join both. Simply push-in the lens in from one side and the detector form the other, when printed accurately enough, they will remain in place.

## Known problems and drawbacks
 * Soldering TO46 on surface mount pads is too difficult, they must be mounted through hole
 * Power consumption per pixel is 65mA, with 9 pixels quite a large regulator is required. 18mA is used by the PIN-TIA and the rest by amplifier, that could be replaced by a simpler one.

![NIR pixel](https://raw.github.com/IRNAS/NIRpixel/master/ver1/NIRpixelV1-1.jpg)
![NIR pixel](https://raw.github.com/IRNAS/NIRpixel/master/ver1/NIRpixelV1-2.jpg)

### Firmware/software
The Energia based firmware for use with TI Launchpads and compatible with Arduino is used to read analog outputs from NIRpixel and send measurements via serial to computer. Processing GUI is used to display color-coded values with numerical value overlayed. This is all very basic and just proof-of-concept.



See the Wiki for comparison with other similar systems.

### Source description
The designs are currently prepared in Alitum Designer due to the ease of workflow. Schematic and gerber files are available, the design will be ported to KiCad as soon as possible.

---

#### License

All our projects are as usefully open-source as possible.

Hardware including documentation is licensed under [CERN OHL v.1.2. license](http://www.ohwr.org/licenses/cern-ohl/v1.2)

Firmware and software originating from the project is licensed under [GNU GENERAL PUBLIC LICENSE v3](http://www.gnu.org/licenses/gpl-3.0.en.html).

Open data generated by our projects is licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/legalcode).

All our websites and additional documentation are licensed under [Creative Commons Attribution-ShareAlike 4 .0 Unported License] (https://creativecommons.org/licenses/by-sa/4.0/legalcode).

What this means is that you can use hardware, firmware, software and documentation without paying a royalty and knowing that you'll be able to use your version forever. You are also free to make changes but if you share these changes then you have to do so on the same conditions that you enjoy.

Koruza, GoodEnoughCNC and IRNAS are all names and marks of Institut IRNAS Rače. 
You may use these names and terms only to attribute the appropriate entity as required by the Open Licences referred to above. You may not use them in any other way and in particular you may not use them to imply endorsement or authorization of any hardware that you design, make or sell.
