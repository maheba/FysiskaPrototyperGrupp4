# FysiskaPrototyperGrupp4
Fullständig kod för VibraSeat


/* Grupp 3 - Prototyp: Vibrationssätet
    Ett säte som vibrerar när användaren har suttit på sätet i en bestämd period.
*/



// Analog input pin that the Velostat is connected to
const int analogInPin = A0;

// value read from the Velostat

int sensorValue = 0;

unsigned long timer = 0;

unsigned long setTime = 3000;

boolean sitTooLong = false;

int vibrator1 = 2;
int vibrator2 = 4;

void setup() {
  Serial.begin(9600);
  pinMode(vibrator1, OUTPUT);
  pinMode(vibrator2, OUTPUT);

}

void loop() {
  // read the analog in value:
  unsigned long currentTime = millis();
  sensorValue = analogRead(analogInPin);

  for (sensorValue; sensorValue < 460;) {
    timer = currentTime + setTime;
    break;
  }

  if (currentTime > timer) {
    sitTooLong = true;
  } else {
    sitTooLong = false;
  }

  if (sitTooLong == true) {
    digitalWrite(vibrator1, HIGH);
    digitalWrite(vibrator2, HIGH);
  } else {
    digitalWrite(vibrator1, LOW);
    digitalWrite(vibrator2, LOW);
  }

  // print the results to the serial monitor:
  Serial.print("sensor = " );
  Serial.print(sensorValue);
  Serial.print("\t sitTooLong = ");
  Serial.print(sitTooLong);
  Serial.print("\t timer = ");
  Serial.println(timer);
}

