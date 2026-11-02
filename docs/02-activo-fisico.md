# 2. Activo físico

El activo físico corresponde al montaje construido en RA2.3 y reutilizado para RA3.2.

## Entradas

| Señal | Pin Arduino | Función |
|---|---:|---|
| START | D2 | Inicio del sistema |
| STOP | D3 | Parada del sistema |
| B1 | D4 | Nivel inferior |
| B2 | D5 | Nivel intermedio |
| B3 | D6 | Nivel superior |

## Salidas

| Señal | Pin Arduino | Estado |
|---|---:|---|
| H1 | D8 | Nivel correcto |
| H2 | D9 | Nivel bajo |
| H3 | D10 | Nivel alto |
| H4 | D11 | Tanque vacío |
| H5 | D12 | Error de secuencia |

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

El montaje fue reconstruido y probado nuevamente. Las entradas B1, B2 y B3 y las salidas H1-H5 responden a la lógica esperada. START se encuentra operativo. STOP continúa pendiente de ajuste físico y será documentado como limitación mientras se completa la integración.

> Pendiente: agregar fotografía final del montaje y evidencia de las pruebas físicas.
