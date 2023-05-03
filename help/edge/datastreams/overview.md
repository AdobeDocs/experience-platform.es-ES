---
title: Información general sobre Datastreams
description: Conecte la integración del SDK de Experience Platform del lado del cliente con productos de Adobe y destinos de terceros.
keywords: configuración;datastreams;datastreamId;edge;id de datastream;Configuración de entorno;edgeConfigId;identidad;sincronización de id habilitada;ID de contenedor de sincronización de ID;Sandbox;entrada de flujo;conjunto de datos de evento;target;código de cliente;token de propiedad;ID de entorno de Target;destinos de cookies;destinos de url;id de grupo de informes de bloqueo de configuración de Analytics;preparación de datos para recopilación de datos;Mp;prep de datos apper;XDM Mapper;Mapper on Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Información general sobre Datastreams

Una secuencia de datos representa la configuración del lado del servidor al implementar los SDK web y móvil de Adobe Experience Platform. Mientras que la variable [configurar, comando](../fundamentals/configuring-the-sdk.md) en el SDK controla los elementos que se deben gestionar en el cliente (como el `edgeDomain`), los conjuntos de datos administran todas las demás configuraciones para el SDK. Cuando se envía una solicitud a la red perimetral de Adobe Experience Platform, la variable `edgeConfigId` se utiliza para hacer referencia al conjunto de datos. Esto le permite actualizar la configuración del lado del servidor sin tener que realizar cambios de código en el sitio web.

Puede crear y administrar conjuntos de datos seleccionando **[!UICONTROL Datastreams]** en la navegación izquierda de la interfaz de usuario de Adobe Experience Platform o de la colección de datos.

![Ficha Datastreams en la interfaz de usuario](../assets/datastreams/overview/datastreams-tab.png)

Para obtener más información sobre cómo configurar un conjunto de datos en la interfaz de usuario, consulte la [guía de configuración](./configure.md).

## Gestión de datos confidenciales en conjuntos de datos {#sensitive}

>[!IMPORTANT]
>
>El contenido de este documento no es asesoramiento jurídico y no está pensado para sustituir el asesoramiento jurídico. Consulte con el departamento jurídico de su empresa para obtener asesoramiento sobre la gestión de datos confidenciales.

Las políticas de administración de datos corporativos y los requisitos regulatorios están aumentando las restricciones sobre cómo se pueden recopilar, procesar y utilizar los datos confidenciales de los clientes. Esto incluye la recolección, procesamiento y uso de Datos de Salud Protegidos (PHI) que están sujetos a regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, por sus siglas en inglés).

Datastreams proporciona tres métodos para ayudarle a gestionar de forma segura sus datos confidenciales:

* [Encriptado mejorado](#encryption)
* [Administración de datos](#governance)
* [Registros de auditoría](#audit-logs)

### Encriptado mejorado {#encryption}

Todos los datos en tránsito a través de la red perimetral se realizan a través de conexiones seguras y cifradas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si el conjunto de datos introduce datos en el Experience Platform, los datos se cifran en reposo en el lago de datos del Experience Platform. Consulte el documento en [cifrado de datos en Experience Platform](../../landing/governance-privacy-security/encryption.md) para obtener más información.

### Administración de datos {#governance}

Datastreams aprovecha las capacidades de control de datos integradas de Experience Platform para evitar que los datos confidenciales se envíen a servicios que no están preparados para HIPAA. Al etiquetar campos específicos que contienen datos confidenciales en los esquemas del conjunto de datos, puede tomar el control granular sobre qué campos de datos se pueden utilizar para fines específicos.

El siguiente vídeo ofrece una breve descripción general de cómo se configuran y aplican las restricciones de uso de datos para conjuntos de datos en la interfaz de usuario:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

En Experience Platform, puede aplicar [etiquetas de uso de datos confidenciales](../../data-governance/labels/reference.md#sensitive) a esquemas y campos que contienen datos que su organización considera confidenciales. Por ejemplo, la variable `RHD` se utiliza para denotar información protegida sobre la salud (PHI), y `S1` representa los datos de geolocalización.

>[!NOTE]
>
>Para obtener más información sobre cómo aplicar etiquetas de uso de datos en la variable [!UICONTROL Esquemas] en la interfaz de usuario del Experience Platform o de la recopilación de datos, consulte la [tutorial de etiquetado de esquemas](../../xdm/tutorials/labels.md).

Al crear un nuevo conjunto de datos, si el esquema seleccionado contiene etiquetas de uso de datos confidenciales, el conjunto de datos solo se puede configurar para enviar esos datos a destinos listos para HIPAA. Actualmente, el único destino listo para HIPAA compatible con los conjuntos de datos es Adobe Experience Platform. Otros servicios de destino, incluidos Adobe Target, Adobe Analytics, Adobe Audience Manager, el reenvío de eventos y los destinos Edge, están desactivados para los conjuntos de datos que contienen etiquetas de uso de datos confidenciales.

Si se está utilizando un esquema en un conjunto de datos existente con servicios no preparados para HIPAA, intentar agregar una etiqueta de uso de datos confidenciales al esquema genera un mensaje de infracción de directiva y se evita la acción. El mensaje especifica qué conjunto de datos activó la infracción y sugiere eliminar cualquier servicio no listo para HIPAA del conjunto de datos para resolver el problema.

### Registros de auditoría

En Experience Platform, las actividades del conjunto de datos se pueden monitorizar en forma de registros de auditoría. Un registro de auditoría indica **who** performed **what** acción y **when**, junto con otros datos contextuales que pueden ayudarle a solucionar problemas relacionados con los conjuntos de datos para ayudar a su empresa a cumplir con las políticas de administración de datos corporativos y los requisitos regulatorios.

Cada vez que un usuario crea, actualiza o elimina un conjunto de datos, se crea un registro de auditoría para registrar la acción. Lo mismo ocurre cuando un usuario crea, actualiza o elimina una asignación a través de [Preparación de datos para la recopilación de datos](./data-prep.md). Independientemente de si se trataba de un conjunto de datos o de una asignación que se actualizó, el registro de auditoría resultante se clasifica en la categoría [!UICONTROL Datastreams] tipo de recurso.

Consulte la documentación sobre [registros de auditoría](../../landing/governance-privacy-security/audit-logs/overview.md) para obtener más información sobre cómo interpretar los registros de conjuntos de datos y otros servicios compatibles.

## Pasos siguientes

Esta guía proporciona información general de alto nivel sobre los conjuntos de datos y su uso en la recopilación de datos y el procesamiento de datos confidenciales. Para ver los pasos sobre cómo configurar un nuevo conjunto de datos, consulte la [guía de configuración de datastream](./configure.md).
