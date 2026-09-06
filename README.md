**SURFACE SCANNER**

1.  Introduction
    1.  Existing problem
    2.  Limitation of conventional methods
    3.  Proposed solution
    4.  Principle in proposed solution
2.  Objectives
3.  Bill of Materials
    3.1.  Components description
4.  Schematic
    4.1.  Circuit description
5.  Working
    5.1.  Flow chart
    5.2.  Calculations
    5.3.  Pseudocode
    5.4.  Actual code
6. Difficulties faced
7. Limitations
8. Future scopes and extensions
9. Conclusion
10. References
11. Glossary
12. Images

**1. INTRODUCTION**

**1.1 Existing Problem**

Measurement of an object's dimensions, shape, and surface profile is an important requirement in various engineering and industrial applications. However, conventional profile measurement methods are often performed manually, particularly when measurements need to be taken at multiple points along the surface of an object.

Manual measurement requires repeated positioning of the measuring instrument and recording of distance values at different locations. This makes the process tedious and time-consuming and can introduce human errors. Therefore, there is a need for an automated method that can measure the surface profile accurately and consistently.

**1.2 Limitations of Conventional Methods**

Although conventional methods can be used to determine the dimensions and profile of an object, they have several limitations:

-   Measurements are generally **manual and time-consuming**.
-   Taking measurements at multiple points requires repeated human intervention.
-   Manual positioning can result in **inconsistent measurement locations**.
-   Recording several measurements manually increases the possibility of **human errors**.
-   Obtaining a continuous representation of the object's surface profile can be difficult.
-   Repeated measurements of complex or irregular surfaces can require considerable effort.

These limitations motivate the development of an automated system capable of performing measurements at predefined intervals with minimum human intervention.

**1.3 Proposed Solution**

To overcome the difficulties associated with conventional measurement methods, an automated object profiling system is proposed. The system automatically measures the vertical distance between a distance sensor and the surface of the object at regular horizontal intervals.

The sensor is moved along the horizontal direction in discrete steps, and the corresponding distance measurements are recorded at each position. These measurements are then used to reconstruct the surface profile of the object, thereby reducing the need for manual measurements.

**1.4 Principle in proposed solution**

The proposed system uses an ESP32 microcontroller, NEMA 17 stepper motor, DRV8825 motor driver, VL53L1X distance sensor, and a screw-and-nut mechanism to automate the profiling process. The NEMA 17 stepper motor rotates a lead screw through a flexible shaft. The rotation of the lead screw causes the nut, on which the distance sensor is mounted, to move linearly along the horizontal direction. The sensor is moved in discrete steps of 1 mm. At every 1 mm displacement, the motor stops and the VL53L1X sensor measures the vertical distance between the sensor and the object's surface. The measured distance corresponding to each horizontal position is then recorded for profile generation.

**2. OBJECTIVE**

-   To develop an automated object profile scanning system.
-   To integrate sensing, motion control and data processing into a single automated system.
-   To measure the vertical distance between the sensor and the object's surface accurately.
-   To generate the surface profile of the object using distance data obtained at regular intervals.
-   To determine the dimensions and shape of an object from the collected measurements.
-   To achieve accurate linear movement of the sensor using a stepper motor and lead screw mechanism.
-   To provide a reliable and repeatable profiling process.
-   To mitigate vibration and overheating in the system.
-   To improve measurement accuracy and precision when compared to manual methods.

**3. Bill Of Materials**

  Component (Quantity) - Cost in rupees

  NEMA 17(1) - 400

  DRV 8825(1) - 139

  ESP32(1) - 450

  VL53L1X(1) - 282

  Lead Screw(1) - 204

  Nut(2) - 60

  Bread Board(1) - 45

  Jumpers(20) - 20

  Capacitor(1) - 5

  Adapter(1) - 250

  Wooden blocks(3) - 100
  
  Flexible coupler(1) - 52

Total approximate cost required for the project is 2500 rupees.

3.1.  Components description

VL53L1X – Time-of-Flight Sensor  
This sensor measures the distance between itself and an object’s surface. It operates at 2.6–3.5 V and provides precise vertical distance readings during scanning.

ESP32 – Microcontroller  
The ESP32 acts as the main controller of the system. It manages the stepper motor, triggers the distance sensor, and records measurement data.

DRV8825 – Stepper Motor Driver  
This driver receives control signals from the ESP32 and powers the stepper motor. It supports up to 2.2 A per phase and requires 8.2–45 V for motor supply and 3.3–5 V logic input.

NEMA 17 – Stepper Motor  
The NEMA 17 motor runs on 12 V and draws 1.2–1.6 A. Its rotation drives the lead screw, converting rotary motion into precise linear movement.

12 V, 1.5 A Adapter – Power Supply  
This adapter provides the main DC power for the motor and driver circuit. It delivers a stable 12 V output with a maximum current of 1.5 A.

**4. CIRCUIT DIAGRAM**



Fig. No.:4.1 Schematic of the circuit

The above circuit diagram made with KICAD software shows the connections of ESP 32 micro-controller with sensor and motor driver, along with the connection of motor driver with the motor.

**4.1 CIRCUIT DESCRIPTION**

The circuit consists of an ESP32 microcontroller, a VL53L1X Time-of-Flight distance sensor, an DRV 8825 stepper motor driver, a NEMA 17 stepper motor and a 12 V power supply. The ESP32 coordinates the movement of the stepper motor, acquisition of distance measurements from the sensor and transfer the data serially to the laptop.

A 12 V DC supply is connected to the VMOT pin of the DRV 8825 motor driver to power the stepper motor. A 1000 μF capacitor is connected across the motor supply terminals to suppress voltage spikes generated and ensure stable power delivery. The VDD pin of the DRV 8825 is connected to the 3.3 V supply, while the ground terminals of all modules are connected together as a common reference.

The NEMA 17 stepper motor is connected to the output terminals of the DRV 8825 driver. The driver controls the motor windings and converts the STEP and DIRECTION signals received from the ESP32 into the required sequence of currents for motor rotation.

GPIO18 of the ESP32 is connected to the STEP pin of the DRV 8825 and is used to generate step pulses, while GPIO19 is connected to the DIRECTION pin to control the direction of motor rotation. The ENABLE pin is tied to GND to activate the driver which is active LOW. The MS1, MS2 and MS3 pins are tied to GND as no micro-stepping is required for the operation. The RESET and SLEEP pins are connected together and held high to keep the driver active during operation.

The VL53L1X distance sensor measures the distance between the sensor and the object surface at multiple points of regular intervals. The sensor is powered using the 3.3 V supply and communicates with the ESP32 through the I2Cprotocol. GPIO22 of the ESP32 is connected to the SDA (Serial Data) pin of the sensor, while GPIO21 is connected to the SCL (Serial Clock) pin. Through this interface, the ESP32 periodically requests and receives distance measurements from the sensor.

During operation, the ESP32 sends step pulses to the DRV 8825 driver, causing the stepper motor to rotate the lead screw mechanism. The rotation of the lead screw translates into linear motion of the sensor. At each predefined displacement interval, the motor is stopped and the VL53L1X sensor measures the distance to the object surface. These measurements are received and sent to the laptop through serial communication.

**5. WORKING**

The object profiling system operates by moving a distance sensor horizontally above the object and recording distance measurements at regular intervals of 1mm. The complete setup consists of a NEMA 17 stepper motor, lead screw mechanism, VL53L1X distance sensor, ESP32 microcontroller and a Python-based graphical interface.

The stepper motor is mounted at one end of the setup and is mechanically coupled to a lead screw through a flexible coupling shaft. A nut is mounted on the lead screw and constrained such that it cannot rotate along with the screw. As a result, when the lead screw rotates, the nut traverses linearly along the length of the screw.

The VL53L1X distance sensor is fixed to the lead screw nut. The entire lead screw assembly is mounted horizontally at a certain height above the table surface. The object to be profiled is placed directly below the sensor path so that the sensor can measure the distance between itself and different points on the object's surface.

When the system is started, the ESP32 generates STEP and DIRECTION signals for the DRV 8825 motor driver. The driver rotates the stepper motor, causing the lead screw to rotate. This results in horizontal movement of the sensor from one end of the object to the other.

At predetermined intervals of 1 mm of linear displacement, the ESP32 acquires a distance measurement from the VL53L1X sensor through the I2C communication interface. The measured distance value represents the separation between the sensor and the object's surface at that particular horizontal position.

The ESP32 continuously transmits the collected distance data to a computer through serial communication. A Python-based application running on the computer receives the data, processes it and plots the measurements graphically. Each measurement point corresponds to a specific position along the object's length.

As the sensor traverses across the object and measurements are collected at multiple locations, a complete set of surface profile data is obtained. The graph is plotted and the ends of each line segment is joined to represent the object surface. From this profile, the shape, dimensions and surface characteristics of the object can be determined.

The automated scanning process reduces manual measurement effort while improving the consistency and repeatability of profile measurements.

**5.1 FLOW CHART**

 

Fig.No.:5.1Flow of working

**5.2 CALCULATIONS**

Distance sensor moves before each stop

Pitch of screw(p) = 2mm

Number of revolutions = N

Distance sensor moves before each stop(D) = p\*n

Step of motor = 1.8 degree

D = 1mm

N = D/p = 1mm / 2mm = 0.5 rotation

The motor shaft has to rotate 180 degrees for every reading.

Reference voltage for motor driver

**Vref = Imax \* 0.5 \* R**

R = 1 ohm

Imax required is 1.2 A

Vref = 0.6 V

**5.3 PSEUDO-CODE**

**MOVEMENT**

Move sensor to initial position

Set ROI for the sensor

For specified distance

Rotate the motor shaft

For every 1mm  

Stop motor

Trigger the sensor

Send the position and distance to laptop via serial communication

End loop

End loop

**PYTHON CODE**

Initialize empty arrays for height and distance

Read the data

Store the data

Plot horizontal lines for each distance to plot graph between distance and height

Join the end of line segments

End

If distance is constant

Shape = cuboidal

Else if distance decreases and then increases uniformly

Shape = spherical

Else

Shape = irregular

Return shape

End

**5.4 ACTUAL CODE**

**ESP 32 CODE**

**#include <Wire.h>**

**#include <Adafruit\_VL53L1X.h>**

**#define STEP\_PIN 3**

**#define DIR\_PIN 4**

**const int stepsPerMove = 100; // 100 steps = 1 mm**

**const int stepDelay = 800; // microseconds between steps**

**const int pauseTime = 1000; // t = 1 second pause**

**const int totalCycles = 250; // number of measurements**

**Adafruit\_VL53L1X vl53 = Adafruit\_VL53L1X();**

**void setup()** 

**{**

  **pinMode(STEP\_PIN, OUTPUT);**

  **pinMode(DIR\_PIN, OUTPUT);**

  **digitalWrite(DIR\_PIN, HIGH); // set movement direction**

  **Serial.begin(9600);**

  **Wire.begin();**

  **if (!vl53.begin(0x29, &Wire))** 

  **{**

    **Serial.println("VL53L1X not detected");**

    **while (1);**

  **}**

  **vl53.startRanging();**

  **// -------- ROI SETTINGS (OPTIONAL) --------**

  **// vl53.setROI(8,8);**

  **//vl53.setTimingBudget(100);**

**}**

**void loop() {**

  **for (int cycle = 0; cycle < totalCycles; cycle++)**

  **{**

    **for (int i = 0; i < stepsPerMove; i++)** 

    **{**

      **digitalWrite(STEP\_PIN, HIGH);**

      **delayMicroseconds(stepDelay);**

      **digitalWrite(STEP\_PIN, LOW);**

      **delayMicroseconds(stepDelay);**

    **}**

    **delay(pauseTime);**

    **if (vl53.dataReady())** 

    **{**

      **int distance = vl53.distance(); // distance in mm**

      **vl53.clearInterrupt();**

      **Serial.println(distance); // send to Python**

    **}**

  **}**

  **while (1);**

**}**

**PYTHON CODE**

**import serial**

**import matplotlib.pyplot as plt**

**import time**

**ser = serial.Serial('COM4', 9600)**

**time.sleep(2)**

**distances = \[\]**

**print("Collecting data...")**

**file = open("distance\_data.txt", "w")**

**while len(distances) < 250:**

    **if ser.in\_waiting > 0:**

        **data = ser.readline().decode('utf-8').strip()**

        **try:**

            **distance = float(data)**

            **distances.append(distance)**

            **file.write(str(distance) + "\\n")**

            **print(distance)**

        **except:**

            **pass**

**ser.close()**

**file.close()**

**heights\_mm = list(range(len(distances)))**

**plt.figure(figsize=(6,8))**

**for h, d in zip(heights\_mm, distances):**

    **plt.hlines(y=h, xmin=0, xmax=d, linewidth=0.5)**

**plt.xlabel("Distance (mm)")**

**plt.ylabel("Height (mm)")**

**plt.title("Vertical Scan Profile")**

**if len(distances) > 0:**

    **plt.xlim(0, max(distances)+2)**

    **plt.ylim(0, max(heights\_mm))**

**plt.grid(True)**

**plt.show()**

**6. DIFFICULTIES FACED**

A significant amount of time was spent on procuring the components with the required specifications. Finding compatible and precise mechanical parts was difficult, especially because this was our first experience working with mechanical systems.

Ensuring proper compatibility between components was challenging. For example - Selecting a shaft coupler that fits both the 8 mm lead screw and the 4 mm motor shaft required careful selection.

Achieving proper tightening between the motor shaft, coupler and lead screw was difficult and thus took multiple adjustments.

Identifying a suitable nut for the lead screw was challenging. If too loose caused unwanted rotation and if too tight it led to jamming. Achieving the right balance was critical for smooth linear motion.

Fixing the time-of-flight sensor securely onto the nut was not straightforward. Proper mounting was required to ensure stability and accurate readings.

Setting the right reference voltage for the motor driver was very crucial because a higher one leads to overheating on continuous operation and a lower one affects the motion so an optimum 0.6 V was fixed.

Designing and building a proper base for the entire setup was challenging. Horizontal placement of the entire setup reduced the vibrations significantly that was observed when the complete system was vertically placed.

**6. LIMITATIONS**

The accuracy of the object profiling system is dependent on the performance and measurement capability of the VL53L1X distance sensor. Variations in ambient lighting, surface reflectivity, surface texture, and the angle of the object's surface may affect the measured distance. Highly reflective, transparent, dark, or irregular surfaces may therefore result in inaccurate or inconsistent readings.

The 1 mm scanning interval limits the spatial resolution of the obtained profile. Features or surface variations that are smaller than the scanning interval may not be detected accurately. Therefore, very small surface irregularities may be missed during the profiling process.

The accuracy of the linear movement also depends on the stepper motor, DRV8825 driver, lead screw, and mechanical assembly. Mechanical backlash, shaft misalignment, vibrations, or missed motor steps can cause errors in the actual position of the sensor. These errors can affect the correspondence between the measured distance and the assumed horizontal position.

The system requires the object to be positioned properly below the sensor's scanning path. The object should remain sufficiently stationary and within the measurable range of the sensor throughout the scanning process. Objects with highly irregular geometries, steep slopes, or discontinuous surfaces may be difficult to profile accurately because the sensor may not obtain reliable measurements at every position.

Finally, the developed system is primarily intended for surface profile measurement over a defined horizontal scanning range. Its performance is limited when profiling objects with one dimension and geometries outside the mechanical travel range of the lead screw or the measurement range of the VL53L1X sensor.

**8. FUTURE SCOPES AND EXTENSION**

The developed object profiling system successfully demonstrates the automated measurement of an object's surface profile. However, several improvements and extensions can be incorporated in future versions to enhance its functionality and performance.

A higher-resolution distance sensor can be used to improve measurement accuracy and obtain finer surface details. The mechanical structure can also be strengthened to further reduce vibrations and improve the stability of the scanning process.

The current system performs one-dimensional profiling along a single axis. By introducing an additional motorized axis, the system can be extended to perform two-dimensional or three-dimensional surface scanning. This would enable the reconstruction of complete object geometries rather than a single surface profile.

Wireless communication features such as Wi-Fi or Bluetooth can be integrated to allow remote monitoring and control of the system.

Furthermore, advanced data processing techniques and machine learning algorithms can be employed to automatically identify object shapes, detect surface defects and perform dimensional analysis.

**9. CONCLUSION**

The objective of this project was to develop an automated object profiling system capable of determining the shape and dimensions of an object from its surface profile. The system was successfully implemented using an ESP32 microcontroller, VL53L1X Time-of-Flight distance sensor, NEMA 17 stepper motor, DRV 8825 motor driver and a lead screw-based linear motion mechanism.

The developed setup enabled controlled horizontal movement of the sensor across the object while acquiring distance measurements at regular intervals. The collected data was transmitted to a computer and processed using a Python interface to generate a graphical representation of the object's surface profile. This profile is used to determine the shape and dimensions of the scanned object.

Throughout the project, various mechanical and electronic challenges were encountered and addressed, leading to improvements in system stability and measurement reliability. In particular, adopting a horizontal mounting arrangement significantly reduced vibrations and improved the overall performance of the system.

The project demonstrates the successful integration of embedded systems, motion control, sensing and software-based data visualization. The developed system provides an efficient and automated alternative to manual profile measurement methods, reducing human effort while improving consistency and repeatability.

**10. REFERENCES**

Stepper motor working

[https://youtu.be/09Mpkjcr0bo?si=Yd8CdWGqq6XWO\_gY](https://youtu.be/09Mpkjcr0bo?si=Yd8CdWGqq6XWO_gY)

Integrating motor with driver

[https://youtu.be/wcLeXXATCR4?si=uZfmRSPwtpjuv6Zl](https://youtu.be/wcLeXXATCR4?si=uZfmRSPwtpjuv6Zl)

Supporting rod idea

[https://www.youtube.com/shorts/akqacnu7kJ4](https://www.youtube.com/shorts/akqacnu7kJ4)

Working the Proximity sensor.

[https://zbotic.in/vl53l1x-time-of-flight-sensor-precise-ranging-up-to-4m/?srsltid=AfmBOopAkQ40DWXfBDbguCaA7bVED1MmyE2NDeD-HNDJ-9OKYy6PKVk-](https://zbotic.in/vl53l1x-time-of-flight-sensor-precise-ranging-up-to-4m/?srsltid=AfmBOopAkQ40DWXfBDbguCaA7bVED1MmyE2NDeD-HNDJ-9OKYy6PKVk-)

Industrial scanner

[https://hexagon.com/products/product-groups/measurement-inspection-hardware/3d-laser-scanners](https://hexagon.com/products/product-groups/measurement-inspection-hardware/3d-laser-scanners)

**11. GLOSSARY**

ESP32: A microcontroller used to control the overall operation of the system.

VL53L1X: A Time-of-Flight (ToF) distance sensor used to measure the distance between the sensor and the object surface.

Time-of-Flight (ToF): A distance measurement technique that calculates distance based on the time taken by light to travel to an object and return.

Stepper Motor: An electric motor that rotates in precise angular steps, enabling accurate position control.

NEMA 17: A standard-sized stepper motor used to provide rotational motion for the lead screw mechanism.

DRV 8825: A stepper motor driver module used to control the operation of the stepper motor and provide the required current for the motor.

Lead Screw: A mechanical component that converts rotational motion into linear motion here.

Lead Screw Nut: A component that moves linearly along the lead screw when the screw rotates.

Surface Profile: The graphical representation of the shape and contour of an object's surface.

I2C (Inter-Integrated Circuit): A communication protocol used for data exchange between the ESP32 and the VL53L1X sensor.

SDA (Serial Data): The data transmission line used in I2C communication.

SCL (Serial Clock): The clock signal line used in I2C communication.

GPIO (General Purpose Input/Output): Programmable pins of a microcontroller used for interfacing with external devices.

STEP Signal: A control signal that determines the number of steps taken by the stepper motor.

DIRECTION Signal: A control signal that determines the direction of rotation of the stepper motor.

Micro-stepping: A technique used to divide a motor step into smaller increments for smoother and more precise movement.

Serial Communication: A method of transferring data sequentially between the ESP32 and a computer.

Region of Interest (ROI): A configurable sensing area of the VL53L1X sensor used to reduce unwanted measurements.

**12. Images**

12.1 CIRCUIT

https://github.com/TECS-TheelectronicsclubatSASTRA/Surface_Scanner/blob/main/Images/12.1%20Circuit.jpeg

12.2 ARRANGEMENT



12.3 OUTPUT

