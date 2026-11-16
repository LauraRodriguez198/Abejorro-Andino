<div align="center">

# 🐝 Abejorro Andino
### Semillero Kynzha · Colombia Biodiversa

*Un modelo animatrónico que hace visible lo invisible: la polinización por vibración.*

![Status](https://img.shields.io/badge/estado-prototipo%20funcional-success)
![Platform](https://img.shields.io/badge/plataforma-ESP32--S3-blue)
![Sensors](https://img.shields.io/badge/sensores-VL53L0X%20%2B%20TCS34725-orange)
![License](https://img.shields.io/badge/licencia-académica-lightgrey)

</div>

---

## 📑 Tabla de contenidos

- [¿Qué es esto?](#-qué-es-esto)
- [Arquitectura](#-arquitectura)
- [Cómo decide el abejorro](#-cómo-decide-el-abejorro)
- [Calibración en campo](#-calibración-en-campo)
- [Costos](#-costos)
- [Equipo](#-equipo)
- [Presentación (PITCH)](#-presentación-pitch)

## 🌼 ¿Qué es esto?

Cada vez que comes algo que viene de una flor, hay una probabilidad real de que exista gracias a un sonido que nunca has escuchado: el zumbido de polinización de un abejorro vibrando contra una flor. Ocurre en milisegundos — a simple vista, es invisible.

Este proyecto lo hace visible. Construimos un modelo animatrónico interactivo del **abejorro andino** (*Bombus atratus*) que reconoce una flor por su color, se acerca con un sensor de distancia, y solo entonces reproduce la vibración torácica real que libera el polen — con retroalimentación visual inmediata en LED.

Es uno de los **7 animatrónicos polinizadores** de la iniciativa **Colombia Biodiversa** del Semillero Kynzha, pensado para divulgación científica itinerante: ferias, colegios y eventos de la Universidad Central.

## 🧠 Arquitectura

| Componente | Función |
| --- | --- |
| 🔭 `VL53L0X` | Sensor de distancia — detecta el acercamiento a la flor |
| 🎨 `TCS34725` | Sensor de color — clasifica el pétalo presentado |
| 🖥️ `ESP32-S3` | Microcontrolador — corre la máquina de estados |
| ⚙️ Motor N20 + leva | Vibración torácica realista |
| 📳 Motor de moneda | Vibración/sonido perceptible al tacto |
| 💡 LED RGB ("ojos") | Retroalimentación visual del estado |

```
REPOSO → DETECCIÓN → POLINIZA / RECHAZO → DESCANSO
                 ↳ BATERIA (seguridad por bajo voltaje)
```

## ⚙️ Cómo decide el abejorro

Los dos sensores comparten por defecto la misma dirección I2C, así que al encender el equipo se inicializa primero el sensor de color y luego se reasigna la dirección del sensor de distancia por software, para que ambos puedan funcionar al tiempo.

Estos son los parámetros que definen su comportamiento:

| Parámetro | Valor | Qué significa |
| --- | --- | --- |
| Distancia de detección | 120 mm | A partir de aquí el abejorro "nota" que algo se acerca |
| Distancia de lectura de color | 50 mm | A esta distancia decide qué color es el pétalo |
| Duración de la vibración (polinización) | 6 s | Cuánto dura la vibración torácica cuando el color es correcto |
| Tiempo de descanso | 4 s | Pausa antes de volver a estar disponible |
| Voltaje mínimo de batería | 6,4 V | Por debajo de esto, se corta la vibración por seguridad |

El color se clasifica en una de cinco categorías (amarillo, azul, morado, rechazo o sin color), y antes de cambiar de estado el firmware exige **dos lecturas iguales seguidas**, para no confundirse por ruido o por un reflejo pasajero.

## 🔧 Calibración en campo

El firmware tiene un modo de diagnóstico por el monitor serial (115200 baudios), pensado para ajustar un solo parámetro a la vez sin reprogramar:

| Comando | Acción |
| --- | --- |
| `v` | Vista verbose — muestra % de R, G, B y la letra de clasificación en cada lectura |
| `f` | Remedir la luz ambiental de fondo |
| `w` | Rehacer el balance de blanco (se guarda en memoria NVS, sobrevive a reinicios) |

**Protocolo:** cambiar un solo número a la vez, subirlo, y probar antes del siguiente ajuste. Presentar la flor por un pétalo, no por el centro.

## 💰 Costos

| Concepto | Valor |
| --- | --- |
| Costo total del prototipo | ≈ $1.678.000 COP |

Dividido entre los 5 integrantes: ≈ $335.600 COP c/u.

## 👥 Equipo

| Integrante | Área | Rol |
| --- | --- | --- |
| Laura Rodríguez | Electrónica | Firmware, lógica de sensores, diseño de PCB |
| Yuli Alape | Electrónica | Sensores de color y distancia, calibración |
| Juan Soler | Electrónica | Integración del sistema y experiencia de usuario |
| Santiago Roa | Mecánica | Estructura, cuerpo y mecanismo de vibración |
| Andrés Sánchez | Mecánica | Materiales, impresión 3D y ensamble |

## 🎤 Presentación (PITCH)

La presentación completa, con la estructura socializada en clase, está disponible aquí:
**[Ver el PITCH →](https://claude.ai/artifact/AmDZasfmefJbPmwrj7UasP)**

---

<div align="center">

*Cada vez que este abejorro vibra, recuerda que algo real, en algún lugar, está vibrando igual.*

</div>
