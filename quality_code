#define BLYNK_TEMPLATE_ID "TMPL3Q_2zAj_i"
#define BLYNK_TEMPLATE_NAME "water quality check"
#define BLYNK_AUTH_TOKEN "YOUR_BLYNK_AUTH_TOKEN"

#define BLYNK_PRINT Serial

#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
#include <OneWire.h>
#include <DallasTemperature.h>

// ---------------- WiFi ----------------
char ssid[] = "YOUR_WIFI_NAME";
char pass[] = "YOUR_WIFI_PASSWORD";

// ---------------- Sensor Pins ----------------
#define TDS_PIN 33
#define PH_PIN 34
#define TURBIDITY_PIN 35
#define ONE_WIRE_BUS 4

// ---------------- Temperature Sensor ----------------
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature tempSensor(&oneWire);

BlynkTimer timer;

// ---------------- Functions ----------------
float readTemperature() {
  tempSensor.requestTemperatures();
  return tempSensor.getTempCByIndex(0);
}

float readTDS() {
  int raw = analogRead(TDS_PIN);
  float voltage = raw * (3.3 / 4095.0);
  float tdsValue = (133.42 * voltage * voltage * voltage
                  - 255.86 * voltage * voltage
                  + 857.39 * voltage) * 0.5;
  return tdsValue;
}

float readPH() {
  int raw = analogRead(PH_PIN);
  float voltage = raw * (3.3 / 4095.0);
  float phValue = 7 + ((2.5 - voltage) / 0.18);
  return phValue;
}

float readTurbidity() {
  int raw = analogRead(TURBIDITY_PIN);
  float voltage = raw * (3.3 / 4095.0);
  float turbidity = map(raw, 0, 4095, 3000, 0);
  return turbidity;
}

String waterStatus(float ph, float tds, float turbidity) {
  if ((ph >= 6.5 && ph <= 8.5) && (tds < 500) && (turbidity < 1000)) {
    return "SAFE";
  }
  return "UNSAFE";
}

void sendSensorData() {
  float temperature = readTemperature();
  float tds = readTDS();
  float ph = readPH();
  float turbidity = readTurbidity();

  String status = waterStatus(ph, tds, turbidity);

  Serial.println("==============================");
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  Serial.print("TDS Value: ");
  Serial.print(tds);
  Serial.println(" ppm");

  Serial.print("pH Value: ");
  Serial.println(ph);

  Serial.print("Turbidity: ");
  Serial.println(turbidity);

  Serial.print("Water Quality Status: ");
  Serial.println(status);
  Serial.println("==============================");

  Blynk.virtualWrite(V0, temperature);
  Blynk.virtualWrite(V1, tds);
  Blynk.virtualWrite(V2, ph);
  Blynk.virtualWrite(V3, turbidity);
  Blynk.virtualWrite(V4, status);
}

void setup() {
  Serial.begin(115200);

  analogReadResolution(12);
  analogSetAttenuation(ADC_11db);

  tempSensor.begin();

  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  timer.setInterval(10000L, sendSensorData); // every 10 sec
}

void loop() {
  Blynk.run();
  timer.run();
}
