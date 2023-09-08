---
title: Información general de secuencias de datos
description: Conecte la integración del SDK de Experience Platform del lado del cliente con productos de Adobe y destinos de terceros.
keywords: configuración;secuencias de datos;datasetreamId;edge;id de secuencia de datos;Configuración de entorno;edgeConfigId;identidad;sincronización de ID habilitada;ID de contenedor de sincronización de ID;espacio aislado;entrada de transmisión;conjunto de datos de evento;destinatario;código de cliente;token de propiedad;ID de entorno de destino;destinos de cookies;destinos de url;configuración de Analytics id de grupo de informes de bloque;preparación de datos para la recopilación de datos;preparación de datos;asignador;asignador XDM;asignador en Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: ht
source-wordcount: '780'
ht-degree: 100%

---


# Información general de secuencias de datos

Una secuencia de datos representa la configuración del lado del servidor al implementar los SDK web y móvil de Adobe Experience Platform. Mientras que el [comando configurar](../edge/fundamentals/configuring-the-sdk.md) en el SDK controla los elementos que se deben gestionar en el cliente (como el `edgeDomain`), las secuencias de datos gestionan todas las demás configuraciones del SDK. Cuando se envía una solicitud a Adobe Experience Platform Edge Network, el `edgeConfigId` se utiliza para hacer referencia a la secuencia de datos. Esto le permite actualizar la configuración del lado del servidor sin tener que realizar cambios en el código del sitio web.

Puede crear y administrar secuencias de datos seleccionando **[!UICONTROL Secuencias de datos]** en el panel de navegación izquierdo dentro de la IU de Adobe Experience Platform o de la IU de recopilación de datos.

![Pestaña secuencias de datos de la IU](assets/overview/datastreams-tab.png)

Para obtener más información sobre cómo configurar una secuencia de datos en la IU, consulte la [guía de configuración](./configure.md).

## Administración de datos confidenciales en secuencias de datos {#sensitive}

>[!IMPORTANT]
>
>Este documento no contiene un asesoramiento legal ni está pensado para sustituirlo. Consulte con el departamento legal de su empresa para obtener asesoramiento sobre el tratamiento de datos confidenciales.

Las políticas de administración de datos corporativos y los requisitos regulatorios son restricciones cada vez mayores sobre cómo se pueden recopilar, procesar y utilizar los datos confidenciales de los clientes. Esto incluye la recopilación, el procesamiento y el uso de los Datos de salud protegidos (PHI), que están sujetos a regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA).

Secuencias de datos proporciona tres métodos para ayudarle a gestionar de forma segura sus datos confidenciales:

* [Cifrado mejorado](#encryption)
* [Gobernanza de datos](#governance)
* [Registros de auditoría](#audit-logs)

### Cifrado mejorado {#encryption}

Todos los datos en tránsito a través de Edge Network se realizan a través de conexiones seguras y cifradas mediante [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si la secuencia de datos introduce datos en Experience Platform, estos se cifran en reposo en el lago de datos de Experience Platform. Consulte el documento sobre [cifrado de datos en Experience Platform](../landing/governance-privacy-security/encryption.md) para obtener más información.

### Gobernanza de datos {#governance}

Secuencias de datos aprovecha las capacidades integradas de control de datos de Experience Platform para evitar que los datos confidenciales se envíen a servicios no preparados para HIPAA. Al etiquetar campos específicos que contienen datos confidenciales en los esquemas de la secuencia de datos, puede tomar el control granular sobre qué campos de datos se pueden utilizar para fines específicos.

El siguiente vídeo proporciona una breve descripción sobre cómo se configuran y aplican las restricciones de uso de datos para secuencias de datos en la IU:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

En Experience Platform, puede aplicar [etiquetas de uso de datos confidenciales](../data-governance/labels/reference.md#sensitive) a esquemas y campos que contienen datos que su organización considera confidenciales. Por ejemplo, la etiqueta `RHD` se usa para denotar la Información médica protegida (PHI), y la etiqueta `S1` representa los datos de geolocalización.

>[!NOTE]
>
>Para obtener más información sobre cómo aplicar etiquetas de uso de datos dentro de la pestaña [!UICONTROL Esquemas] en la IU del Experience Platform o la IU de recopilación de datos, consulte el [tutorial de etiquetado del esquema](../xdm/tutorials/labels.md).

Al crear una nueva secuencia de datos, si el esquema seleccionado contiene etiquetas de uso de datos confidenciales, la secuencia de datos solo se puede configurar para enviar esos datos a destinos compatibles con HIPAA. Actualmente, el único destino compatible con HIPAA que admite secuencias de datos es Adobe Experience Platform. Otros servicios de destino, como Adobe Target, Adobe Analytics, Adobe Audience Manager, el reenvío de eventos y los destinos perimetrales, se desactivan para los flujos de datos que contienen etiquetas de uso de datos confidenciales.

Si se utiliza un esquema en una secuencia de datos existente con servicios no preparados para HIPAA, intentar agregar una etiqueta de uso de datos confidencial al esquema genera un mensaje de infracción de directiva y se impide la acción. El mensaje especifica qué secuencia de datos activó la infracción y sugiere eliminar cualquier servicio no compatible con HIPAA de la secuencia de datos para resolver el problema.

### Registros de auditoría

En Experience Platform, las actividades de secuencia de datos se pueden monitorizar en forma de registros de auditoría. Un registro de auditoría indica **quién** realizó **qué** acción, y **cuándo**, junto con otros datos contextuales que pueden ayudarle a solucionar problemas relacionados con secuencias de datos para ayudar a su empresa a cumplir con las políticas de administración de datos corporativos y los requisitos regulatorios.

Cada vez que un usuario crea, actualiza o elimina una secuencia de datos, se crea un registro de auditoría para registrar la acción. Lo mismo ocurre cada vez que un usuario crea, actualiza o elimina una asignación mediante [Preparación de datos para la recopilación de datos](./data-prep.md). Independientemente de si se ha actualizado una secuencia de datos o una asignación, el registro de auditoría resultante se clasifica en el tipo de recurso [!UICONTROL Secuencias de datos].

Consulte la documentación sobre [registros de auditoría](../landing/governance-privacy-security/audit-logs/overview.md) para obtener más información sobre cómo interpretar los registros de secuencias de datos y otros servicios compatibles.

## Pasos siguientes

En esta guía se proporciona una amplia descripción general de las secuencias de datos y su uso en la recopilación de datos y el procesamiento de datos confidenciales. Para ver los pasos sobre cómo configurar una nueva secuencia de datos, consulte la [guía de configuración de secuencia de datos](./configure.md).
