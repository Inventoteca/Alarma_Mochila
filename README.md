# Alarma_Mochila
Alarma antirrobo que se activa cuando dispositivo BT se aleja.

Módulo principal formado por una Raspberry Pi Zero W. Se coloca en la mochila y detecta la señal de un dispositivo Bluetooth.
Hojas de datos de la Raspberry Pi Zero W  
https://datasheets.raspberrypi.com/rpizero2/raspberry-pi-zero-2-w-product-brief.pdf  
https://cdn.sparkfun.com/assets/learn_tutorials/6/7/6/PiZero_1.pdf  
https://pinout.xyz  
El módulo principal se alimenta con 2 baterías 18650 en serie, el voltaje de alimentación es 8V, el consumo de corriente va de 200 mA a 300 mA.  
Se instaló una sirena que se emplea comúnmente en automóbiles. Su voltaje de alimentación va de 6 V a 14 V. Su consumo de corriente es 50 mA.

El módulo secundario está formado por un ESP32-WROOM. Funciona como beacon Bluetooth Low Energy (BLE). Transmite un mensaje cada 10 segundos.
¿Qué es un beacon o baliza Bluetooth? https://es.wikipedia.org/wiki/Baliza_electr%C3%B3nica  
Hoja de datos del ESP32 WROOM https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf  

La Raspberry ejecuta Node-RED (https://nodered.org)  
En Node-RED se instalaron los siguientes nodos para poder detectar el módulo BLE

Beacon Scanner  
https://flows.nodered.org/node/node-red-contrib-beacon-scanner  
Es el nodo con actualizaciones más recientes. Solo detecta beacons que se identifican como Estimote, EddyStone o iBeacon. Si hay otros beacons disponibles los ignora.  

BLE Beacon Scanner
https://flows.nodered.org/node/node-red-contrib-blebeacon-scanner
Está basado en código fuente del nodo anterior. Funciona de manera similar, pero detecta beacons de otros tipos.  

Ambos nodos dependenden de otros programas que se deben instalar

```
sudo apt-get install bluetooth bluez libbluetooth-dev libudev-dev
sudo setcap cap_net_raw+eip $(eval readlink -f `which node`)

sudo apt-get install libbluetooth-dev libudev-dev pi-bluetooth
npm install @abandonware/noble
```

Hay otros nodos para beacons que no se probaron. Por ejemplo eddystone-url https://flows.nodered.org/node/node-red-contrib-eddystone

## GPS
Se usa un módulo GPS para obtener la ubicación de la mochila.  
Primero se utilizó este módulo https://docs.onion.io/omega2-docs/using-gps-expansion.html  
Después se cambió a este módulo https://content.u-blox.com/sites/default/files/products/documents/NEO-6_DataSheet_%28GPS.G6-HW-09005%29.pdf  
https://www.electronicwings.com/raspberry-pi/gps-module-interfacing-with-raspberry-pi  
https://lastminuteengineers.com/neo6m-gps-arduino-tutorial/  
Aquí se pueden decodificar mensajes de GPS en formato NMEA https://rl.se/gprmc  
Se siguió este tutorial para configurar los nodos de mapa  https://www.industrialshields.com/es_ES/blog/raspberry-pi-para-la-industria-26/post/tutorial-de-node-red-como-obtener-las-coordenadas-gps-con-un-widget-de-mapas-304  
El flujo quedó un poco diferente al tutorial  
Se instalaron estos nodos:  
El primero convierte mensajes NMEA en objetos de javascript https://flows.nodered.org/node/node-red-contrib-nmea  
El segundo provee un mapa en el que se pueden dibujar marcadores https://flows.nodered.org/node/node-red-contrib-web-worldmap  

## Diseño 3D
El modelo del porta pilas se descargó de aquí https://www.thingiverse.com/thing:5237855  
La carcasa del beacon se diseñó con SolidWorks  
