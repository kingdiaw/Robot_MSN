# Note Minggu Sains Negara xx October 2024
## Activity 1: The tasks for controlling Motor A and Motor B using the RZDriver library:
### ESP32 I/O Mapping
| **ESP32** | **Devices**         |
|-----------|---------------------|
| D5        | RC-CH1              |
| D18       | RC-CH2              |
| D19       | RC-CH3              |
| D12       | BUZZER              |
| D14       | Motor B Backward    |
| D27       | Motor B Forward     |
| D26       | Motor A Backward    |
| D25       | Motor A Forward     |
## Step-by-Step Procedure
### 1.Install the RZDriver Library:
- Open the terminal or command prompt.
- Clone the RZDriver library repository from GitHub:
```bash
git clone https://github.com/kingdiaw/RZ7886Driver.git
```
- Copy the downloaded library folder `RZ7886Driver` to your Arduino libraries folder, typically located at `Documents/Arduino/libraries` on most systems.

### 2.Open the Example Sketch:
- Launch the Arduino IDE.
- Go to **File > Examples > RZ7886Driver > ESP32_RZ_Basic**.
- This will open the example sketch for controlling motors using the RZDriver library.

### 3.Instantiate Motor Objects:
- In the example sketch, create instances of RZDriver for Motor A and Motor B using their respective pins:
```cpp
RZDriver motorA(25, 26); // Motor A: Forward pin D25, Backward pin D26
RZDriver motorB(27, 14); // Motor B: Forward pin D27, Backward pin D14
```
### 4.Alter Code to Move Motor A Clockwise:
- To move Motor A clockwise, set the speed to a positive value:
```cpp
motorA.setSpeed(255);  // Maximum speed in the clockwise direction
```

### 5.Alter Code to Move Motor A Anticlockwise:
- To move Motor A anticlockwise, set the speed to a negative value:
```cpp
motorA.setSpeed(-255);  // Maximum speed in the anticlockwise direction
```
### 6.Alter Code to Move Motor B Clockwise:
- Similarly, to move Motor B clockwise, set the speed to a positive value:
```cpp
motorB.setSpeed(255);  // Maximum speed in the clockwise direction
```
### 7.Alter Code to Move Motor B Anticlockwise:
- To move Motor B anticlockwise, set the speed to a negative value:
```cpp
motorB.setSpeed(-255);  // Maximum speed in the anticlockwise direction
```
### 8.Move the Robot Forward for 2 Seconds and Stop:
- Set both motors to move forward by setting their speeds to positive values:
```cpp
motorA.setSpeed(255);  // Forward full speed for Motor A
motorB.setSpeed(255);  // Forward full speed for Motor B
delay(2000);           // Move forward for 2 seconds
motorA.setSpeed(0);    // Stop Motor A
motorB.setSpeed(0);    // Stop Motor B
```
### 9.Move the Robot Backward for 2 Seconds and Stop:
- Set both motors to move backward by setting their speeds to negative values:
```cpp
motorA.setSpeed(-255); // Backward full speed for Motor A
motorB.setSpeed(-255); // Backward full speed for Motor B
delay(2000);           // Move backward for 2 seconds
motorA.setSpeed(0);    // Stop Motor A
motorB.setSpeed(0);    // Stop Motor B
```
### 10.Turn the Robot Right (90 Degrees) and Stop:
- To turn right, set Motor A to move forward and Motor B to move backward:
```cpp
motorA.setSpeed(255);  // Forward full speed for Motor A
motorB.setSpeed(-255); // Backward full speed for Motor B
delay(500);            // Adjust time for a 90-degree right turn
motorA.setSpeed(0);    // Stop Motor A
motorB.setSpeed(0);    // Stop Motor B
```
- Adjust the **delay** time (**500** in this case) based on your robot's turning radius and speed.

### 11.Turn the Robot Left (-90 Degrees) and Stop:
- To turn left, set Motor A to move backward and Motor B to move forward:
```cpp
motorA.setSpeed(-255); // Backward full speed for Motor A
motorB.setSpeed(255);  // Forward full speed for Motor B
delay(500);            // Adjust time for a 90-degree left turn
motorA.setSpeed(0);    // Stop Motor A
motorB.setSpeed(0);    // Stop Motor B
```
- Similarly, adjust the **delay** time to achieve a -90-degree turn.
## Notes:
### Upload and Test:
- After making each modification, compile the code and upload it to your ESP32 using the Arduino IDE.
- Test each function to ensure that the motors and robot behave as expected.
- The maximum and minimum speeds are set to 255 and -255 respectively as per the setSpeed() method in the RZDriver library.
- Adjust the delay times (2000 for moving forward/backward and 500 for turning) based on the actual performance of your robot to achieve precise movements.
- Refer to the RZDriver library code for more details on how the library functions and customize further as needed.

## Activity 2: To control the robot movement using a remote control, follow these steps. This guide includes downloading an APK file for remote control, setting up the ESP32 with example code, and writing code to handle remote signals for robot movement.
### Step-by-Step Procedure
### 1. Download the APK for Remote Control
- Use a QR code scanner app on your smartphone to scan the provided QR code.
<p align="center">
  <img src="image/remoteBT_apk_qr-code.png" alt="QR Code" width="200"/>
</p>
  
- The QR code will direct you to a download link for the APK file.
### 2. Write the Example Code for Testing Remote Control Functionality
- Open Arduino IDE.
- Open an **File >Examples >RZDriver >ESP32_RZ_BT**
- Change your Bluetooth name's `String device_name = "ESP32-BT-Slave"` from ESP-BT-Slave to your prefer.

### 3.Write the loop() Function to Handle Remote Control Signals:
- Use the `loop()` function to read signals from the Bluetooth remote control and control the motors:
```cpp
 void loop() {
  if (SerialBT.available()) {
    char command = SerialBT.read();

    switch (command) {
      case 'F':  // Move Forward
        motorA.setSpeed(255);
        motorB.setSpeed(255);
        break;
      case 'B':  // Move Backward
        motorA.setSpeed(-255);
        motorB.setSpeed(-255);
        break;
      case 'L':  // Turn Left
        motorA.setSpeed(-255);
        motorB.setSpeed(255);
        break;
      case 'R':  // Turn Right
        motorA.setSpeed(255);
        motorB.setSpeed(-255);
        break;
      case 'S':  // Stop
        motorA.setSpeed(0);
        motorB.setSpeed(0);
        break;
      default:
        motorA.setSpeed(0);
        motorB.setSpeed(0);
        break;
    }
  }
  delay(20); // Small delay for stability
}
```
### 4.Upload the Code to the ESP32:
- Connect your ESP32 to your computer via USB.
- Select the appropriate board and port from **Tools** > **Board** and **Port** in the Arduino IDE.
- Click the upload button to compile and upload the code to your ESP32.

### 5. Test the Remote Control Functionality
#### 5.1 Pair Your Smartphone with the ESP32:
- Open the Bluetooth settings on your smartphone.
- Pair with the ESP32 device named "ESP32-BT-Slave" (or whatever name you used in `String device_name`).
#### 5.2 Open the Remote Control App:
- Launch the APK file you installed earlier.
- Connect to the paired ESP32 device through the app.
#### 5.3 Control the Robot:
Use the remote control app to send commands:
- **Forward**: Robot moves forward.
- **Backward**: Robot moves backward.
- **Left**: Robot turns left.
- **Right**: Robot turns right.
- **Stop**: Robot stops all movement.

#### 5.4 Troubleshooting:
- If the robot does not respond, check the serial monitor in Arduino IDE to see if commands are being received.
- Ensure the Bluetooth connection is stable and the motors are connected correctly.

By following these steps, you will be able to control your robot using the remote control app via Bluetooth, allowing for dynamic movement and navigation based on remote commands.


