# 1. Síntesis y alcance

RA3.2 toma como punto de partida el sistema de control de nivel desarrollado en RA2.3 y lo extiende hacia un **gemelo digital**. El objetivo es que el estado del activo físico pueda ser representado en CODESYS y posteriormente publicado y modificado desde una plataforma IoT.

## Requisitos de la actividad

La solución debe:

1. Reutilizar o modificar el activo físico de RA2.3.
2. Reutilizar o modificar el activo virtual desarrollado en CODESYS.
3. Conectar ambos mediante Arduino/ESP32 y protocolo Modbus.
4. Publicar el estado del tanque en una plataforma IoT.
5. Modificar el estado del tanque desde dicha plataforma.
6. Sustentar la solución en clase.
7. Documentar diseño, implementación y validación mediante una wiki con soporte gráfico.

## Estrategia adoptada

Se decidió reutilizar el **Arduino UNO** disponible y emplear comunicación **Modbus RTU por USB** entre Arduino y CODESYS. Para la capa IoT, el computador actuará como gateway hacia Internet.

Esta estrategia evita reemplazar el montaje físico ya validado y permite avanzar por etapas:

- activo físico,
- comunicación Modbus,
- sincronización con CODESYS,
- publicación IoT,
- control remoto,
- validación integral.
