 This is IOT based Air Pollution Monitoring System which measures indoor harmful gases present in air like Carbon Dioxide(CO2) using an MQ135 gas sensor and Carbon Monoxide(CO) using an MQ7 sensor. It will show the air quality in PPM(Parts Per Million) on the LCD and as well as on Thingspeak so that we can monitor it very easily in PPM.

Components Requirement:
Arduino Uno
Wi-Fi module Node-MCU ESP8266
16x2 LCD
MQ135 Gas sensor
MQ 7 LPG gas sensor
Buzzer
LEDs
System Architecture:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/15678f3c-004f-4732-933d-5a445fd7faa8)


architecture

Software Requirement:
Arduino IDE
Arduino IDE used to upload programming in Arduino board and Node-MCU board with required library.

Thingspeak
ThingSpeak is an IoT analytics platform service that allows you to aggregate, visualize, and analyze live data streams in the cloud. You can send data to ThingSpeak from your devices, create instant visualization of live data, and send alerts.

Measurement:
The most important step is to calibrate the sensor in fresh air and then draw an equation that converts the sensor output voltage value into our convenient units PPM (parts per million). Here are the mathematical calculations derived:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/47665939-7778-4b80-a1fa-42181e89cf38)



For a log-log scale, the formula looks like this:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/57c94467-d63c-4c50-ac96-cd672386dca6)



Let’s find the slope. The formula to calculate slope m(here) is the following:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/34c8da27-4e7d-42fd-b28d-40e361a47108)



If we apply the logarithmic quotient rule we get the following:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/30a7fc5a-4f39-422b-9006-219fc48c1fa5)



Now we substitute the values for x, x0, y, and y0. Now that we have m and b, we can find the gas concentration for any ratio with the following formula:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/5bb8898f-b5d4-448a-984d-8559c460a289)



Using this we will be able to convert the sensor output values into PPM (Parts per Million)

However, in order to get the real value of the gas concentration according to the log-log plot we need to find the inverse log of x:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/6df59556-0b7b-4a0f-87b9-5d8c84ad5560)



Datasheets for:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/cfd17419-4ecc-4973-a33e-520ddfdf1eb9)


MQ135
MQ7
Results:
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/13bae5d7-3958-46e8-84d3-eeb8d098e258)
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/1d157616-e5bb-4fd6-a84a-76c893f0ea12)
![image](https://github.com/jayavanthsaggurthi/Air-poluution-System/assets/116862373/3d90f95a-5bc0-48a3-a1a6-d5f604d33ecf)

 



