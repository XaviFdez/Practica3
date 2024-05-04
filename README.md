# Práctica 3: WIFI Y BLUETOOTH

## Introducción de la práctica
La principal función de la práctica está destinada a trabajar con el wifi y el bluetooth.

Con la ayuda del microprocesador ESP32, utilizado en las prácticas anteriores, se llevará a cabo una práctica dónde se generará un web server desde la placa, también con la ayuda de una aplicación que se descargará en el móvil y con la ayuda del bluetooth, de este anterior, elaboraremos una comunicación serie.

## PRACTICA A- GENERACIÓN DE UNA PÁGINA WEB
```c++
#include <WiFi.h>
#include <WebServer.h>
#include <Arduino.h>

const char* ssid = "Xiaomi_11T_Pro"; 
const char* password = "12345678"; 
WebServer server(80);

void handle_root();

// Object of WebServer(HTTP port, 80 is defult)
void setup() {
Serial.begin(115200);
Serial.println("Try Connecting to ");
Serial.println(ssid);
// Connect to your wi-fi modem
WiFi.begin(ssid, password);
// Check wi-fi is connected to wi-fi network
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}
Serial.println("");
Serial.println("WiFi connected successfully");
Serial.print("Got IP: ");
Serial.println(WiFi.localIP()); //Show ESP32 IP on serial
server.on("/", handle_root);
server.begin();
Serial.println("HTTP server started");
delay(100);
}
void loop() {
server.handleClient();
}
```
HTML:
```
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1> Pagina Web creada , Practica 3 - Wifi &#128522;</h1>\
</body>\
</html>";

// Handle root url (/)
void handle_root() {
 server.send(200, "text/html", HTML);
}
```
### Funcionamiento y salida por terminal:

Principalmente el fucionamiento de este código és configurar la placa ESP32, para que esta actue como un servidor, así para que genere una página web, donde esa página web es una página HTML, dónde se accede a su IP, desde un navegador.
- En la función *setup()*, se inicializa la comunicación serial, se conecta a la red Wi-Fi y se inicia el servidor web.
- En la función *loop()*, se manejan las solicitudes de los clientes al servidor web.

El código incluye de las librerías WiFi.h y WebServer.h, para hacer lo dicho anteriormente.

La salida que se muestra por terminal del código:

```
Try Connecting to 
Xiaomi_11T_Pro
...........................
WiFi connected successfully
Got IP: 192.168.1.100
HTTP server started
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



