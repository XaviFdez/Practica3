# Práctica 3: WIFI Y BLUETOOTH

## Introducción de la práctica
La principal función de la práctica está destinada a trabajar con el wifi y el bluetooth.

Con la ayuda del microprocesador ESP32, utilizado en las prácticas anteriores, se llevará a cabo una práctica dónde se generará un web server desde la placa, también con la ayuda de una aplicación que se descargará en el móvil y con la ayuda del bluetooth, de este anterior, elaboraremos una comunicación serie.

## PRACTICA A- GENERACIÓN DE UNA PÁGINA WEB
```c++

HACER DE NUEVO
}
```
### Funcionamiento y salida por terminal:

Principalmente el fucionamiento de este código és configurar la placa ESP32, para que esta actue como un servidor, así para que genere una página web, donde esa página web es una página HTML, dónde se accede a su IP, desde un navegador.
EL código incluye de las librerías WiFi.h y WebServer.h, para hacer lo dicho anteriormente.

__....____

La salida por terminal del código es:
```
SALIDAS
````

## PRACTICA B- COMUNICACIÓN BLUETOOTH CON EL MOVIL

```c++
#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}
```
### Funcionamiento y salidas que se obtienen:

Este código trabajamos con bluetooth, donde se establece una comunicación entre la placa ESP32 y un dispositivo móvil a traves del bluetooth, donde se puede enviar i recibir datos.

Las salidas que se obtienen:
Las salidas que obtenemos a traves del puerto serie son los datos de que se envian y reciben en la comunicacón de los 2 dispositivos. 
Los datos pueden ser enviados de 2 formas:
. ESP32 al dispositivo
. Del dispositivo al ESP32



