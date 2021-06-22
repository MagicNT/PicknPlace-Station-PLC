# PLC Project: Commissioning of a Pick and Place Station


## Introduction
A Programmable Logic Controller (PLC) is a manufacturing data processing machine that consistently controls the state of input instruments and operates with the help of a programmed code the state of output machines. The topic of this paper which is the Pick and place machines, have become the most used PLCs in present-day manufacturing companies. Continuously referred to as being straightforward, repetitive and with the simple operations that these devices generally outdo at, pick and place robots offer a vast number of advantages for producers. The following paper will describe and detail the design of a Pick and Place station that can run in automatic/manual mode and has stop/start/reset input buttons to control the station.

## Interface

### INPUTS
Symbol	| Address| Comment
--- | --- | ---
part_available	| I 124.0	| First sensor in the program, indicates the availability of a housing work piece
mini_slide_retracted|	I 124.1	| Indicates that the mini slide is pulled in
mini_slide_extended|	I 124.2	|Indicates that the mini slide is expanded
mini_slide_up	|I 124.3	|Indicates that the mini slide is upwards
workpiece_picked_up	|I 124.4	|Indicates that the token is acquired
workpiece_at_processing	|I 124.5	|Indicates that the token is being monitored
no_workpiece	|I 124.6	|Indicates that no token is being monitored
downstream_station	|I 124.7	|Synchronization signal to indicate the availability of the housing piece at the end of the trajectory
start	|I 125.0	|It initiates the system
stop	|I 125.1	|It stops the system
auto_man	|I 125.2	|It indicates whether the operations should be performed automatically or manually
reset	|I 125.3	|It resets the system


### RELAYS
Symbol|	Address	|Comment
---|---|---
start_relay|	M 0.0|	

### OUTPUTS
Symbol	|Address	|Comment
---|---|---
conveyor_motor_on|	Q 124.0	|Activate or turn off the belt
retract_mini_slide|	Q 124.1|	Retract the mini-slide (using 5/2 valve)
extend_mini_slide|	Q 124.2|	Extend the mini-slide  (using 5/2 valve)
move_mini_slide_down	|Q 124.3	|Move the mini-slide downwards/upwards (using 3/2 valve)
vacuum_on	|Q 124.4	|Turn on/off the vacuum
extend_seperator	|Q 124.5	|Extend/retract the separator
station_occupied|	Q 124.6|	Synchronization output for the neighboring station
LED_start	|Q 125.0|	Indicates that the system has been initiated
LED_reset	|Q 125.1	|Indicates that the system has been reset

### For documenting purposes, here is the symbols table used in the project:
![1](https://user-images.githubusercontent.com/86275885/122997626-95f4f500-d382-11eb-8f56-bbbc28fa160d.png)


## Program


![2](https://user-images.githubusercontent.com/86275885/122997931-dc4a5400-d382-11eb-96e7-5ab640ace127.png)
![3](https://user-images.githubusercontent.com/86275885/122997928-dbb1bd80-d382-11eb-9a6c-07bc545940b9.png)
![4](https://user-images.githubusercontent.com/86275885/122997926-db192700-d382-11eb-997b-88064d70776e.png)
![5](https://user-images.githubusercontent.com/86275885/122997924-db192700-d382-11eb-84f5-8a929328da60.png)
![6](https://user-images.githubusercontent.com/86275885/122997923-da809080-d382-11eb-9d02-84da35b696b6.png)
![7](https://user-images.githubusercontent.com/86275885/122997921-da809080-d382-11eb-8ea6-bd3f303c23a8.png)
![8](https://user-images.githubusercontent.com/86275885/122997916-d9e7fa00-d382-11eb-8b35-d833a1cb4c56.png)
![9](https://user-images.githubusercontent.com/86275885/122997913-d94f6380-d382-11eb-8c5a-1985a152923d.png)


## Flowchart


![6](https://user-images.githubusercontent.com/86275885/122998305-406d1800-d383-11eb-902f-b3494f2db90f.png)


## Commentary
-	The system starts off through a reset button press. This button will reset the conditions of all components to a ready state for the system to restart (retract mini-slide, move mini-slide up, stop conveyor, close separator and turn off vacuum).
-	This button press is accompanied by a blinking LED signal on the button itself.
•	Once the system is reset, the user can now start the operation by first choosing a mode: either automatic (continuous loop) or manual.
-	The start button when pressed is accompanied by a turned ON LED placed on the button itself. This light will not turn off in automatic mode but will turn off in manual mode once the operation has concluded.
-	The stop emergency button is used to completely freeze the Pick and Place system at any moment in time. The system will not return to operation until the user presses the reset button. After this reset button press, the system returns to the initial state it has begun with in the first place. 
-	The operations on this station required precision time study to be carried out in order to make sure that we optimize every single step and make the runtime as fast and efficient as possible.
-	For this purpose, many timers were implemented to synchronize every step throughout the program flow and make sure every part of the operation is on time.
-	It was noticed that the conveyor suffers from a maladjustment that leads to the placement of the insert work piece on top of the housing work piece in a deviated non-centered manner so in order to resolve this problem it was decided to rather let go the insert work pieces on top of the processed housing work pieces and then press them into place using the mini-slide’s downward/upward motion.
-	The mini-slide uses a 5/2 valve to create the extract/extend motion and a 3/2 valve to create the upward/downward motion. It also has sensors to detect the extracted/extended and moved up status.
-	The conveyor is controlled using a motor which we control the state using the user-controlled conveyor-on output.
-	The separator is used to stop the pieces exactly under the specified location so that the mini-slide can place its insert pieces unto the housing work pieces.
-	There are 3 sensors placed on the conveyor to dictate the movement of the housing pieces and organize the operation so that at a specified moment there is only one housing piece under the mini-slide.
-	The system provided in this paper can simultaneously handle 2 pieces appropriately spaced on the conveyor and send them off in an organized manner out to the next station.
-	In the below picture we have the Function bock diagram which is the design code we displayed previously and we have placed unto its initiate-sequence input the stop signal to freeze the system. And on a new network line we have made the stop button which is normally closed, stop the conveyor motor to save power and prevent energy leak.

![1](https://user-images.githubusercontent.com/86275885/122998352-4e229d80-d383-11eb-8c05-a47013e0d88e.png)

## Conclusion
The flexibility of a pick and place machine is proven through its capability to adjust, monitor, assemble devices and other mechanical concrete tasks that enhance the global condition of manufacturing and decrease time waste. Pacing improves productivity, as pick and place mechanism transport merchandise automatically, which is indeed faster and more efficient than manual labor work that replaces it. 


