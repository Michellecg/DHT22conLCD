# Practica ESP32 con DHT22 y LCD
En este repositorio se muestra una práctica utilizando la página Wokwi para la simulación del sensor DHT22 con LCD de 16x2.

## Introducción

### Descripción

Se recrea una simulación de un sensor de temperatura (DHT22) utilizando una tarjeta ```ESP32```, donde los datos se muestran en una LCD. En esta práctica se usara un simulador llamado [WOKWI](https://wokwi.com/).


## Material Necesario

Para realizar esta práctica se ocuparon las siguientes herramientas y componentes:

- [SIMULADOR WOKWI](https://wokwi.com/)
- Tarjeta ESP32
- Sensor DHT22
- LCD 16x2 (I2C)




## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Al ingresar a la página de [WOKWI](https://wokwi.com/) se selecciona la tarjeta ESP32, se agrega el sensor DHT22 y una LCD de 16x2 (I2C).

2. Una vez seleccionado la tarjeta ```Esp32```, en la parte izquierda se encuentra la pestaña de código donde se agrega lo siguiente:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0,0);
  lcd.print("Diplomado AIyM");
  lcd.setCursor(0,1);
  lcd.print("Michelle C. G.");
  delay(1500);

  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");
  delay(3000);

}

```
3. Instalar la libreria de **DHT sensor library for ESPx** y **LiquidCrystal I2C** como se muestra en la siguente imagen.

![](https://github.com/Michellecg/DHT22conLCD/blob/main/Lib_LCD.PNG)

4. Hacer la conexión de **DHT22** y **LCD 16x2 (I2C)** con la **ESP32** como se muestra en la siguente imagen.

![](https://github.com/Michellecg/DHT22conLCD/blob/main/Conex_LCD.PNG)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Modificar la temperatura y humedad dando *doble click* al sensor **DHT22**
4. Añadir un mensaje al inicio de recolección de datos en la LCD. 

## Resultados

Una vez compilado el programa y que no se hayan presentado errores, se podrán observar los datos del sensor en la LCD tal como se muestra en la siguente imagen.

![](https://github.com/Michellecg/DHT22conLCD/blob/main/Func_LCD1.PNG)

![](https://github.com/Michellecg/DHT22conLCD/blob/main/Func_LCD2.PNG)

![](https://github.com/Michellecg/DHT22conLCD/blob/main/Result_LCD.PNG)


# Créditos

Desarrollado por Michelle Cuatlapantzi González

- [GitHub](https://github.com/Michellecg/)