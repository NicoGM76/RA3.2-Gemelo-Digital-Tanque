# 5. Integración IoT

La capa IoT se implementa utilizando el computador como gateway entre CODESYS y la plataforma en Internet.

## Flujo de trabajo

```text
Arduino UNO
   ↕ Modbus RTU
CODESYS
   ↕ Gateway local
PC
   ↕ Internet
Ubidots
```

## Estado del tanque a publicar

Se propone codificar el estado general del tanque de la siguiente forma:

| Valor | Estado |
|---:|---|
| 0 | Sistema detenido / sin estado |
| 1 | Tanque vacío |
| 2 | Nivel bajo |
| 3 | Nivel correcto |
| 4 | Nivel alto |
| 5 | Error de secuencia |

## Dispositivo IoT creado

Se creó en Ubidots el dispositivo **Tanque_Digital** con seis variables Raw:

- `b1`
- `b2`
- `b3`
- `run`
- `estado_tanque`
- `comando_remoto`

## Dashboard

Se creó el dashboard **Gemelo Digital - Tanque**.

Actualmente contiene:

- un widget **Indicator** asociado a `b1`, `b2`, `b3` y `run`,
- un widget **Switch** asociado a `comando_remoto`.

El dashboard ya está preparado para visualizar el estado del tanque y enviar una orden remota. En este punto aún no se han recibido datos reales desde CODESYS, por lo que los indicadores aparecen sin información disponible.

## Control remoto

La variable `comando_remoto` se utiliza como orden digital de la plataforma IoT:

- `0` = OFF
- `1` = ON

El objetivo de la siguiente prueba es enlazar esta variable con `ComandoRemoto` en CODESYS y verificar que el comando llegue finalmente al Arduino mediante Modbus RTU.

## Estado actual

- Dispositivo Ubidots creado: ✅
- Variables IoT creadas: ✅
- Dashboard creado: ✅
- Indicadores B1/B2/B3/RUN: ✅ configurados
- Switch `comando_remoto`: ✅ configurado
- Publicación de datos reales desde CODESYS: ⏳ pendiente
- Orden Ubidots → CODESYS → Arduino: ⏳ pendiente de validación
