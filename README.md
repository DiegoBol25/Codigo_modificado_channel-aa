
# Menú Interactivo en Asterisk usando ARI

Este proyecto implementa un sistema de respuesta de auto atendida (aa, por sus siglas en inglés) utilizando la Interfaz de Asterisk basada en REST (ARI), Node.js y basado en el ejemplo de channel-aa.
Está diseñado para recibir llamadas entrantes, reproducir un menú de opciones y manejar las decisiones del usuario mediante la detección de tonos DTMF.

## Objetivo del Proyecto

El objetivo es demostrar cómo construir un aa básico pero funcional utilizando JavaScript y ARI para Asterisk.
Este tipo de sistemas es común en aplicaciones de atención al cliente, encuestas telefónicas automatizadas, confirmación de citas, entre otros.

##  Funcionalidades Principales

- Conexión a Asterisk vía ARI: Utiliza la librería `ari-client` para conectarse al servidor Asterisk expuesto en el puerto 8088.
- Gestión de eventos en canales: Se manejan eventos como `StasisStart`, `StasisEnd` y `ChannelDtmfReceived` para controlar el flujo de llamadas y detectar entradas del usuario.
- Reproducción de menú interactivo: Se reproducen mensajes de voz que invitan al usuario a presionar una opción del menú.
- Manejo de entradas DTMF:
  - Opción 1: Redirige la llamada a la extensión 100 del contexto `default`.
  - Opción 2: Termina la llamada.
  - Otras opciones: Reproduce un mensaje indicando que la opción es inválida y reinicia el menú.
- Temporizador de inactividad: Si no se presiona ninguna tecla durante 10 segundos tras escuchar el menú, se reproduce un mensaje adicional y se reinicia el menú.
- Limpieza de recursos: Se eliminan temporizadores y listeners activos cuando el canal termina para evitar fugas de memoria.

## Estructura del Código

El archivo principal del proyecto sigue esta estructura:

1. Conexión ARI: Establecida mediante `ari.connect(...)`.
2. Definición del menú: Se define un conjunto de opciones válidas y los sonidos a reproducir.
3. Manejo de eventos: Se suscriben funciones a eventos clave como `StasisStart` y `ChannelDtmfReceived`.
4. Reproducción de menú: Se utiliza una lógica secuencial para reproducir múltiples audios y permitir su interrupción por entrada del usuario.
5. Acciones por opción DTMF: El script ejecuta distintas acciones según la tecla presionada.
6. Control de estado: Utiliza estructuras como objetos y temporizadores para controlar la ejecución del menú de forma reactiva.


##  Instalación y Ejecución

Este proyecto utiliza credenciales simples (`asterisk` / `asterisk`) solo para fines de prueba. Para entornos de producción, se recomienda:

- Usar HTTPS en la interfaz ARI.
- Configurar usuarios y contraseñas fuertes.
- Usar firewalls y control de acceso.


## Autor

Diego Alejandro Bolaños
Estudiante de Ingeniería Electrónica y Telecomunicaciones  
Universidad del Cauca  
diegoabolanos@unicauca.edu.co


## Ideas futuras

- Implementar un menú de varios niveles.
- Integrar con bases de datos para opciones dinámicas.
- Generar reportes automáticos de llamadas recibidas.
- Usar WebSocket para control en tiempo real.

