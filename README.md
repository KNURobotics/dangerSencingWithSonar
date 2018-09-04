# 초음파센서

#### 아두이노 초음파 센서 HY-SRF05

### 



``` C

int trigPin = 13;
int echoPin = 12;
int led = 51 ;
int buzzer = 52;
int danger = 0;

void setup()
{
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(led, OUTPUT);
  pinMode(buzzer, OUTPUT);
}

void loop()
{
  digitalWrite(led, LOW);
  digitalWrite(buzzer, LOW);

  //길이계산
  long duration, distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 17 /1000 ;
  Serial.println(distance);
  delay(1000);

  //위험상황
  if(distance>16)
  {
    danger ++ ;
    Serial.println(distance);
    Serial.println(danger);
    if(danger >= 3)
    {
      for(int i =0 ; i< 5 ; i++)
      {
      digitalWrite(led, HIGH);
      digitalWrite(buzzer, HIGH);
      delay(50);
      digitalWrite(led,LOW);
      digitalWrite(buzzer, LOW);
      delay(50);
      Serial.println(distance);
      Serial.println(danger);
      }
      int danger = 0;
    }
    else
    {
      Serial.println(distance);
    }

  }

}

```




[DIY 메카솔루션 오픈랩](https://blog.naver.com/roboholic84/220912417440)
