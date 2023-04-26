# Alarma_Mochila
Alarma antirrobo que se activa cuando dispositivo BT se aleja.

Módulo principal formado por Raspberry Pi Zero. Se coloca en la mochila y detecta la señal de un dispositivo Bluetooth.

El módulo secundario está formado por un ESP32-WROOM. Funciona como beacon Bluetooth Low Energy (BLE). Transmite un mensaje cada 10 segundos.

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

Para hacer una interfaz gráfica se instaló node-red-dashboard https://flows.nodered.org/node/node-red-dashboard  
