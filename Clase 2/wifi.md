# Conexión a Internet

## Conexión Wifi
### Introducción

Es muy normal el poseer dispositivos que pueden conectarse a Internet, como lo es un teléfono móvil, una laptop, una televisión, etc. Hay muchos casos en los cuales, se necesita hacer el envío de información hacia alguna plataforma alojada en la Nube. Lo necesario para realizar esto es conectarse a Internet. 

En esta sección se realizará la conexión de la tarjeta ESP32 hacia una red WiFi aprovechando que nativamente el chip cuenta con conectividad WiFi. Esta última es compatible con 802.11 b/g/n en la banda de los 2.4GHz, alcanzando velocidades de hasta 150 Mbits/s. También incluye comunicación Bluetooth compatible con Bluetooth v4.2 y Bluetooth Low Energy (BLE) que serán mencionados a posterior.

### Configurar una conexión Wifi

Para conectar la tarjeta Esp32 a una red inalámbrica es necesario conocer como mínimo los siguientes datos:
- **SSID**: es el nombre público que identifica una red local inalámbrica, es decir, una WLAN. Son las siglas de Service Set Identifier.
- **PASSWORD**: Clave de seguridad de la red.

Estos datos pasan a ser constantes del sketch cuyos valores dependerán de la red a la que se conecta la placa. A continuación se muestra el código necesario:
>
>``` c++
>#include <WiFi.h>
>
>const char* SSID = "UNA_RED";
>const char* PASS = "UN_PASS";
>
>void setup() {
>    Serial.begin(115200);
>    Serial.println("");
>    WiFi.begin(SSID, PASS);
>    while (WiFi.status() != WL_CONNECTED) {
>        delay(500);
>        Serial.print(".");
>    }
>    Serial.println("");
>    Serial.println("WiFi conectado");
>    Serial.println(WiFi.localIP());
>    server.begin();  // iniciamos el servidor
>}
>```

El funcionamiento del código anterior se explica a continuación:

Como primer paso, se debe llamar a la librería WiFi.h, que se encuentra instalada en el IDE de Arduino por defecto (No es necesario instalar).

>``` c++
>#include <WiFi.h>
>```
Ahora, se definen como char constante el nombre y la contraseña de la red WiFi a la cual se realiza la conexión.

>```c++
>const char* SSID = "UNA_RED";
>const char* PASS = "UN_PASS";
>```

Se define en la función **setup()** el inicio del terminal Serial a una velocidad de baudios determinada, y se inicia la conexión WiFi con el comando **WiFi.begin()**, añadiendo los nombres de las variables mencionadas (SSID y PASS). Adicionalmente se añade un retardo de 2 segundos.

>```c++
>void setup() {
>  /*Iniciamos el terminal Serial para la escritura de >algunos parámetros */
>  Serial.begin(9600);
>  /*Iniciamos la conexión a la red WiFi definida*/
>  WiFi.begin(SSID, PASS);
>  delay(2000);
>```

Se añade un ciclo While que tiene como función imprimir puntos (“.”) mientras se realice la conexión con la red WiFi. Una vez conectado, dejarán de aparecer esos caracteres.

>```c++
>  Serial.print("Se está conectando a la red WiFi denominada ");
>  Serial.println(SSID);
>  while (WiFi.status() != WL_CONNECTED) {
>        delay(500);
>        Serial.print(".");
>    }
>```    
Cuando la conexión se haya realizado, se imprimirá en el monitor Serial “WiFi Connected”, junto a la dirección IP que se le asignó al ESP32. Cabe mencionar que no se contempla el uso de Loop () debido a que, la conexión se realiza una única vez, por lo que no es necesario realizar un bucle infinito de conexiones.

>``` c++    
>Serial.println("");
>Serial.println("WiFi connected");
>Serial.println("IP address: ");
>Serial.println(WiFi.localIP());
>```    

