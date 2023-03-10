# Practica 1.1. Blink

## **Introducción**
En la primera práctica generaremos un programa que mediante un bucle infinito encienda y apague un led durante 500 milisegundos cada fase y escriba por el puerto serie un mensaje de ON y OFF.

## **Material**
- Un led
- Cables
- Processador ESP32
- Visual Code Studio


## **Funcionamiento**
En primer lugar iniciaremos el PlatformIO, su entorno de trabajo y el modelo de la placa. En nuestro caso el modelo de placa que utilizo es el espressif32-nodemcu-32s, y el framework será Arduino.

A continuación utilizaremos el código de ejemplo que nos proporciona el entorno Arduino, desde su aplicación y posterioirmente definiremos el led que conectaremos en la placa.
En nuestro caso el led 13.

Por último se compila el programa y se carga en la ESP32 mediante la extensión de PlatformIO.

## **Código completo**
```cpp
#include <Arduino.h>

/*
  Blink
  Turns on an LED on for one second, then off for one second, repeatedly.
 */
 
// Pin 13 has an LED connected on most Arduino boards.
// give it a name:
int led = 13;

// the setup routine runs once when you press reset:
void setup() {                
  // initialize the digital pin as an output.
  pinMode(led, OUTPUT);    
}

// the loop routine runs over and over again forever:
void loop() {
  digitalWrite(led, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(500);               // wait for a second
  digitalWrite(led, LOW);    // turn the LED off by making the voltage LOW
  delay(500);               // wait for a second
}
```
## **Diagrama de flujo**
```mermaid
graph LR
    A[LED ON] --> B[Msg LED ON]
    B[Msg LED ON] --> C[Wait 500 ms]
    C[wait 500 ms] --> D[LED OFF]
    D[LED OFF] --> E[Msg LED OFF]
    E[Msg LED OFF] --> F[Wait 500 ms]
    F[Wait 500 ms] --> A[LED ON]
```
## **Diagrama de tiempos**

```wavedrom
{ signal : [
  { name: "led",  wave: "10101010" },
  { name: "estado",  wave: "34343434",   data: "ON OFF ON OFF ON OFF ON OFF" },
]}
```


## **Ejercicio voluntario**

- Leer el valor del sensor de temperatura interno y sacarlo por el puerto serie.

## **Codigo Completo**

```cpp

#include <Arduino.h>

int led = 1;

#ifdef __cplusplus
extern "C" {
#endif
uint8_t temprature_sens_read();
#ifdef __cplusplus
}
#endif
uint8_t temprature_sens_read();

void setup() { 
  Serial.begin(115200);
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH);
  Serial.print("Led On  ");
  delay(500);
  digitalWrite(led, LOW);
  Serial.print("Led Off ");
  delay(500);

   Serial.print("Temperature: ");

   //pasa la temperatura de F a Cº.

   Serial.print((temprature_sens_read() - 32) / 1.8);
   Serial.println(" C");
   delay(5000);
}
```