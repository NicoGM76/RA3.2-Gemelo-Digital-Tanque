# 2. Activo físico

El activo físico corresponde al montaje construido en RA2.3 y reutilizado para RA3.2.

## Entradas

| Señal | Pin Arduino | Dirección IEC | Función |
|---|---:|---|---|
| START | D2 | `%IX0.0` | Inicio del sistema |
| STOP | D3 | `%IX0.1` | Parada del sistema |
| B1 | D4 | `%IX0.2` | Nivel inferior |
| B2 | D5 | `%IX0.3` | Nivel intermedio |
| B3 | D6 | `%IX0.4` | Nivel superior |

## Salidas

| Señal | Pin Arduino | Dirección IEC | Estado |
|---|---:|---|---|
| H1 | D8 | `%QX0.0` | Nivel correcto |
| H2 | D9 | `%QX0.1` | Nivel bajo |
| H3 | D10 | `%QX0.2` | Nivel alto |
| H4 | D11 | `%QX0.3` | Tanque vacío |
| H5 | D12 | `%QX0.4` | Error de secuencia |
| Remoto | D13 | `%QX0.5` | Coil reservado para mando remoto |

## Tabla funcional

| B1 | B2 | B3 | Resultado |
|---:|---:|---:|---|
| 0 | 0 | 0 | H4 - Tanque vacío |
| 1 | 0 | 0 | H2 - Nivel bajo |
| 1 | 1 | 0 | H1 - Nivel correcto |
| 1 | 1 | 1 | H3 - Nivel alto |
| 0 | 1 | 0 | H5 - Error |
| 0 | 0 | 1 | H5 - Error |
| 1 | 0 | 1 | H5 - Error |
| 0 | 1 | 1 | H5 - Error |

La combinación `000` representa tanque vacío y no se considera una falla.

## Estado de validación

El montaje fue probado nuevamente durante RA3.2. Las entradas **START, STOP, B1, B2 y B3** respondieron correctamente y las salidas **H1-H5** reprodujeron la tabla funcional esperada.

La señal `Remoto` se reservó en D13 como `%QX0.5` para la etapa de control externo mediante Modbus FC05.

Con estas pruebas el activo físico queda validado como base del gemelo digital.
