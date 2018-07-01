# Controlling-Lights-with-Bluetooth-HC05-and-Arduino-from-a-Smartphone

This program will turn the LED connected to an Arduino On or Off depending on what is being sent from the Smartphone.

The App installed from Google PlayStore was https://play.google.com/store/apps/details?id=com.giumig.apps.bluetoothserialmonitor&showAllReviews=true


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




Some snaps from the demo:

![screen shot 2018-07-01 at 7 08 43 pm](https://user-images.githubusercontent.com/14288989/42134975-3f4dcc00-7d62-11e8-9dc7-0b5a19fca3cc.png)

![screen shot 2018-07-01 at 7 06 33 pm](https://user-images.githubusercontent.com/14288989/42134976-3f7819d8-7d62-11e8-9efb-6f33049067d8.png)

![screen shot 2018-07-01 at 7 06 19 pm](https://user-images.githubusercontent.com/14288989/42134977-3fa21c60-7d62-11e8-9fb5-7b92d533088a.png)


 
