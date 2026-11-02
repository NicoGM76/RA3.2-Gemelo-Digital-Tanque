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

La prueba pendiente consiste en comprobar que al accionar B1, B2 y B3 en el montaje físico, CODESYS reciba los mismos valores mediante Modbus RTU.

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
- captura online de variables,
- captura del HMI,
- dashboard IoT,
- evidencia de control remoto.

Esta página se actualizará a medida que se complete cada prueba.
