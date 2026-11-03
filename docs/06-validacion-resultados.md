# 6. Validación y resultados

La validación se realizó por etapas para comprobar que cada capa conservara el mismo estado del proceso.

## Pruebas funcionales del activo físico

| B1 | B2 | B3 | Resultado esperado | Estado |
|---:|---:|---:|---|---|
| 0 | 0 | 0 | H4 - Tanque vacío | ✅ Validado |
| 1 | 0 | 0 | H2 - Nivel bajo | ✅ Validado |
| 1 | 1 | 0 | H1 - Nivel correcto | ✅ Validado |
| 1 | 1 | 1 | H3 - Nivel alto | ✅ Validado |
| Combinación incoherente | | | H5 - Error | ✅ Validado |

START y STOP respondieron correctamente durante la prueba online. B1, B2 y B3 también fueron comprobados individualmente y en combinación.

## Validación Modbus

La aplicación de CODESYS fue descargada al runtime local y ejecutada en modo **RUN**. El dispositivo Modbus serial apareció **En ejecución**.

Durante la validación online se observó:

- `Request Counter`: **3844**
- `Error Counter`: **0**

También se comprobó que los cambios físicos se reflejaran en `EntradasByte`, `StartFisico`, `StopFisico`, `B1Fisico`, `B2Fisico` y `B3Fisico`.

Las salidas H1-H5 respondieron de acuerdo con la tabla funcional y la HMI mostró el mismo estado que el montaje.

```text
Montaje físico == Variables Modbus == HMI CODESYS
```

Resultado de la cadena principal:

```text
Activo físico -> Arduino UNO -> Modbus RTU -> CODESYS -> HMI
```

**Estado: ✅ Validado.**

## Escritura remota preparada

Se agregó el canal `Comando_Remoto` mediante `FC05 - Write Single Coil` sobre el coil 5 y se reservó D13 / `%QX0.5` en OpenPLC con alias `Remoto`.

En CODESYS se añadieron `ComandoRemoto` y `ComandoRemotoByte` y el canal quedó mapeado al byte correspondiente con compilación en 0 errores.

## Validación IoT

Se preparó en Ubidots:

- dispositivo `Tanque_Digital`,
- variables `b1`, `b2`, `b3`, `run`, `estado_tanque` y `comando_remoto`,
- dashboard `Gemelo Digital - Tanque`,
- indicador para B1/B2/B3/RUN,
- switch para `comando_remoto`.

También se preparó un gateway Python para intercambiar datos entre Modbus RTU y la API de Ubidots.

### Estado de la prueba IoT

| Prueba | Estado |
|---|---|
| Estructura Ubidots creada | ✅ |
| Variables creadas | ✅ |
| Dashboard creado | ✅ |
| Switch remoto configurado | ✅ |
| Gateway Python preparado | ✅ |
| Publicación real con Arduino conectado | ⏳ Pendiente de prueba final |
| Orden Ubidots → Arduino | ⏳ Pendiente de validación final |

Las dos últimas pruebas no se marcan como completadas porque todavía no fueron observadas físicamente con el Arduino conectado al gateway IoT.

## Resultado general

La integración física y el gemelo digital en CODESYS quedaron operativos y validados. La capa IoT quedó implementada a nivel de dispositivo, dashboard, variables, mando remoto y gateway, pendiente únicamente de la prueba final en hardware.
