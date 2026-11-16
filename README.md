# Abejorro Andino — Semillero Kynzha

Modelo animatrónico interactivo del abejorro andino (*Bombus atratus*), que demuestra la **polinización por vibración torácica** (buzz pollination) para la divulgación científica de la iniciativa **Colombia Biodiversa** (Semillero Kynzha, Universidad Central).

## Equipo

| Integrante | Área | Rol |
| --- | --- | --- |
| Laura Rodríguez | Electrónica | Firmware, lógica de sensores, diseño de PCB |
| Yuli Alape | Electrónica | Sensores de color y distancia, calibración |
| Juan Soler | Electrónica | Integración del sistema y experiencia de usuario |
| Santiago Roa | Mecánica | Estructura, cuerpo y mecanismo de vibración |
| Andrés Sánchez | Mecánica | Materiales, impresión 3D y ensamble |

## Cómo funciona

El sistema corre sobre un **ESP32-S3** y combina:

- **VL53L0X** — sensor de distancia, detecta el acercamiento a la flor.
- **TCS34725** — sensor de color, clasifica el pétalo presentado.
- Máquina de estados: `REPOSO → DETECCIÓN → POLINIZA / RECHAZO → DESCANSO`, más un estado `BATERIA` de seguridad por bajo voltaje.
- Motor N20 + leva para la vibración torácica realista, y un motor de moneda para la vibración/sonido perceptible al tacto.
- LED RGB ("ojos") como retroalimentación visual del estado.
- Calibración de blanco persistente (NVS), compensación de luz ambiental y doble verificación (debounce) para evitar falsos positivos.
- Modo de diagnóstico por monitor serial (comandos `v`, `f`, `w`) para calibrar en campo sin reprogramar.

## Estructura del repositorio

```
firmware/     Código del ESP32-S3 (ver nota abajo)
docs/         Documentación del proyecto (Entrega 1, cronograma, etc.)
```

## Firmware

> **Pendiente:** este repositorio todavía no incluye el archivo real `abejorro.ino` que ya corre sobre el hardware (el que maneja VL53L0X + TCS34725, la máquina de estados completa y la calibración). Agréguenlo dentro de `firmware/` antes de la entrega — ver `firmware/README.md`.

## Costos

Cotización final con Ayuda en Ingeniería (servicio mecánico + electrónico): **$1.400.000 COP**, más materiales estimados de compra directa: **≈$278.000 COP**. Total: **≈$1.678.000 COP**, dividido entre los 5 integrantes.

## Presentación (PITCH)

La presentación del PITCH de este proyecto, con la estructura socializada en clase, está disponible como artefacto de Claude en:
`https://claude.ai/artifact/AmDZasfmefJbPmwrj7UasP`

## Contexto

Proyecto desarrollado para el Semillero Kynzha, dentro de la iniciativa Colombia Biodiversa de la Universidad Central.
