---
title: Vista de entrega de Edge
description: Esta guía detalla información sobre la vista Entrega perimetral en Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 1%

---

# Vista de entrega de Edge en Assurance

El **[!UICONTROL Entrega en Edge]** ver dentro **[!UICONTROL Adobe Experience Platform Assurance]** permite realizar comprobaciones y validaciones [!UICONTROL AJO entrante] envío de mensajes perimetrales a sus aplicaciones web y móviles. Esta vista es especialmente útil para solucionar problemas del envío de [!UICONTROL AJO entrante] campañas y recorridos web y móviles.

## Introducción

Antes de continuar, asegúrese de que tiene acceso a los siguientes servicios:

- El [IU de recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para obtener información sobre cómo instalar **[!UICONTROL Assurance]** en su aplicación, lea la [implementación de la guía Assurance](../tutorials/implement-assurance.md).

## Use Assurance con Edge Delivery

Una vez que abra una **[!UICONTROL Assurance]** sesión, puede añadir el **[!UICONTROL Entrega en Edge]** ver en **[!UICONTROL Assurance]**. En la parte inferior del panel izquierdo, seleccione **[!UICONTROL Configurar]** para añadir el **[!UICONTROL Entrega en Edge]** ver y **Guardar** it.

![Para añadir el complemento, seleccione Configurar en la parte inferior izquierda](./images/edge-delivery/add-plugin.png)

Una vez añadida, seleccione la **[!UICONTROL Entrega en Edge]** ver en la **[!UICONTROL Adobe Journey Optimizer]** para validar el envío perimetral entrante.

![Se puede acceder a Edge Delivery desde el grupo de vistas de Adobe Journey Optimizer](./images/edge-delivery/ajo-plugins.png)

## Lista de solicitudes

En el panel principal de la vista, se muestra la lista de solicitudes de entrega perimetral. Esta lista muestra todos los [!UICONTROL AJO entrante] solicitudes realizadas a Experience Edge y procesadas por el **[!UICONTROL Servicio de envío entrante]**, incluidas las solicitudes para recuperar decisiones de personalización, así como para realizar un seguimiento de las interacciones de propuestas de personalización (como mostrar, hacer clic, déclencheur o descartar).

Las solicitudes se ordenan por marca de tiempo, con las solicitudes más recientes en la parte superior. Además de la marca de tiempo, la lista también incluye una columna ID de solicitud, así como un Tipo de solicitud, que puede ser uno de los siguientes:

- **[!UICONTROL Entrega de experiencias]**: una solicitud para recuperar decisiones de personalización
- **[!UICONTROL Interacciones de experiencia]**: una solicitud para rastrear interacciones de propuestas de personalización
- **[!UICONTROL Entrega de experiencias e interacciones]**: una solicitud para recuperar decisiones de personalización que también incluyen interacciones de propuesta de personalización
- **[!UICONTROL Previsualizar envío]**: una solicitud para recuperar la vista previa de decisiones de personalización

Las solicitudes también se pueden filtrar introduciendo un término de búsqueda en la barra de búsqueda de la parte superior de la lista. Esto resulta útil a la hora de filtrar por valores específicos, como ID.

![La lista de las solicitudes entrantes se muestra en la vista principal](./images/edge-delivery/request-list.png)

## Vistas de solicitud detalladas

Una vez seleccionada una solicitud en la vista principal, a la derecha se muestra información detallada sobre la solicitud seleccionada. Esta vista incluye las siguientes secciones:

### Resumen de solicitudes

Esta sección proporciona información general de alto nivel sobre la solicitud seleccionada, incluyendo lo siguiente [!UICONTROL ID de organización], [!UICONTROL Clúster de Edge], [!UICONTROL ID de solicitud] y [!UICONTROL Tipo de solicitud], [!UICONTROL ID de zona protegida], [!UICONTROL Nombre de zona protegida], [!UICONTROL ID de flujo de datos], así como la lista de superficies de solicitud en caso de [!UICONTROL Entrega de experiencias] solicitudes.

![La sección de información general de solicitudes proporciona detalles de solicitud de alto nivel](./images/edge-delivery/request-overview.png)

### Perfil

Esta sección proporciona información sobre los datos de perfil utilizados al procesar la solicitud, incluido el mapa de identidad, la pertenencia a segmentos y la configuración de consentimiento.\
El [!UICONTROL Perfil] Esta sección es muy útil cuando se solucionan problemas como que la entrega no funciona como se espera debido a la falta o al retraso de la membresía del segmento o la configuración del consentimiento de exclusión.

![La sección Perfil incluye el mapa de identidad, la pertenencia a segmentos y la configuración de consentimiento](./images/edge-delivery/profile.png)

### Actividades calificadas

En esta sección se proporciona una lista de las actividades cualificadas para la solicitud seleccionada, incluido el tipo de actividad, los ID, el área de nombres de identidad, las superficies, la programación y las audiencias. Encontrará información más detallada sobre la actividad en la [sección de seguimiento de ejecución sin procesar](#execution).

![La sección Actividades cualificadas contiene los detalles de las actividades cualificadas](./images/edge-delivery/qualified-activities.png)

### Actividades no calificadas

Esta sección proporciona una lista de las actividades que se excluyeron de la calificación. Además del tipo de actividad, los ID, las áreas de nombres de identidad, las superficies, las programaciones y las audiencias, esta sección también incluye una lista de motivos por los que la actividad no estaba cualificada.

![La sección Actividades no cualificadas contiene detalles de actividad no cualificados y motivos de exclusión](./images/edge-delivery/unqualified-activities.png)

### Detalles del mensaje

Esta sección proporciona información detallada sobre los mensajes enviados para la solicitud seleccionada. Incluye ID de mensaje, fragmentos, políticas de decisión, etc. [!UICONTROL Offer decisioning] parámetros, así como el contexto de selección de mensajes.

![Sección que contiene detalles del mensaje enviado, como ID de mensaje y contexto de selección, fragmentos, políticas de decisión y parámetros de decisión](./images/edge-delivery/message-details.png)

### Interacciones

Esta sección proporciona información detallada sobre las interacciones de las que se ha realizado un seguimiento en la solicitud seleccionada. Incluye el tipo de interacción (en `propositionEventType`), así como los metadatos de propuestas asociados, como los metadatos de actividades (en `scopeDetails.activity`) y token de evento de propuesta (en `scopeDetails.characteristics.eventToken`).

![El seguimiento de las interacciones se realiza mediante tokens de propuesta y metadatos de actividad asociados](./images/edge-delivery/interactions.png)

### Rastros sin procesar

Esta sección proporciona los seguimientos sin procesar de la solicitud seleccionada. Incluye el seguimiento completo de la solicitud, incluida la solicitud real tal y como se recibió en **[!UICONTROL Servicio de envío entrante]**, seguimiento de ejecución y seguimiento de respuesta. Esto resulta útil para la resolución de problemas avanzada, como que la entrega no funciona según lo esperado debido a la indisponibilidad del servicio de entrega, la falta de datos o datos incorrectos, o para comprender el flujo completo del procesamiento de solicitudes.

#### Solicitud

El seguimiento de la solicitud incluye la solicitud completa tal como la recibió el **[!UICONTROL Servicio de envío entrante]** **[!UICONTROL Konductor]** río arriba. Incluye los encabezados de solicitud, el cuerpo y otros metadatos. Por ejemplo, la carga útil XDM de la solicitud se puede inspeccionar en la variable `event.body.xdm` field.

![Encontrará información detallada sobre la solicitud, incluidos los encabezados y el cuerpo, en el seguimiento de solicitudes](./images/edge-delivery/request.png)

#### Ejecución

El seguimiento de ejecución incluye el seguimiento completo de la solicitud tal como la procesó el **[!UICONTROL Servicio de envío entrante]**. Muestra el contexto de ejecución, la calificación de la actividad, la selección del mensaje y otros pasos de procesamiento. Cualquier error o advertencia que se haya producido durante el procesamiento de la solicitud se encuentra en `context.messages` y `context.exceptions` campos. Encontrará información detallada sobre la cualificación de actividades en la `context.qualifiedActivitiesDetailed` y `context.unqualifiedActivitiesDetailed` campos.

![El seguimiento de ejecución incluye el contexto de ejecución, la calificación de la actividad, la selección de mensajes y otros detalles de procesamiento](./images/edge-delivery/execution.png)

#### Respuesta

El seguimiento de respuestas incluye la respuesta completa tal como la devolvió **[!UICONTROL Servicio de envío entrante]** flujo descendente a **[!UICONTROL Konductor]**. Incluye los encabezados de respuesta, el cuerpo y otros metadatos. El cuerpo de respuesta completo se puede inspeccionar copiando el mensaje con el ID `1` al portapapeles mediante el **[!UICONTROL Copiar valor]** y pegarlo en un visor JSON.

![El seguimiento de respuestas contiene el cuerpo de respuesta completo devuelto en sentido descendente](./images/edge-delivery/response.png)
