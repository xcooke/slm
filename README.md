# slm

This code is a mess! This is left as I was using it.

This code was for my summer research project at Imperial. I worked in the Imperial Strontium Lab, (https://www.stronlab.net/) and (https://www.hep.ph.ic.ac.uk/AION-Project/).

More details about the project are in the Imperial Strontium Lab labbook (https://labbook.stronlab.net/2026/2026-09-11-Xander-UROP-Write-Up).

In this repo I learnt about how the SLM works, I wrote code to calibrate the Voltage->Phase, and I wrote some functions for my `tweezer-array` repo.

# slmsuite

I am using slmsuite to talk to Meadowlark SLM and to the Thorlabs camera.

Read about "ij", "kxy", "knm" space in slmsuite documentation https://slmsuite.readthedocs.io/en/latest/api.html

Read about Fourier calibration in slmsuite docs https://slmsuite.readthedocs.io/en/latest/_examples/experimental_holography.html#Fourier-Calibration

# Installation

Using UV as package manager.

Also need to install Meadowlark drivers as well. Use lab book entry for how I did it https://labbook.stronlab.net/2026/2026-07-29-SLM-investigation. Tom provided me with Meadowlark software, I don't think you can find on web.

Thorlabs camera drivers are installed automatically with ThorCam or ThorImageCam (ThorImageCam is newer, I mainly used this). Camera specific details in labbook entry (https://labbook.stronlab.net/2026/2026-07-24-2D-AOD-setup-continued.)

There is a bug in the source code of slmsuite for interaction with the Thorlabs camera. The fix is in labbook entry (https://labbook.stronlab.net/2026/2026-08-03-SLM-calibration-continued). The correct `thorlabs.py` file is in the repo (can also be found well as in the git bug report).

# Beware

Camera should be initiated with `cam = ThorCam(rot = "270")` given the current physical camera setup, but not all code files have this. This should be set given the physical orientation of the camera.

See above re slmsuite ThorCam bug.

I think the bug also effects slmsuite's HDR and frame averaging features, but I haven't tested this, and I never got them working.

# Voltage->Phase calibration of SLM

I followed a ThorLabs guide to calibrating the Voltage->Phase of SLM (https://www.youtube.com/watch?v=3GGVmw1_8W8)

I used this once, and changed the physical setup since then. It wasn't perfect in the initial configuration and it is probably worse now.

Instead of doing this I think you can use the Meadowlark software. Spoke to Daniel and he said he used it and it works well.

# Files

## Used parallel to tweezer-array

`fourier_calibrate.ipynb` does Fourier calibration in desired location, specified in kxy space. This is used in tweezer-array repo

`write_phase.ipynb` writes phase to SLM from a pickle file. Useful to check if SLM is working

## Spot array generators

`blaze_generator.ipynb` makes array of spots, determined by position in kxy space. Uses none of slmsuite helper functions to generate a very rough phase pattern (not optimised!)

`spot_array_generator.ipynb` makes array of spots, determined by position in kxy space. Uses slmsuite computational optimise functions to improve phase pattern

## Calibration

`calibrate.ipynb` file I ran to do voltage->phase calibration. I haven't looked at this in a long time

`interpolated_voltage.lut` is the useful output from `calibrate.ipynb` that contains colour bit->voltage (->phase)

`19x12_8bit_linearVoltage.lut` is the default linear colour bit->voltage map that uses the whole voltage range

`check_calibration.ipynb` file to test voltage->phase calibration

## Other

`fit_gaussian.ipynb` fits slice from ThorImageCam software to gaussian curve and outputs image with 1/e^2 radius

`simulating_zernike_correction.ipynb` was an incomplete attempt to understand aberrations. Note if turn up Z amplitude too high get aberration due to finite (8um) pixel spacing of SLM

