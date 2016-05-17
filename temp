#define BLYNK_PRINT Serial    // Comment this out to disable prints and save space
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <SimpleTimer.h>
#include <DHT.h>
#define DHTPIN 2
#define DHTTYPE DHT22   
DHT dht(DHTPIN, DHTTYPE);
char auth[] = "SNIP";
const int ledPin = BUILTIN_LED;  // the onboard LED


//Simple Uptime Monitor on V5
SimpleTimer timer;
void sendUptime()
{
  // You can send any value at any time.
  // Please don't send more that 10 values per second.
  Blynk.virtualWrite(V5, millis() / 1000);
  // End of Uptime 
}


void setup()
{
  Serial.begin(9600);
  Blynk.begin(auth, "SNIP", "SNIP");
  pinMode(ledPin, OUTPUT);  // initialize onboard LED as output

  // Setup a function to be called every second
  timer.setInterval(1000L, sendUptime);

// TEMP TEST
  dht.begin();
  float h = dht.readHumidity();
  float t = dht.readTemperature();
  Blynk.virtualWrite(1, t); // virtual pin temperature app Value
  Blynk.virtualWrite(2, h); // virtual pin humidity app Value 
  Serial.print(t);
  Serial.print(h);  
}


BLYNK_WRITE(V10)
{
  Serial.print("Got a value: ");
  Serial.println(param.asStr());
  int brightness = param.asInt();
  analogWrite(ledPin, brightness);
}
  
void loop() 
{
    Blynk.run();
    timer.run();

}
