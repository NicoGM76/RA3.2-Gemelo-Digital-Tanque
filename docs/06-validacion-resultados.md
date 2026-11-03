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

START se encuentra operativo y, durante la prueba online más reciente, **STOP también respondió correctamente**, por lo que ambos controles físicos quedan funcionales en el montaje actual.

## Validación Modbus

La aplicación de CODESYS fue descargada al runtime local y ejecutada en modo **RUN**. El dispositivo Modbus serial aparece **En ejecución** dentro de CODESYS.

Durante la validación online se observó el siguiente diagnóstico:

- `Request Counter`: **3844**
- `Error Counter`: **0**

Este resultado confirma que la capa Modbus está procesando solicitudes sin errores de comunicación en el diagnóstico observado.

También se realizó una prueba con una entrada física del montaje y CODESYS reflejó correctamente el cambio en las variables asociadas, validando el flujo:

```text
Activo físico -> Arduino UNO -> Modbus RTU -> CODESYS
```

Además, el control físico STOP respondió correctamente durante esta etapa.

La siguiente validación consiste en recorrer B1, B2 y B3 de forma individual y combinada para comprobar que `EntradasByte`, `B1Fisico`, `B2Fisico` y `B3Fisico` reproduzcan completamente el estado físico y que la HMI muestre el mismo estado del tanque.

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
- captura online de variables B1/B2/B3 cambiando,
- captura del HMI,
- dashboard IoT,
- evidencia de control remoto.

Esta página se actualizará a medida que se complete cada prueba.
