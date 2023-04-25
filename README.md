# Alarma_Mochila
Alarma antirrobo que se activa cuando dispositivo BT se aleja.

Módulo principal formado por Raspberry Pi Zero. Se coloca en la mochila y detecta la señal de un dispositivo Bluetooth.

El módulo secundario está formado por un ESP32-WROOM. Funciona como beacon Bluetooth Low Energy (BLE). Transmite un mensaje cada 10 segundos.
