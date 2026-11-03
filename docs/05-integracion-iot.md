# 5. Integración IoT

La capa IoT se implementa utilizando el computador como gateway entre el Arduino UNO y Ubidots. El activo virtual en CODESYS ya fue validado por separado mediante Modbus RTU sobre el mismo puerto serial.

## Arquitectura utilizada

```text
                 ┌────────────────────┐
                 │ CODESYS + HMI      │
                 │ Gemelo virtual     │
                 └─────────┬──────────┘
                           │ Modbus RTU
                           │
Arduino UNO / OpenPLC ─────┤ COM5
                           │
                           │ Modbus RTU
                 ┌─────────┴──────────┐
                 │ Gateway Python PC  │
                 └─────────┬──────────┘
                           │ HTTPS
                           ▼
                        Ubidots
```

El puerto COM5 es serial y solo puede ser tomado por un cliente a la vez. Por esta razón, la validación del gemelo CODESYS y la validación IoT se ejecutan en etapas separadas sobre el mismo activo físico. Esto evita agregar hardware adicional y permite reutilizar completamente el Arduino UNO disponible.

## Estado del tanque publicado

El gateway publica las variables `b1`, `b2`, `b3`, `run` y `estado_tanque`.

La variable `estado_tanque` se codifica así:

| Valor | Estado |
|---:|---|
| 0 | Sistema detenido / sin estado |
| 1 | Tanque vacío |
| 2 | Nivel bajo |
| 3 | Nivel correcto |
| 4 | Nivel alto |
| 5 | Error de secuencia |

## Dispositivo IoT

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

El dashboard queda preparado tanto para monitoreo como para control.

## Gateway PC ↔ Ubidots

Se preparó un script en Python que:

1. abre el puerto Modbus RTU del Arduino,
2. lee las entradas discretas B1, B2 y B3,
3. lee las salidas H1-H5 para determinar `run` y `estado_tanque`,
4. publica esos valores en Ubidots mediante HTTPS,
5. consulta el último valor de `comando_remoto`,
6. escribe ese valor en el coil 5 de Modbus mediante FC05.

En OpenPLC se reservó `%QX0.5` en el pin D13 con alias **Remoto** para recibir el comando externo.

## Control remoto

La variable `comando_remoto` trabaja como una orden digital:

- `0` = OFF
- `1` = ON

El objetivo de la validación final es utilizar ese coil remoto como una entrada de mando en la lógica OpenPLC, de forma que una orden desde Ubidots produzca una modificación observable en el estado del sistema físico.

## Estado actual

- Dispositivo Ubidots creado: ✅
- Variables IoT creadas: ✅
- Dashboard creado: ✅
- Indicadores B1/B2/B3/RUN: ✅ configurados
- Switch `comando_remoto`: ✅ configurado
- Gateway Python Modbus ↔ Ubidots: ✅ preparado
- D13 / `%QX0.5` reservado para mando remoto: ✅ configurado
- Publicación de datos reales en Ubidots: ⏳ pendiente de prueba con Arduino conectado
- Orden Ubidots → Arduino: ⏳ pendiente de validación final
