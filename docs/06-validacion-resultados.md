# 6. Validación y resultados

La validación se realiza por etapas para comprobar que cada capa conserve el mismo estado del proceso.

## Pruebas funcionales del activo físico

| B1 | B2 | B3 | Resultado esperado | Estado |
|---:|---:|---:|---|---|
| 0 | 0 | 0 | H4 - Tanque vacío | ✅ Validado |
| 1 | 0 | 0 | H2 - Nivel bajo | ✅ Validado |
| 1 | 1 | 0 | H1 - Nivel correcto | ✅ Validado |
| 1 | 1 | 1 | H3 - Nivel alto | ✅ Validado |
| Combinación incoherente | | | H5 - Error | ✅ Validado |

START se encuentra operativo. STOP continúa pendiente de ajuste físico.

## Validación Modbus

La aplicación de CODESYS fue descargada al runtime local y ejecutada en modo **RUN**. El dispositivo Modbus serial aparece **En ejecución** dentro de CODESYS.

Durante la validación online se observó el siguiente diagnóstico:

- `Request Counter`: **3844**
- `Error Counter`: **0**

Este resultado confirma que la capa Modbus está procesando solicitudes sin errores de comunicación en el diagnóstico observado.

La prueba funcional siguiente consiste en accionar B1, B2 y B3 en el montaje físico y comprobar que CODESYS reciba los mismos valores en `EntradasByte`, `B1Fisico`, `B2Fisico`, `B3Fisico` y finalmente en la HMI.

Criterio de éxito:

```text
Montaje físico == Variables Modbus == HMI CODESYS
```

## Validación IoT

La etapa final deberá comprobar:

1. publicación del estado actual del tanque,
2. actualización del dashboard al cambiar los sensores,
3. envío de una orden remota,
4. recepción de dicha orden en el sistema.

## Evidencias pendientes

- fotografía final del montaje,
- captura del proyecto `Tanque_V2_Modbus`,
- captura de configuración Modbus en CODESYS,
- captura online de variables cambiando,
- captura del HMI,
- dashboard IoT,
- evidencia de control remoto.

Esta página se actualizará a medida que se complete cada prueba.
