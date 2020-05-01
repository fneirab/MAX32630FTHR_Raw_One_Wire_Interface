# MAX32630FTHR Raw 1-Wire Interface
Firmware plus GUI for the MAX32630FTHR that exposes a raw 1-Wire interface so customers can use the system as tool to help read and decipher 1-Wire data sheet commands for the 1-Wire and iButton devices sold by Maxim.<br>

<b>Required Components</b>:
<ul>
<li>MAX32630FTHR + USB Cable + MAX32630PICO (to load the Firmware)</li>
<li>Access to the GUI and Firmware</li>
<li>Any number of 1-Wire devices</li>
<li>Hardware to create a 1-Wire device bus</li>
</ul>

<b>Setup</b>:
<ul>
<liThe MAX32630FTHR (FTHR) must be attached to your PC via Serial Port for the communication pathway to be established between the GUI and the FTHR </li>
<li>The 1-Wire devices can be either Parasite Powered or supplied with 3.3-5V</li>
<li>A logic analyzer or oscilloscope is helpful to connect to the bus and see the waveforms being generated by the One Wire Master and Slaves</li>
<li>The FTHR must be loaded with the distributed firmware and the GUI must be installed on your PC</li>
<li>When the GUI process begins, the Maxim Splash Screen will appear. This is something everyone else experiences and is a normal part of growing up and running programs</li>
<li>After 3 seconds, the Maxim Splash Screen will disapppear and the 'Connect to Serial Port' screen will appear. This screen is where you will connect your serial port to the FTHR</li>
<li>Press the 'Search' button to populate the list of COM ports. Select the COM port that the FTHR is connected to, and press the 'Connect' button</li>
<li>Once you are connected to a Serial port, the Main Program will appear and specify the COM port and Baud rate, as well as the firmware version</li>
</ul>

<b>Usage</b>:
<ul>
<li>On the Left side of the Screen are all of the ROM layer commands</li>
<ul>
<li>Standard Search: Populates the dropdown list with ROM ID's of devices on the bus</li>
<li>Alarm Search: Populates the dropdown with ROM ID's of actively alarming devices</li>
<li>When a device is selected in the dropdown, that device's ROM ID will be used in any ROM Command that must specify the device (Match ROM and OD Match ROM)</li>
<li>To issue a ROM Command, simply select the command and press 'Send ROM Command' </li>
<ul>
<li>Note: Not all ROM commands will work at all times (Read ROM on a multi-device bus). Ensure that the command you are trying to issue is within the 1-Wire specs</Li>
</ul>
</ul>
<li>Once a ROM command is issued and a specific device is selected, then any of the device's Function Commands can be issued by entering the command's Hex values in the Text box and pressing 'Send Data + Pullup Option'</li>
<ul>
<li>If the Function Command requires more than 1 byte, then the string can be issued all at once (1 press of the send button) or separately (More than 1 press of the send button)</li>
<li>If the Function Command requres a strong pull up on the bus, then write the command to the text box but before pressing send, change the selection in the box to Strong Pull-up After Writing Bit/Byte.</li>
<ul>
<li>To get back into normal power mode, just change the selection back to normal and press 'Send Data + Pull-up Option' again</li>
</ul>
</ul>
<li>Output from the bus and the firmware is displayed in the Text Box on the right side of the screen</li>
<li>LED Indicator on the FTHR will blink red while the board initializes the 1-Wire Master</li>
<li>LED will cycle from Blue to Green when commands are received</li>
</ul>

<b>Example</b>:<p>
Following along with the DS18B20 datasheet on page 18, this will demonstrate how to use this program to mirror the operations
DS18B20 Operation Example 1:
<ol>
<li> <p>
<ul>
<li>Standard Search (to obtain ROM ID's)</li>
<li>Select a ROM ID from the dropdown</li>
<li>Select 'Reset + Match ROM'</li>
<li>'Send ROM Command'</li>
</ul>
</li>
<li><p>
<ul>
<li>Enter '44' into 'Data to Send'</li>
<li>Change the selection from Normal to Strong Pull-Up after Writing Byte</li>
<li>'Send Data + Pull-Up Option'</li>
<li>Change selection back to 'Normal'</li>
<li>'Send Data + Pull-Up Option'</li>
</ul>
</li>
<li><p>
<ul>
<li>Select the same ROM ID from the list</li>
<li>'Reset + Match ROM'</li>
<li>'Send ROM Command'</li>
</ul>
</li>
<li><p>
<ul>
<li>Enter 'BE' into 'Data to Send'</li>
<li>Select 9 in the 'Number of Bytes to Read' +/- box</li>
<li>'Read Bytes'</li>
</ul>
</li>
<li><p><b>Output</b>:
<ul>
<li>9 byte scratchpad, 1st byte is LSB of Temperature; 9th byte is CRC</li>
<li>Note: Should not be a sequence of F's, which indicates unsuccessfull communication</li>
</ul>
</li
</ol><p>
<p>

<b>Decoding</b>:<p>
This program relies on an arbitrary ASCII set of codes that was created by the developer and is hidden from the user when interacting with the GUI. However, if only using the firmware and not the GUI, then you will need these codes to keep the firmware functional by
sending them through the serial port to the FTHR via a serial port terminal program. Each code stands for a 1-Wire command.
<p>
<ul>
<li>ROM Commands:</li>
<ul>
<li>'RMT': Match ROM</li>
<li>'ROM': Overdrive Match ROM</li>
<li>'ROS': Overdrive Skip ROM</li>
<li>'RRI': Read ROM</li>
<li>'RRS': Resume</li>
<li>'RRI': Standard Bus Search</li>
<li>'RSK': Skip ROM</li>
<li>'RAS': Alarm Search</li>
</ul>
<li>Speed Commands:</li>
<ul>
<li>'SNL': Normal Speed</li>
<li>'SOD': Overdrive Speed</li>
</ul>
<li>Read/Write Commands</li>
<ul>
<li>'WWI' + '1/0': Write Bit (1 | 0)</li>
<li>'WRI': Read Bit</li>
<li>'WWY' + data: Write Bytes and the data to write</li>
<li>'WRY' + numBytes: Read Bytes and the number of bytes to read</li>
</ul>
<li>Pullup Commands</li>
<ul>
<li>'PNO': Normal Pullup</li>
<li>'PWI' + '1/0': Strong Pullup after Writing Bit (1 | 0)</li>
<li>'PWY' + byte: Strong Pullup after Writing Byte and the byte to write</li>
</ul>
</ul><p>
