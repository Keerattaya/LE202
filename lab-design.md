# ระบบรดน้ำต้นไม้อัตโนมัติ
หลักการทำงาน จะต้องเสียบที่วัดความชื้นลงไปในดิน หากพบว่าในดินมีความชื้นน้อยกว่าที่กำหนดไว้ ให้ระบบจำทำงานโดยทำการปล่อยน้ำเมื่อความชื้นได้ตามที่ต้องการ วงจรจะหยุดทำงาน 
## อุปกรณ์การทดลอง
    1.Arduine_ Node MCU
    2.Soil Moisture sensor(อุปกรณ์วัดควมชื้นดิน)
    3.Relay
    4.ปั้มน้ำ
    5.แหล่งจ่ายไฟ
    6.บอร์ดทดลอง(Bread bcard)
## วิธีทำการทดลอง
ต่อวงจรดังรูป
![image](https://user-images.githubusercontent.com/98943481/153996821-030340b7-68cd-418e-8ff2-5cf757027947.png)
### อัปโหลดโปรแกรมลง microcontroller เพื่อให้ระบบทำงาน
    const int analogInPin = A0; // กำหนดขา input เซ็นเซอร์
    const int Relay = 2; // กำหนดขา input รีเลย์
    int sensorValue = 0; // ตัวแปรค่า Analog
    int outputValue = 0; // ตัวแปรสำหรับ Map เพื่อคิด %
    void setup() {
    Serial.begin(9600);
    pinMode(Relay, OUTPUT); // กำหนด รีเลย์เป็น Output
    }
    void loop() {
    sensorValue = analogRead(analogInPin);
    outputValue = map(sensorValue, 0, 1023, 100, 0);
    Serial.print(outputValue);
    Serial.println(" %");
    if (outputValue <= 40) { //ตั้งค่า % ที่ต้องการจะรดน้ำต้นไม้
    digitalWrite(Relay, HIGH); // เมื่อความชื้นน้อยกว่า 40% ให้เปิดปั๊มน้ำ
    }
    else {
    digitalWrite(Relay, LOW); // เมื่อความชื้นมากกว่า 40% ปิดปั๊ม
    }
    delay(500);
    }
### แหล่งที่มา
    https://www.glurgeek.com/education/arduinoautowatering/
  

