#include "DHT.h"

#define DHTPIN 21       // DHT22 data pin connected to GPIO21
#define DHTTYPE DHT22   // DHT22 sensor type
#define RELAYPIN 23     // Relay IN pin connected to GPIO23

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(115200);
  dht.begin();
  pinMode(RELAYPIN, OUTPUT);
  Serial.println("IoT Automation Project Started!");
}

void loop() {
  // Read temperature and humidity
  float temp = dht.readTemperature();
  float hum = dht.readHumidity();

  // Print values to Serial Monitor
  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.print(" °C, Humidity: ");
  Serial.print(hum);
  Serial.println(" %");

  // Relay control logic
  if (temp > 30) {
    digitalWrite(RELAYPIN, HIGH); // Relay ON
    Serial.println("Fan ON (Relay Activated)");
  } else {
    digitalWrite(RELAYPIN, LOW);  // Relay OFF
    Serial.println("Fan OFF (Relay Deactivated)");
  }

  delay(2000); // Wait 2 seconds before next reading
}
