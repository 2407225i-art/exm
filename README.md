

## 1. Задание №1: ESP8266/ESP32 – точка доступа и управление светодиодом

### Цель
Запрограммировать ESP в режиме AP (имя `SmartHome_Gateway`, пароль `12345678`), реализовать веб-сервер с кнопками включения/выключения встроенного светодиода.

### Код (основная логика)

#include <SoftwareSerial.h>

SoftwareSerial espSerial(2, 3);  // RX=2, TX=3

void setup() 
{
  Serial.begin(115200);
  espSerial.begin(9600);
  
  Serial.println("=== СБРОС ESP8266 ===");
  delay(2000);
  
  // 1. Сброс
  Serial.println("1. Перезагрузка...");
  espSerial.println("AT+RST");
  delay(3000);
  
  // 2. Сброс к заводским настройкам
  Serial.println("2. Сброс настроек (Factory Reset)...");
  espSerial.println("AT+RESTORE");
  delay(3000);
  
  // 3. Проверка
  Serial.println("3. Проверка версии...");
  espSerial.println("AT+GMR");
  delay(1000);
  
  // 4. Режим точки доступа
  Serial.println("4. Настройка точки доступа SmartHome_Gateway...");
  espSerial.println("AT+CWMODE=3");
  delay(1000);
  
  // 5. Создание новой сети
  String cmd = "AT+CWSAP=\"SmartHome_Gateway\",\"12345678\",1,3";
  espSerial.println(cmd);
  delay(2000);
  
  // 6. Проверка
  espSerial.println("AT+CIFSR");
  delay(1000);
  
  Serial.println("\n=== ГОТОВО ===");
  Serial.println("Сеть: SmartHome_Gateway");
  Serial.println("Пароль: 12345678");
  Serial.println("\nВыключайте питание ESP8266 на 10 секунд");
  Serial.println("и включайте заново!");
}

void loop() 
{
  // Вывод ответов ESP8266
  while(espSerial.available()) {
    Serial.write(espSerial.read());
  }
  
  // Ручной ввод команд
  while(Serial.available()) {
    espSerial.write(Serial.read());
  }
}
<img width="661" height="773" alt="image" src="https://github.com/user-attachments/assets/581c5d7e-49a1-40de-aa27-4837b03cb08d" />

Задание №2

<img width="1920" height="919" alt="image" src="https://github.com/user-attachments/assets/3348e8aa-4464-4bbc-8fd1-26349c60f609" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/09a6c3d0-ef1f-4929-b1cc-60a2dc50e8d1" />


