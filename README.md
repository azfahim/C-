# C-
sample_1

int ledPin = 9;
int butPin = 5;
int tempPin = A0;

int switchState = 0;
int prevSwitchState = 0;

int ledState = 0;

void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(butPin, INPUT);
}

void loop()
{
  int senseVal = analogRead(tempPin);
  float voltage = (5.0 * senseVal) / 1023.0;
  float tempVal = (voltage - 0.5) * 100.0;

  switchState = digitalRead(butPin);

  if (switchState == HIGH && switchState != prevSwitchState) {
    ledState = !ledState;
    delay(200);
  }

  if (ledState == 1 && tempVal > 60) {
    digitalWrite(ledPin, HIGH);
    delay(1000);
    digitalWrite(ledPin, LOW);
    delay(1000);
  } else {
    digitalWrite(ledPin, LOW);
  }

  prevSwitchState = switchState;
}
