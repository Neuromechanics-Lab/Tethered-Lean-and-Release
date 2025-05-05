# Tethered Lean-and-Release System
The MALAB scripts and Apps for testing the LSL and visualizing the force sensor plus accelerometer data and trigger markers of the tethered lean-and-release system.

For more information about the design and testing of this system, please check the OneNote design notes/logs here: https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Design_notes_operating_instructions_version_history.pdf

# MATLAB App
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/MATLAB_App_GUI_2.png)
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
* 0.45:
  1. Added marker stream.
  2. Added save function for marker stream.
  3. Added log messages that display the name of the selected stream.
  4. Fixed the problem that the Raw Readings Plot Y-axis Label not displaying properly after switching raw readings type.
  5. Added auto marker stream detection to retrieve data from the first typed "Markers" stream from the stream search.
  6. Added display options for raw readings.
  7. Changed plotted line colors from black to blue.
  8. Timeseries object causes crashes, consider implementing with the newer time table object instead.
  9. To Do:
	  a. Implement time table:
		b. Object declaration/initialization
		c. Append new data
    d. Test for performance, latency and consistency, etc.

* 0.60:
  1. Checked the voltage to force conversion
	2. Checked the force to angle conversion
	3. Swaped Controls and Infos Panel for more intuitive use of the app.
  4. Added calibration function.

* 0.70:
	1. Added percent weight display
  2. Trouble shoot
    a. Cannot start stream, error message "vertcat(app.TT_all; TT_new);"
    b. Dimensions of arrays being concatenated are not consistent.

* 0.74:
  1. Fixed the ylimits and yticks for % Body Weights display plot.
  2. Fixed the scale and sign of the % Body Weights display plot.
  3. Fixed the sign of the other modes of the Raw Data display plot.
  4. Added the LiveAmp prop type and prop name as the default settings.
  5. Fixed the issue that switching the Raw Data display option dropdown menu will crash the App.

## Operating Instructions

### 1. Preparations

#### a. Setup the Test Subject

1. Place the necessary sensors.
2. Connect LiveAmp to BrainVision Recorder.
3. Put the harness on the subject.
4. Provide experiment instructions.
5. Record subject's height (cm).
6. Record subject's weight (kg).
7. Note subject's sex.

#### b. Setup the Tethered-Release System

1. Adjust the metal plate height to ~3 cm lower than the metal clip height on the harness when standing straight. Record height (cm).
2. Clip the tether to the bow release and harness.
3. Ask subject to walk forward along red tape until tether is taut.
4. Instruct subject to lean back 1–2 steps, per protocol.

#### c. Setup the LiveAmp LSL Connector
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/liveamp.png)
1. Switch off BrainVision Recorder.
2. Launch the LiveAmp LSL Connector on the MoBI Laptop.
3. Click **Scan**. Confirm the LiveAmp device via Device Number.
4. Set **AUX Channels** to 8 (for STE box).
5. Enable ACC sensors.
6. Keep Chunk Size and Sampling Rate as default.
7. Under LSL Trigger Output Style, check **EEG Channel** (for later analysis).
8. Click **Link**. The button changes to **Unlink** upon success.

#### d. Setup the Lab Recorder
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/labrecorder-default.png)
1. Launch the Lab Recorder.
2. Verify all expected streams (LiveAmp, TriggerBox, STE) are listed.
3. Click **Select All**.
4. Click **Update** if stream list has changed.
5. Set save path and filename.
6. **Important**: Delay clicking **Start** until MATLAB App confirms all streams are functional.

---

### 2. MATLAB App Setup (`Tethered_Lean_Release_Feedback`)

#### a. Launch the App
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/matlab_open_app.png)
1. Open MATLAB R2024b on the MoBI Laptop.
2. Navigate to the **APPS** tab.
3. Open **Tethered_Lean_Release_Feedback**.
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/MATLAB_App_GUI_2.png)
#### b. Configure Stream Info

1. Specify **Sensor Stream Info** and **Marker Stream Info**.
2. Use **Prop Type** and **Prop Value** to locate streams by `name`, `type`, or `source_id`.
3. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/sensor_config.png)
4. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/sensor_config_2.png)
5. Check stream names in Lab Recorder for validation.
6. The log will confirm found and connected streams.

#### c. Configure Patient Info

- Enter weight and height of the subject.
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/patient_info.png)

#### d. Configure Auxiliary Info

1. Enter **Tether Height** (from earlier setup).
2. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/aux_info_tether.png)
3. Configure **CoM Type**:
   - Use preset ratio based on sex or input a custom value.
   - ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/aux_info_com.png)
   - ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/aux_info_com_custom.png)

#### e. Configure Stream Controls

1. Switch off Marker if not using a marker stream. If No marker is detected, the marker switch will automatically turn off.
2. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/marker_switch.png)
3. Click **Initiate** to search for streams using specified props.
4. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/initiate.png)
5. View log output to verify stream connection.
6. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/sample_log_audio.png)
7. Click **Start** to begin streaming and plotting.
8. ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/sample_GUI_audio.png)
9. Use **Channel Select** to change plotted channel number.

#### f. Validation Before Data Collection

- **Sensor plots (blue)** and **markers (orange xlines)** must be visible.
- ![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/sample_plot_force_sensor_release_button.png)
- Select proper channel:
  - EEG: 1–32 or 1–64
  - AUX: 33–40 or 65–72
  - ACC: 41–43 or 73–75 (x, y, z)
- Validation:
  - Pull tether → sensor force changes.
  - Move sensor → accelerometer changes.
  - Press trigger button → marker appears.

If any issues arise, check the log and consider restarting the App, Connector, or Recorder.

#### g. Begin Recording

Return to Lab Recorder and click **Start**.

#### h. Indicator Lights
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/code_indicator_light.png)
- **Red**: Lean angle too large.
- **White**: Lean angle too small.
- **Green**: Target angle reached — ready to release.
- Works with **Lean Torque** if selected.

#### i. Calibration (Experimental)
![Alt text](https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/Figures/calibration_code.png)
1. Attach known weight to tether system.
2. Input calibration weight in app.
3. Start stream.
4. Click **Calibrate**.
5. The app computes an offset from known and measured force.

---

## Notes

- The EEG Channel-style trigger is experimental as of 04/22 and may not be fully compatible with the MATLAB App.
- Restart systems if stream or plotting fails.


# MATLAB Scripts
- Analyzing the Sampling\Timestamp Consistency and Delays: https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/sampling_consistency_and_delay_analysis.mlx
- Analyzing More Sampling Consistency: https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/consistency_analysis_cont.mlx
- Analyzing Analog-to-Digital Conversion of LiveAmp/ActiCHamp System: https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/ADC_Conversion_analysis.mlx

# Reports
- Sampling\Timestamp Consistency and Delays: https://github.com/Neuromechanics-Lab/Tethered-Lean-and-Release/blob/main/sampling_consistency_and_delay_analysis.pdf
