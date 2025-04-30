# Tethered Lean-and-Release System
The MALAB scripts and Apps for testing the LSL and visualizing the force sensor plus accelerometer data and trigger markers of the tethered lean-and-release system.

# MATLAB App
## Purpose

This tool is designed to:
- Display and plot tether tension, estimated lean torque, and estimated lean angle in real-time.
- Provide researchers with a clear indication of whether a test subject has leaned sufficiently and is ready to be released.

## Functionalities

- Calculate lean angle and lean torque using force sensor readings and user-defined input parameters.
- Plot the calculated values in real-time.

## Stream Controls

- **Initiate**:  Initialize the library and retrieve available channels based on their properties.
  
- **Start**:  Connect to a channel inlet and begin receiving data and timestamps.
  
- **Stop**:  Stop the data stream and terminate the initialization.

## Info Panels

### Stream Info

- **Prop Type**:  Type of stream property (e.g., `"name"`, `"type"`, `"source_id"`).
  
- **Prop Name**:  The specific name of the stream property (e.g., `"Name"` → `"My Keyboard"`).
  
- **Pull Type**:  Data pulling method – either `sample` or `chunk`.
  
- **Estimation Type**:  Choose between `lean angle` or `lean torque`.
  
- **Target Value**:  Toggle between target lean angle and torque based on the selected estimation type.

### Patient Info

- **Weight**: Patient's weight in kilograms. 
- **Height**: Patient's height in centimeters.

### Auxiliary Info

- **Height-CoM Coefficient**:  Ratio of the patient's center of mass (CoM) height to total body height. Can be set to an established average or a user-defined value.
  
- **Tether Height**: The height of the mechanical clip (bow release) above the ground.

### Calibrate

- Calibrate the force sensor using known weights.
  - **Calib Weight**: Input the known calibration weight.

### Log

- Displays detailed system information and error messages.

## Display Panel

- **Indicators**
  - Release-Ready Indicator

- **Estimates**
  - Sensor force threshold
  - Lean Angle
  - Pivot-point Torque

- **Sensor Info**
  - Tether tension
  - Sensor force threshold
  - Inclinometer angle readout

- **Channel Number**
  - Displays the selected channel number


## Version History
* 0.45
* 0.60
* 0.70
* 0.74

## Operating Instructions

# MATLAB Scripts

