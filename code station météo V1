// pour ce code il faut obligatoirement les librairies suivantes:
// - DHT Sensor Librairie: https://github.com/adafruit/DHT-sensor-library
// - Adafruit Unified Sensor Librairie:https://github.com/adafruit/Adafruit_Sensor
// -Adafruit_sensor dans manage librairies

#include "DHT.h"
#include <Adafruit_Sensor.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

#define DHTPIN 2     // le capteur DHT est branché sur le pin 2

//choisis ton type de capteur!
#define DHTTYPE DHT11   // DHT 11
//#define DHTTYPE DHT22   // DHT 22  (AM2302), AM2321
//#define DHTTYPE DHT21   // DHT 21 (AM2301)
LiquidCrystal_I2C lcd(0x27,16,2);

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  
  Serial.begin(9600);
  Serial.println(F("DHTxx test!"));

  dht.begin();
  lcd.backlight();
  lcd.begin();
}

void loop() {
  
  // attendre 2 seconde avant le mesurement
  delay(2000);

  // regarder l'humiditée et la température
  float h = dht.readHumidity();
  // regarde temperature en Celsius 
  float t = dht.readTemperature();
  // regarde la  temperature en Fahrenheit 
  float f = dht.readTemperature(true);

  // verifier si le capteur marche.
  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println(F("Failed to read from DHT sensor!"));
    return;
  }

  float hic = dht.computeHeatIndex(t, h, false);

  //ecriture de la température et l'humidité sur le port série 
  Serial.print(F("Humidity: "));
  Serial.print(h);
  Serial.print(F("%  Temperature: "));
  Serial.print(t);
  Serial.println(F("°C "));

  //ecriture de la température sur le lcd 
  lcd.setCursor(0,0);
  lcd.print("temperature:");
  lcd.setCursor(12,0);
  lcd.print(t);

  //ecriture de l'humiditée sur le lcd 
  lcd.setCursor(0,1);
  lcd.print("humidite:");
  lcd.setCursor(9,1);
  lcd.print(h);
  lcd.setCursor(15,1);
  lcd.print("%");
}
