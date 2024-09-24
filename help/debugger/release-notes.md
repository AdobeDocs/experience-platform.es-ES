---
title: Notas de la versión de Adobe Experience Platform Debugger
description: Las notas de la versión más recientes de Adobe Experience Platform Debugger.
keywords: depurador;extensión de Experience Platform Debugger;chrome;extensión;notas de la versión
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 877e38154f6959d50bd0620290c2dce9decfc2b5
workflow-type: ht
source-wordcount: '781'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform Debugger

## Versión 1.6.1: 25 de julio de 2024

### Correcciones y mejoras

* Se ha corregido un problema que impedía a los usuarios añadir nuevos códigos incrustados de etiquetas a las páginas sin ellos.

## Versión 1.6.0: 11 de julio de 2024

### Nuevas funciones

* Permitir que los usuarios acepten la inclusión/exclusión de la recopilación de datos personales y técnicos.

### Correcciones y mejoras

* Corregir la inyección de scripts de Firefox y el vínculo de la política de privacidad.
* Capturar las solicitudes de Analytics que faltan.
* Corregir los bloqueos en páginas con muchos mensajes de consola complejos.
* Actualizar Adobe Experience Platform Debugger a la extensión Manifest v3.

## Versión 1.5.4: 19 de diciembre de 2023

### Correcciones y mejoras

* Se ha corregido un problema que impedía conservar la configuración.
* Se ha corregido un problema que hacía que Debugger se bloqueara al ver las visitas posteriores al procesamiento de Analytics.

## Versión 1.5.3: 6 de diciembre de 2023

### Nuevas funciones

* Se ha añadido la opción “Bloquear la pestaña activa al abrir Debugger”.

### Correcciones y mejoras

* Se ha corregido un problema por el que faltaban solicitudes de Analytics en dominios privados.
* Se ha corregido un problema por el que faltaban datos de Activity Map en la tabla de solicitudes de Analytics.
* Se ha corregido un problema por el que la visualización de TRACE de destino provocaba un bloqueo.
* Se ha añadido una advertencia cuando Debugger no puede configurar una infraestructura en la página en Firefox.

## Versión 1.5.2: 10 de noviembre de 2023

(Solo Firefox)

### Correcciones y mejoras

* Se ha actualizado la organización de archivos.

## Versión 1.5.1: 2 de noviembre de 2023

### Correcciones y mejoras

* Se han corregido problemas por los que los eventos de Analytics se ignoraban o duplicaban.
* Se ha corregido un problema por el que se superaba el tamaño máximo de almacenamiento de estado.
* Se ha corregido un problema por el que la búsqueda de Registros de Edge no filtraba eventos.

## Versión 1.5.0: 19 de octubre de 2023

### Nuevas funciones

* Mostrar vínculos a propiedad, entorno y reglas en resumen de etiquetas y registros.

### Correcciones y mejoras

* Se ha corregido un problema por el que los datos de resumen de etiquetas no se enviaban.
* Se ha corregido un problema por el que las sesiones de Assurance generaban un error CORS
* Se ha corregido un problema que impedía que apareciera TRACE de destino.
* Se ha corregido el botón “Enviar comentarios”.
* Se ha corregido el “ID de secuencia de datos” que faltaba en el Resumen de SDK web para la versión ≥2.18.0.
* Se ha corregido un problema que impedía buscar en los registros de Edge.
* Se ha añadido una nota sobre perfiles adicionales para determinados tipos de cuenta.

## Versión 1.4.1: 1 de noviembre de 2022

* Rendimiento mejorado en páginas con muchos eventos de Adobe Experience Platform Assurance.

## Versión 1.4.0: 3 de octubre de 2022

* Se ha añadido compatibilidad de depuración de AEP Assurance para implementaciones híbridas de SDK web.
* Se ha añadido compatibilidad con varias pestañas dentro de la misma sesión de AEP Assurance.
* Se ha corregido un problema por el que los usuarios no podían cambiar de perfil u organización después de iniciar sesión.
   * En algunas cuentas, es necesario cerrar la sesión y volver a iniciarla para cambiar de organización.
* Se ha añadido un mensaje de error cuando falla la habilitación de TRACE de destino.
* Dependencias actualizadas.

## Versión 1.3.3: 20 de junio de 2022

* Se ha corregido un problema que impedía abrir ventanas emergentes desde las tablas de eventos de red.
* Se ha corregido un problema que impedía cargar la información de Alloy en la página.

## Versión 1.3.2: 9 de junio de 2022

* Se ha añadido un avatar predeterminado cuando el usuario ha iniciado sesión.
* Se ha añadido el resaltado de sintaxis en los objetos JSON de los registros.

## Versión 1.3.1: 24 de mayo de 2022

* Dependencias actualizadas.
* Se ha corregido un problema de Analytics por el que no se podían habilitar las visitas posteriores al procesamiento.
* Se ha corregido un problema por el que el depurador se adjuntaba a la ventana de inicio de sesión de Adobe.
* Se ha corregido un problema de AT.js por el que los mensajes de registro no se mostraban en Debugger.

## Versión 1.3.0: 28 de enero de 2022

* Se ha añadido el vínculo Acerca de para mostrar la versión actual y las notas correspondientes.
* Se ha añadido un conmutador para ver las visitas posteriores al procesamiento de las solicitudes de Analytics. El conmutador está disponible en la sección Analytics.
* Se ha corregido un problema de sesión de depuración remota cuando la sesión se cerraba fuera del depurador.
* Se ha corregido una notificación de error que se mostraba en la pestaña Transacciones de Edge de SDK web.
* Se ha corregido la advertencia de obsolescencia en la página de etiquetas de Adobe cuando el depurador accedía al objeto _satellite.
* Se han corregido algunos casos en los que no se encontraba una instancia de AppMeasurement en la página.
* Se ha corregido un problema de conexión de página que se producía al abrir por primera vez la ventana del depurador.

## Versión 1.2.0: 26 de octubre de 2021

* Mostrar eventos de todas las pestañas del explorador en la vista de red. Para ver solo los eventos de la pestaña actual, seleccione el icono de candado en la esquina inferior derecha del depurador.
* Se ha actualizado la promoción de la marca.

## Versión 1.1.0: 5 de octubre de 2021

* Visualización de depuración remota: organice los eventos de depuración remota en un gráfico de flujo visual en la sección SDK web de Adobe Experience Platform > Transacciones de Edge.
* Requiere que la organización de SDK web de Adobe Experience Platform que se usa en la página coincida con la organización que ha iniciado sesión al comenzar una nueva sesión de depuración remota.
* Mostrar solo las transacciones de Edge de la pestaña conectada. Los registros de TRACE de destino siguen estando disponibles en la sección Registros > Edge.
* Permitir anular la configuración del ID de secuencia de datos independiente para cada instancia de SDK web de Adobe Experience Platform en la página. Añadir el conmutador de depuración habilitada.
* Se ha corregido un problema por el que el token de TRACE de Adobe Target no siempre se enviaba con sesiones de depuración remota para el SDK web de Adobe Experience Platform.

## Versión 1.0.0: 5 de mayo de 2021

* Primera versión principal de Experience Platform Debugger. Diseñada para sustituir a Experience Cloud Debugger.
