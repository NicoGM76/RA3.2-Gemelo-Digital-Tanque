# 5. Integración IoT

La capa IoT se implementará utilizando el computador como gateway entre CODESYS y la plataforma en Internet.

## Flujo previsto

```text
Arduino UNO
   ↕ Modbus RTU
CODESYS
   ↕ Gateway local
PC
   ↕ Internet
Ubidots / ThingSpeak
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

## Control remoto

Para demostrar comunicación bidireccional se habilitará al menos una acción de control desde la plataforma IoT. La primera opción de implementación es una orden de **START remoto**.

El objetivo de esta etapa es demostrar que el gemelo no solo visualiza información del activo físico, sino que también puede recibir una orden desde la capa IoT.

## Plataforma

La primera opción de trabajo es **Ubidots STEM**. ThingSpeak se mantiene como alternativa si resulta más estable para la entrega.

> Estado actual: pendiente de integración después de validar Arduino ↔ CODESYS por Modbus.
