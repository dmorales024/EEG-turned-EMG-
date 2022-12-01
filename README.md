# BME 354 Final Project Description
In our efforts for this final project, we attempted to create a device that would be able to determine your brain's state (either concentrating or relaxed). We drew inspiration from Michael Reeves' [Using Mind Control to Drive a Car](https://www.youtube.com/watch?v=mPbtR4vorgY). An EEG, electroencephelogram, is a test monitoring the user's brain activity. We used electrodes placed in specific locations along the user's scalp to attain an accurate enough reading of the alpha brain waves. Alpha brain waves can vary in frequency from 8-12 Hz, but if the user blinks, an increase in frequency of the alpha brain wave is recored. It reflects activities of the visual cortex: their magnitude is increased with closed eyes and relaxation, and decreased with open eyes and concentration. 


Given the lack of access to partiular components and an accurate placement of electrodes on the user's scalp, we had to transition from an EEG to an EMG. In the EMG, we are able to detect movements of the muscle, particularly when the user blinks. Though with both an EEG and an EMG we are able to detect a shift of some sort in the recorded signal, our final project ended up ultmimately being an EMG. Dependent on these electrode placements, with either device you can determine when the user blinks due to the sharp increase in magnitude of the voltage signal recorded. Our final placement of the eelectrodes ended up right above the eyebrow, on the cheekbone, and behind the left ear (as a virtual ground). 

To accomplish this, we set out to create a bandpass filter for the appropriate frequency we attempted to record (the 8-12 Hz range), and included a series of notch filters to remove as much noise as possible. We used a Raspberry Pi Pico to retrieve the signal and process the signal to turn on an LED in the instant that the user blinked. 

 - Video of our subject turning on the LED by blinking: *INSERT HERE*

We based our project on the guidance of instructables.com/DIY-EEG-and-ECG-Circuit/. However, we created our own circuit design, and wrote our own code for data-taking and analysis.


# Methods
## Components needed for project
 - Resistors
 - Raspberry Pi Pico
 - Electrode Stickers
 - Electrode wiring
 - Potentiometer CT6EW102-ND, 1kOhm
 - Two 9V batteries and battery cases (we used a voltage supply, but it should work with 9V batteries)
 - Bread board and wires
 - Oscilloscope and Function Generator
 - Two Instrumental Amplifiers (INA126)
 - Three Operational Amplifiers (LF353): these opamps have two opamps inside 


## Wiring
Insert image HEREERERERERE


The above diagram details the EMG setup. The user places 3 electrodes on their head, one behind the ear, one on the cheekbone, and one right above the eyebrow. These measure the signals from the body that we can input into our circuit to then process the signal and retrieve the final product. The voltage output is put into a specific Pi Pico pin that can convert an analog signal to digital. Due to the Pi Pico's voltage input limitations, we had to use a shifting amplifier to move our centered signal from 0V to 1.6V. The output from this amplifier was put into the Pi Pico, and using a peak detection program such that we can identify the increase in amplitude upon the user blinking. Below is a picture of the physical setup. Note: we could have used 9V batteries in our setup, but because the voltage supply was readily available to us, we decided to use this instead to ensure a constant output of 9V and -9V to our circuit. For the shifting amplifier, we used a voltage of 0.8V as an input into one end of the op-amp which will be explained in detail later. 

![Screen Shot 2022-12-01 at 10 56 56](https://user-images.githubusercontent.com/114500682/205099648-694d08eb-53d7-4571-be5b-1e4fb73240a7.png)


## Electrode Placement for Alpha Wave Measurements
To accurately measure alpha waves, electrodes must be placed at the left mastoid, mostly to reduce noise (A1); another should be placed approximately one inch up and to the right of the nasion (Fp2) (the midline bony depression between the eyes where the frontal and two nasal bones meet); and the last electrode should be placed one inch above the inion (O2) (the projecting part of the occipital bone at the base of the skull). We attempted this setup; however, we found that to achieve the most precise measurements, we would need to either invest in a full EEG cap (kind of like a swim cap with sensors placed all throughout the different locations to acquire signals of the brain, and only connect the two required for alpha wave measurements) or alter the placement of the elctrodes. We chose to alter the placement of the electrodes, and found that the second and third electrodes should be placed on the tip of your right cheekbone and the bone right above your temple (depicted below). As we wanted to determine when the user blinked, these electrodes placement were sufficient enough to still acquire a strong signal. 


<img src="https://user-images.githubusercontent.com/114500682/205096336-ca60931f-c022-493d-a5ea-139c805f64a4.png" width="300">
<img src="https://user-images.githubusercontent.com/114500682/205096622-996a251c-ca9e-4397-87af-59e2fc773c9c.jpg" width="500">

The voltage difference between the second and third electrode placement is used to target the amplitude difference in the alpha waves when the user blinks. See below for proposed and actual placement of EEG electrodes. 

## Circuit Schematic
![Screen Shot 2022-12-01 at 10 54 56](https://user-images.githubusercontent.com/114500682/205099170-2a750ff3-749b-48f6-9b18-ec752202f9c2.png)

Our circuit has the following stages of amplification and filtering:
 - Instrumental Amplifier (gain=8005)
 - Notch Filter (60 Hz, gain = 156.6)
 - High Pass Filter (7 Hz)
 - 



