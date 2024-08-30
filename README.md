# Note Minggu Sains Negara xx October 2024
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
RZDriver motorA(D25, D26); // Motor A: Forward pin D25, Backward pin D26
RZDriver motorB(D27, D14); // Motor B: Forward pin D27, Backward pin D14
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
 
