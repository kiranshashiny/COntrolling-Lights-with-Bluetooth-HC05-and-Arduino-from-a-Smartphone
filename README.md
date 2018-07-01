# Controlling-Lights-with-Bluetooth-HC05-and-Arduino-from-a-Smartphone

This program will turn the LED connected to an Arduino On or Off depending on what is being sent from the Smartphone.

The App installed from Google PlayStore was https://play.google.com/store/apps/details?id=com.giumig.apps.bluetoothserialmonitor&showAllReviews=true


## Components List :

- Arduino
- HC05 Bluetooth Module
- Arduino Bluetooth App from Google Playstore.
- 330 ohm resistor
- LED


## Connections :

HC05  Arduino

- Rx -> 	Tx
- Tx -> 	Rx
- +5v ->	5V
- GND -> 	GND

( Connecting the Arduino to the LED is not mentioned as it is assumed that the user is familiar with basic connections and schematics )


## The Program

This demo is to show how we can send signals from the Smartphone app ( Android in my case ) to the Bluetooth module which is nearby connected to the Arduino.

The User sends signals like '1' or a '0' which will light up the LED connected to the Arduino, which can be interpreted as Home Automation where the user can control lights in the house to turn off and on.

First Install the app listed below.

Next, upload the code listed in this repo.

Next do the connections from the HC05 to the Arduino.

(If you want to upload repeatedly when the pins of the Arduino Tx and Rx are connected then the Upload will fail. For a short interval when the upload is happening remove the Rx and Tx pins to upload successfully )

 
The Arduino Program is a simple code that reads the serial input and checks if it's a 0 or a 1.

If 0, then the signal is sent to the LED to turn OFF.
If 1, then the signal is sent to turn the LED ON.

		#define ledPin 7
		int state = 0;
		void setup() {
		  pinMode(ledPin, OUTPUT);
		  digitalWrite(ledPin, LOW);
		  Serial.begin( 9600 ); // Default communication rate of the Bluetooth module
		}
		void loop() {
		  if(Serial.available() > 0){ // Checks whether data is comming from the serial port
		    state = Serial.read(); // Reads the data from the serial 
		    Serial.print("state is ");
		    Serial.print (state, DEC);
		    Serial.println(" done");
		 }
		 if (state == '0') {
		  digitalWrite(ledPin, LOW); // Turn LED OFF
		  Serial.println("LED: OFF"); // Send back, to the phone, the String "LED: ON"
		  state = 0;
		 }
		 else if (state == '1') {
		  digitalWrite(ledPin, HIGH);
		  Serial.println("LED: ON");;
		  state = 0;
		 } 
		}



## Challenges faced:

The character being sent from the Smartphone was not getting received properly when the Arduino Serial Monitor was set at 38400 baud.
Setting it to 9600 - got me the right characters being transmitted from the SmartPhone to the HC05.

There is a reset button on the HC05 Controller in case you want to reset the connections.

The Upload of the Arduino Code will not work if the Rx and Tx pins on the Arduino are connected.
To upload new code successfully  unhook the Tx and Rx pins from the HC05 to the Arduino first and then Upload the new code.

## Connecting the HC05 to the SmartPhone App.

- Check that the Bluetooth Module is first identified in the Smartphone. It should say 
- "Connect to Device" and your device has to get identified in the list of other devices.

- There are multiple modes that the SmartPhone app works. I had to choose "Terminal Mode", and I clicked on '1' or a '0' and Finished and noticed that the character got transmitted to the Arduino Serial Monitor.

Note : Setting the Serial Monitor to 38K did not work too well ! so had to scale back to 9600.


## Some snaps from the demo:

![screen shot 2018-07-01 at 7 08 43 pm](https://user-images.githubusercontent.com/14288989/42134975-3f4dcc00-7d62-11e8-9dc7-0b5a19fca3cc.png)

## Serial Monitor Output :

This prints whatever is sent from the bluetooth 

![screen shot 2018-07-01 at 7 06 33 pm](https://user-images.githubusercontent.com/14288989/42134976-3f7819d8-7d62-11e8-9efb-6f33049067d8.png)

## Bluetooth HC05 Pin diagram

![screen shot 2018-07-01 at 7 27 08 pm](https://user-images.githubusercontent.com/14288989/42135196-1361e4d4-7d65-11e8-8a32-e4598c4bbd2f.png)

## Module Front picture :

![img_20180701_190926 1](https://user-images.githubusercontent.com/14288989/42135198-1a5bf36a-7d65-11e8-8072-366ee77539f4.jpg)

## Module Back side view:

![img_20180701_192718](https://user-images.githubusercontent.com/14288989/42135222-6b8dd71c-7d65-11e8-91f6-4c7e33b5e602.jpg)

## Demo showing that the light is lit when the user presses '1'
![img_20180701_190904](https://user-images.githubusercontent.com/14288989/42135200-1abd4dae-7d65-11e8-8068-535dd7ea5853.jpg)






 
