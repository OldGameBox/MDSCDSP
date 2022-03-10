# MDSCDSP
Multi Device Server Centralized Data Swap Protocol

# Project in process

#cAlgorithm:
All devices are connected to the main frame and have their own connection code that is stored only on the main frame and on the devices.
Device and main frame never send connection code to each other!
To connect main frame to device first time the server need to create new connection code and send it to device.
After first connection the device and the main frame are ready to swap data between each other.

# Swapping scheme:
To send info from device to main frame and vise versa each of device needs to understand sended info.
For this reason there is a Swapping Information Codec - SIC.

# MDSCDSP supports only three types of devices:
1) Server (Main Frame) - high priority devices that can get almost any inforamtion about connected device.
2) Device - low priority device that is able to get limited informtion from server and can't work with other devices except main frame.
3) Controller - mid priority device used to control main abilities of connected to the server devices.

All recieved inforamtion doesn't contain any senders, so no one can create a history of swapped inforamtion without all devices.

# Decoded inforamtion scheme:
    {OPERATION : DATA : VALUE|}

OPERATION - describes what kind of operation one device want to do with other one.
Types:
    - "GET" - to get information from device.
    - "SET" - to set/update infromation on other device.
    - "INF" - to change high level of secure data on other device.
    - "CAL" - to call function on other device, for example to measure something.

DATA - describes what about device is actually talking about and stores an actual address of data that is stored on other device.
For this each of devices has its on data list, that connects name and value - Swap Values List - SVL.

VALUE - describes on what to change data or what values are going to be used.

":" - used to separete each value
"|" - used to show the end of the swapping inforamtion

All sended inforamtion is encoded, so that no one can read or send swapping inforamtion without a special code, that is able to decode and encode swapping inforamtion.

To encode, decode and analyze there are three protocols: SIE, SID and SIA.

SIE - Swapping Information Encoder - encodes Swapping Information.
SID - Swapping Information Decoder - decodes Swapping Information.
SIA - Swapping Information Analyzer - analyzes Swapping Information to make computer understand what another device talking about.

# Scheme of Swapping Algorithm:
Device #1 >> SIG >> SIE >> {sending} >> SID >> SIA >> PSDS >> Device #2

SIG - Swapping Information Generator
PSDS - Post Swapping Data Saver

If device has a few messages from other device, so not to lose any messages during analyzing other message each device has its own SIUL - Swapped Information Unprocessed List.
This list contains only unprocessed messages.
