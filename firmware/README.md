# Firmware

Esta carpeta debe contener el código real que ya corre sobre el ESP32-S3 (el archivo que maneja los sensores VL53L0X y TCS34725, la máquina de estados completa — REPOSO, DETECCIÓN, POLINIZA, RECHAZO, DESCANSO, BATERIA — y la calibración de blanco persistente).

No lo incluí todavía porque ese código solo se compartió como texto pegado en el chat, no como archivo, y para no arriesgar un error de transcripción en algo que ya funciona en el hardware real, es mejor que lo copien y peguen ustedes mismos aquí (o me lo vuelvan a adjuntar como archivo `.ino` y yo lo agrego tal cual).

## Qué debería ir aquí

- `abejorro.ino` (o `main.cpp` + `platformio.ini` si usan PlatformIO) — el firmware que ya está probado.
- Dependencias (si usan PlatformIO):

```ini
lib_deps =
    pololu/VL53L0X
    adafruit/Adafruit TCS34725
    adafruit/Adafruit BusIO
```

## Nota sobre versiones anteriores

En el historial de este proyecto hubo una versión especulativa anterior (`kynzha_abejorro_v2.ino`) escrita antes de conocer el firmware real que el equipo ya tenía funcionando. **No es la versión correcta** — usa otro esquema de pines, no tiene el estado de batería, y no tiene la calibración/anti-falsos-positivos del firmware real. No la suban aquí.
