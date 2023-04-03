---
title: Vista Transacciones de Evento
description: Esta guía detalla información sobre la vista Transacciones de Evento en Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Vista Transacciones de Evento

La vista Transacciones de eventos de Adobe Experience Platform Assurance permite validar y depurar la implementación de cliente de Edge Network y ver los resultados de validación de flujo ascendente casi en tiempo real.

## Configuración de Assurance para el flujo de trabajo de la red perimetral

Después [configuración de Assurance](../tutorials/implement-assurance.md), asegúrese de que ha implementado en su aplicación las versiones más recientes de las extensiones Assurance y Edge Network.

Para ver los eventos, en el menú de la izquierda, seleccione **[!UICONTROL Transacciones de Evento]** en el **[!UICONTROL Adobe Experience Platform Edge]** para obtener más información.

Si no ve esta opción, seleccione **[!UICONTROL Configurar]** en la parte inferior izquierda de la ventana, añada la variable **[!UICONTROL Transacciones de Evento]** ver y seleccionar **[!UICONTROL Guardar]**.

## Introducción a la vista Transacciones de eventos

En esta sección, familiarícese con la vista Transacción de eventos y aprenda a utilizarla de forma eficaz para la validación de principio a fin en los flujos de trabajo de la red perimetral.

### Flujo de procesamiento de eventos

![Vista de transacciones de eventos](./images/event-transactions/event-transactions-view.png)

La vista Transacciones de eventos muestra tres columnas en el orden del flujo de procesamiento de eventos:

- **[!UICONTROL Lado del cliente]**: Esta columna muestra los eventos procesados o recibidos del lado del cliente, accesibles para el SDK móvil. Esto incluye los eventos que se crearon mediante una llamada de API, como `Edge.sendEvent`, y los controladores de eventos de respuesta recibidos por el cliente desde el servidor de red perimetral, si los hay. Ejemplos de eventos del lado del cliente:
   - Evento de solicitud de AEP es el evento enviado a través de la extensión de Edge y contiene los datos XDM y de forma libre opcionales.
   - El Gestor de eventos de respuesta de AEP es el identificador de evento recibido de la red perimetral en respuesta a un evento de solicitud de AEP. Un evento de solicitud puede recibir uno, uno o varios controladores de eventos de respuesta.
   - La respuesta de error de AEP puede verse en caso de error, por ejemplo, si la carga útil XDM no se pudo procesar o si uno de los servicios de flujo ascendente devolvió un error o una advertencia.
- **[!UICONTROL Red perimetral]**: Esta columna muestra el evento recibido por la red perimetral del lado del servidor mediante una solicitud de red y los datos y metadatos que contiene el evento.
- **[!UICONTROL Upstream]**: Esta columna muestra los eventos recibidos por los servicios de flujo ascendente configurados, incluida la información detallada sobre los resultados de procesamiento y/o validación para el evento entrante.
Tenga en cuenta que esta columna es dinámica y puede mostrar diferentes tipos de información en función de dos factores principales:
   - La configuración del conjunto de datos y los servicios habilitados en él.
   - Tipo de evento enviado a la red perimetral.

### Eventos de Inspect

Los eventos mostrados en la vista Transacciones de eventos proporcionan información sobre el formato y el contenido de los datos que se procesan en cada estado, así como detalles exhaustivos sobre cualquier advertencia o error que se encuentre cuando los datos se procesen de forma ascendente. La vista ayuda a reducir la información de depuración en el nivel de evento/solicitud e identificar errores al principio del ciclo de desarrollo.

#### Expandir los detalles del evento

Para inspeccionar un evento, seleccione el que desee en la vista. Esta acción amplía el **[!UICONTROL Detalles del evento]** a la derecha de la pantalla.
Los datos anidados se muestran en formato de árbol. Puede inspeccionar los valores de claves anidados seleccionando la variable **+** (signo más) a la izquierda del nombre de la clave.

![Detalles del evento](./images/event-transactions/event-details.png)

#### Errores o advertencias de Inspect

A cada nombre de evento se le añade un icono que indica el estado de alto nivel del procesamiento de ese evento:

- Si el evento se procesó correctamente, se muestra una marca de verificación verde.
- Si se han detectado advertencias o errores, se muestra un signo de advertencia. Seleccione el evento relacionado para obtener más información sobre la causa de la advertencia o del error en la **[!UICONTROL Detalles del evento]** vista.

### Ajustes de configuración

Puede comprobar el identificador del conjunto de datos que se está utilizando seleccionando la información de objeto junto al **[!UICONTROL Red perimetral]** encabezado de columna.

![Mostrar el ID del conjunto de datos](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Cuando varios clientes se conectan a la misma sesión de garantía y se utilizan ID de flujo de datos diferentes, todos ellos se muestran aquí. Sin embargo, esto no significa que la implementación actual esté utilizando varios conjuntos de datos. Solo se utiliza el ID del conjunto de datos actual establecido en la etiqueta (propiedad móvil) utilizada por la aplicación para procesar nuevos eventos de ese cliente. Al probar casos de uso más complicados con diferentes configuraciones de configuración y varios clientes conectados, puede resultar útil utilizar sesiones de seguridad independientes para simplificar el proceso de validación.
