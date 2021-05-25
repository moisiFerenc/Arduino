# Arduino
This is a sort porject , nothing special

here is a little instruction:
https://youtu.be/I50MS7iE-MQ


here is my source code
```c++
#include <ESP8266WiFi.h>
const char WiFiPassword[] = "12345678";
const char AP_NameChar[] = "ferenc;;MOISI" ;
 
WiFiServer server(80);
 
String header = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n";
String html_1 = "<!DOCTYPE html><html><head><title>LED Control</title></head><body><div id='main'><h2>LED Control</h2>";
String html_2 = "<form id='F1' action='LEDON'><input class='button' type='submit' value='LED ON' ></form><br>";
String html_3 = "<form id='F2' action='LEDOFF'><input class='button' type='submit' value='LED OFF' ></form><br>";
String html_4 = "</div></body></html>";
 
String request = "";
int LED_Pin = D0;
 
void setup() 
{
    pinMode(LED_Pin, OUTPUT); 
 
    boolean conn = WiFi.softAP(AP_NameChar, WiFiPassword);
    server.begin();
 
} // void setup()
 
 
void loop() 
{
 
    
    WiFiClient client = server.available();
    if (!client)  {  return;  }
    request = client.readStringUntil('\r');
 
    if       ( request.indexOf("LEDON") > 0 )  { digitalWrite(LED_Pin, LOW);  }
    else if  ( request.indexOf("LEDOFF") > 0 ) { digitalWrite(LED_Pin, HIGH);   }
 
    client.flush();
 
    client.print( header );
    client.print( html_1 );
    client.print( html_2 );
    client.print( html_3 );
    client.print( html_4);
 
    delay(5);

 
}
```
