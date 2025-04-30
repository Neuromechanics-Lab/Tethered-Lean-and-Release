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

1. Switch off BrainVision Recorder.
2. Launch the LiveAmp LSL Connector on the MoBI Laptop.
3. Click **Scan**. Confirm the LiveAmp device via Device Number.
4. Set **AUX Channels** to 8 (for STE box).
5. Enable ACC sensors.
6. Keep Chunk Size and Sampling Rate as default.
7. Under LSL Trigger Output Style, check **EEG Channel** (for later analysis).
8. Click **Link**. The button changes to **Unlink** upon success.

#### d. Setup the Lab Recorder

1. Launch the Lab Recorder.
2. Verify all expected streams (LiveAmp, TriggerBox, STE) are listed.
3. Click **Select All**.
4. Click **Update** if stream list has changed.
5. Set save path and filename.
6. **Important**: Delay clicking **Start** until MATLAB App confirms all streams are functional.

---

### 2. MATLAB App Setup (`Tethered_Lean_Release_Feedback`)

#### a. Launch the App

1. Open MATLAB R2024b on the MoBI Laptop.
2. Navigate to the **APPS** tab.
3. Open **Tethered_Lean_Release_Feedback**.

#### b. Configure Stream Info

1. Specify **Sensor Stream Info** and **Marker Stream Info**.
2. Use **Prop Type** and **Prop Value** to locate streams by `name`, `type`, or `source_id`.
3. Check stream names in Lab Recorder for validation.
4. The log will confirm found and connected streams.

#### c. Configure Patient Info

- Enter weight and height of the subject.

#### d. Configure Auxiliary Info

1. Enter **Tether Height** (from earlier setup).
2. Configure **CoM Type**:
   - Use preset ratio based on sex or input a custom value.

#### e. Configure Stream Controls

1. Switch off Marker if not using a marker stream.
2. Click **Initiate** to search for streams using specified props.
3. View log output to verify stream connection.
4. Click **Start** to begin streaming and plotting.
5. Use **Channel Select** to change plotted channel number.

#### f. Validation Before Data Collection

- **Sensor plots (blue)** and **markers (orange xlines)** must be visible.
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

- **Red**: Lean angle too large.
- **White**: Lean angle too small.
- **Green**: Target angle reached — ready to release.
- Works with **Lean Torque** if selected.

#### i. Calibration (Experimental)

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

