# 3. Activo virtual

El activo virtual corresponde a la HMI desarrollada en **CODESYS** durante RA2.3.

## Variables representadas

La interfaz virtual representa:

- marcha del sistema,
- START y STOP,
- sensores B1, B2 y B3,
- indicadores H1, H2, H3, H4 y H5.

La lógica base utilizada es:

```text
H1 = RUN AND B1 AND B2 AND NOT B3
H2 = RUN AND B1 AND NOT B2 AND NOT B3
H3 = RUN AND B1 AND B2 AND B3
H4 = RUN AND NOT B1 AND NOT B2 AND NOT B3
H5 = RUN AND ((B2 AND NOT B1) OR (B3 AND NOT B2))
```

Para RA3.2 la HMI no se reemplaza. Se reutiliza y se adapta para recibir las señales reales desde el Arduino por Modbus, de modo que el activo virtual refleje el comportamiento del montaje físico.

## Objetivo de sincronización

La validación esperada consiste en observar una misma condición en tres niveles:

1. montaje físico,
2. HMI de CODESYS,
3. plataforma IoT.

> Pendiente: incorporar captura final de la HMI y captura online durante una prueba física.
