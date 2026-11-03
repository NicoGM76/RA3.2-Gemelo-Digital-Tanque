# 7. Conclusiones

La actividad RA3.2 tomó como base el sistema funcional desarrollado en RA2.3 y lo amplió hacia una arquitectura de gemelo digital.

Se comprobó que:

- el montaje físico conserva la lógica esperada,
- START, STOP, B1, B2 y B3 funcionan correctamente,
- H1-H5 reproducen los estados definidos del tanque,
- el Arduino UNO puede mantenerse como microcontrolador principal,
- Modbus RTU permite conectar el activo físico con CODESYS sin reemplazar el hardware existente,
- CODESYS refleja correctamente los cambios físicos en variables y HMI,
- el diagnóstico Modbus operó con solicitudes activas y sin errores durante la prueba observada,
- el computador puede emplearse como gateway para integrar una plataforma IoT sin adquirir un ESP32.

La cadena **Arduino UNO -> Modbus RTU -> CODESYS -> HMI** quedó validada de forma funcional.

Para la capa IoT se creó el dispositivo `Tanque_Digital` en Ubidots, sus variables, dashboard, indicadores, switch remoto y un gateway Python encargado de traducir entre Modbus RTU y HTTPS. Además se reservó el coil 5 / D13 como señal de control remoto.

La publicación real de datos y la orden Ubidots -> Arduino permanecen pendientes de la prueba final con el hardware conectado. Por esta razón no se reportan como validadas hasta observar su funcionamiento físico.

La solución demuestra que es posible extender un sistema de automatización existente hacia un gemelo digital e IoT reutilizando el hardware disponible, separando la solución en capas de activo físico, comunicación industrial, activo virtual y plataforma de supervisión remota.
