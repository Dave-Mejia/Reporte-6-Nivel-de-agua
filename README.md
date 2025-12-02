# Reporte 6 Nivel de agua

Se programará un ESP32 de modo que mediante un sensor ultrasónico HC-SR04 se detecte el nivel de agua y en función de cada nivel prenda un led de distinto color, a su vez el valor del nivel se mostrará en una pantalla LCD 16x2(I2C)
## Introducción
### Descripción
Utilizaremos l plataforma WOKWI para simular la adquisición de datos de distancia mediante un sensor ultrasónico HC-SR04 y la programación del mismo en un microcontrolador ESP32, los datos se mostrarán en una pantalla LCD

### Material Necesario
Para realizar esta practica necesitas lo siguiente

a. Plataforma WOKWI

b. Tarjeta ESP 32

c. Sensor ultrasónico HC-SR04

d. Pantalla LCD 16x2(I2C)

## Instrucciones
### Previo
1. Abrir la plataforma WOKWI.

### Preparación
2. Ir a la pestaña de sketch.ino y borrar el codigo e programación predeterminado
3. Abrir la terminal de programación y colocar la siguente programación:

```
#include <LiquidCrystal_I2C.h>
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 17;
const int led2 = 5;
const int led3 = 19;
const int led4 = 18;
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   16
// defines variables
long duration;
int distance;
int safetyDistance;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
  lcd.init();
  lcd.backlight();
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=1 && safetyDistance<=99)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.clear();
  lcd.print("Porcentaje: 100%");
  delay(2000);
}
else if(safetyDistance>=100 && safetyDistance<=199) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 75%");
  delay(2000);
}
else if(safetyDistance>=200 && safetyDistance<=299) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 50%");
  delay(2000);
}
else if(safetyDistance>=300 && safetyDistance<=399) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, HIGH);
   lcd.clear();
  lcd.print("Porcentaje: 25%");
  delay(2000);
}
else if(safetyDistance>=400 && safetyDistance<=499) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.clear();
  lcd.print("Porcentaje: 0%");
  delay(2000);
}
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.clear();
  lcd.print("Eror");
  delay(2000);
}

// Prints the distance on the Serial Monitor
Serial.print("Distancia: ");
Serial.println(distance);
lcd.clear();
lcd.setCursor(2, 0);
lcd.print("Distancia: " + String(distance));
delay (2000);

  delay(2000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("al curso");
  delay(2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("David Mejia");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanico");
  delay(2000);
   lcd.clear();
  lcd.setCursor(1, 0);
  lcd.print("Fecha:  ");
  lcd.setCursor(5, 1);
  lcd.print("29/11/25");
  delay(2000);
}

```

4. Ir a la pestaña "Library manager" haer clic sobre el icon "+", buscar la libreria "HCSR04 ultrasonic sensor" y agregarla
![](https://github.com/Dave-Mejia/Reporte-4-ESP32-con-sensor-ultrasonico/blob/main/libreria%20sensor%20ultrasonico.png?raw=true)

5. De igual manera agregar la librería "LiquidCrystal I2C" para la pantalla LCD
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/Libreria%20Pantalla%20LCD%20Liquid%20cristal.png?raw=true)
  
7. Ir al esquema de simulación, dar clic al icono "+ (add new part)"

![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/Add%20new%20part.png?raw=true)

8. Buscar el sensor  y agregar
   
![](

9. Repetir el paso anterior buscar el sensor HCSR04 y agregar 
10. De igual forma buscar la pantalla LCD 16x2(I2C) y agregar
   
11. Conectar circuito como indica la figura de abajo
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/Conexion%20Tarjeta%20ESP32,%20Sensor%20DHT22,%20sensor%20HC-SR-04%20y%20pantalla%20LCD.png?raw=true)

### Operación
12. Iniciar simulador dando clic en el icono "start simulation"

![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/play.png?raw=true)


13. Visualizar los datos en el monitor serial.

## Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/resultado%20sensor%20ultrasonico%20y%20temperatura%201.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/resultado%20sensor%20ultrasonico%20y%20temperatura%202.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/resultado%20sensor%20ultrasonico%20y%20temperatura%203.png?raw=true)
![](https://github.com/Dave-Mejia/Reporte-5-Sensor-ultrasonico-y-de-temperatura/blob/main/resultado%20sensor%20ultrasonico%20y%20temperatura%204.png?raw=true)

## Créditos
Ralizado por el Ingeniero David Mejía
