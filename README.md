# PIC18F4550_PICDEM_FS_USB_board
updated software for the PICDEM FS USB demonstration board using Microchip 2008 MLA, MPLAB X 5.1 and XC8 V2.05
Based on the MICROCHIP MLA ( https://www.microchip.com/en-us/tools-resources/develop/libraries/microchip-libraries-for-applications )
This updates the Demo to a HID protocol 
USB address:
    0x04D8,                 // Vendor ID
    0x0054,                 // Product ID: Custom HID device demo
    
 64 bit words 
 
 Endpoint address 0x81
 
 USB commands   
    -0x80  - TOGGLE_LED
    -0x81 -  GET_BUTTON_STATUS (Buffer[1] 1/0 for switch up down
    -0x37 -  READ_POTENTIOMETER(Buffer [1] - LSB, Buffer [2] = MSB) 10 bit ADC
        0x93 -  READ_TEMP (via SPI) (Buffer[1] = byte 1, Buffer [2] = byte 2 
        
 The temaperture sensor has a 12 bit word structure.
 
 Python to read bytes =    temp_word=(byteread[1]<<8 |byteread[2])
           to read temp    temp_word>>7  (positive whole values)
           and             temp_word>>3 & 0b00000111 (positive decimal values)
 if temp_word bit 16 set, negitive temp and requires 2's complement of values.
 
 RS232 set at 57600 bit/sec, 8 bits, 1 stop bit no parity. Sends hello world message on start-up 
 Handbook to board (DSS1526A) in project file. 
 
 Using USB communicate with a windows computer python appication may need the driver changing (using a program such as zadig v 2.5) 
 - this has been tesed using Windows 10 & the libusb - win32 driver assocated with the vendor ID/product ID

USN has been tested witha raspbery Pi running Python 3 with no problems (accept needing to run in admin mode or update USB sercurity file) 

