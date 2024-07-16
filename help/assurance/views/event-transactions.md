---
title: Vista Transacciones de los eventos
description: Esta guía detalla información sobre la vista de Transacciones de los eventos en Adobe Experience Platform Assurance.
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 100%

---

# Vista Transacciones de los eventos

La vista Transacciones de eventos de Adobe Experience Platform Assurance le permite validar y depurar la implementación del cliente Edge Network y ver los resultados de validación ascendente en casi tiempo real.

## Configuración de Assurance para el flujo de trabajo de Edge Network

Después de [configurar Assurance](../tutorials/implement-assurance.md), asegúrese de haber implementado las versiones más recientes de las extensiones de Assurance y Edge Network en la aplicación.

Para ver los eventos, en el menú de la izquierda, seleccione **[!UICONTROL Transacciones de eventos]** en la sección **[!UICONTROL Adobe Experience Platform Edge]**.

Si no ve esta opción, seleccione **[!UICONTROL Configurar]** en la parte inferior izquierda de la ventana, añada la vista **[!UICONTROL Transacciones de eventos]** y seleccione **[!UICONTROL Guardar]**.

## Introducción a la vista Transacciones de eventos

En esta sección, familiarícese con la vista Transacción de eventos y aprenda a utilizarla de forma eficaz para la validación de extremo a extremo en flujos de trabajo de Edge Network.

### Flujo de procesamiento de eventos

![Vista de transacciones de eventos](./images/event-transactions/event-transactions-view.png)

La vista Transacciones de eventos muestra tres columnas en el orden del flujo de procesamiento de eventos:

- **[!UICONTROL Lado del cliente]**: esta columna muestra los eventos procesados o recibidos del lado del cliente, accesibles para el SDK móvil. Esto incluye los eventos creados mediante una llamada de API, como `Edge.sendEvent`y los identificadores de evento de respuesta recibidos por el cliente desde el servidor de Edge Network, si los hay. Ejemplos de eventos del lado del cliente:
   - El evento de solicitud de AEP es el evento enviado a través de la extensión de Edge y contiene el XDM y los datos de forma libre opcionales.
   - El controlador de eventos de respuesta de AEP es el controlador de eventos recibido de Edge Network en respuesta a un evento de solicitud de AEP. Un evento de solicitud puede recibir uno o varios controladores de eventos de respuesta, como así también ninguno.
   - La respuesta de error de AEP se puede ver en el caso de un error, por ejemplo, si la carga útil de XDM no se ha podido procesar o si uno de los servicios de flujo ascendente ha devuelto un error o una advertencia.
- **[!UICONTROL Edge Network]**: esta columna muestra el evento recibido del lado del servidor por Edge Network a través de una solicitud de red y qué datos y metadatos contenía el evento.
- **[!UICONTROL Flujo ascendente]**: esta columna muestra los eventos recibidos por los servicios de flujo ascendente configurados, incluida información detallada sobre los resultados de procesamiento o de validación del evento entrante.
Tenga en cuenta que esta columna es dinámica y puede mostrar diferentes tipos de información según dos factores principales:
   - La configuración de la secuencia de datos y los servicios habilitados en ella.
   - El tipo de evento enviado a Edge Network.

### Eventos de Inspect

Los eventos mostrados en la vista Transacciones de eventos proporcionan información sobre el formato y el contenido de los datos que se procesan en cada estado, así como detalles reveladores sobre cualquier advertencia o error que se encuentre cuando los datos se procesan en sentido ascendente. La vista ayuda a reducir la información de depuración en el nivel de evento/solicitud e identificar errores al principio del ciclo de desarrollo.

#### Expanda los detalles del evento

Para inspeccionar un evento, seleccione el que desee en la vista. Esta acción amplía la vista **[!UICONTROL Detalles del evento]** en el lado derecho de la pantalla.
Los datos anidados se muestran en formato de árbol. Puede inspeccionar los valores clave anidados seleccionando el botón **+** (más) a la izquierda del nombre de la clave.

![Detalles del evento](./images/event-transactions/event-details.png)

#### Advertencias o errores de Inspect

Cada nombre de evento lleva como prefijo un icono que indica el estado de alto nivel del procesamiento de ese evento:

- Si el evento se ha procesado correctamente, se muestra una marca de verificación verde.
- Si se han detectado advertencias o errores, se muestra un signo de advertencia. Seleccione el evento relacionado para obtener más información acerca de la causa de la advertencia o el error en la vista **[!UICONTROL Detalles del evento]**.

### Parámetros de configuración

Puede comprobar el identificador de la secuencia de datos utilizado actualmente seleccionando la información del objeto junto al encabezado de columna **[!UICONTROL Edge Network]**.

![Mostrar el ID de la secuencia de datos](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Cuando varios clientes se conectan a la misma sesión de Assurance y se utilizan distintos ID de secuencia de datos, verá todos ellos aquí. Sin embargo, esto no significa que la implementación actual esté utilizando varios flujos de datos. Solo el ID de secuencia de datos actual establecido en la etiqueta (propiedad móvil) utilizada por la aplicación se utiliza para procesar los nuevos eventos de ese cliente. Al probar casos de uso más complicados con diferentes configuraciones y varios clientes conectados, puede resultar útil utilizar sesiones de Assurance independientes para simplificar el proceso de validación.
