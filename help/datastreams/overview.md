---
title: Información general de secuencias de datos
description: Descubra cómo los flujos de datos le ayudan a conectar su integración de Experience Platform SDK del lado del cliente con productos de Adobe y destinos de terceros.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 48%

---

# Información general de secuencias de datos

Un conjunto de datos representa la configuración del lado del servidor para los SDK web y móvil de [!DNL Adobe Experience Platform]. Mientras que el comando [`configure`](/help/collection/js/commands/configure/overview.md) de SDK administra la configuración del lado del cliente (como `edgeDomain`), las secuencias de datos administran todas las demás configuraciones.

Cuando envía una solicitud a [!DNL Edge Network], `datastreamId` hace referencia al conjunto de datos al que se envían los datos. Puede actualizar la configuración del lado del servidor sin cambiar el código del sitio web.

Puede crear y administrar flujos de datos seleccionando **[!UICONTROL Datastreams]** en el panel de navegación izquierdo de la interfaz de usuario de [!DNL Adobe Experience Platform] o de la recopilación de datos.

![Captura de pantalla de la ficha Flujos de datos en la interfaz de usuario de Adobe Experience Platform.](assets/overview/datastreams-tab.png)

Para obtener más información sobre cómo configurar una secuencia de datos en la IU, consulte la [guía de configuración](/help/datastreams/configure.md).

## Administración de datos confidenciales en secuencias de datos {#sensitive}

>[!IMPORTANT]
>
>Este documento no contiene un asesoramiento legal ni está pensado para sustituirlo. Consulte con el departamento legal de su empresa para obtener asesoramiento sobre el tratamiento de datos confidenciales.

Las políticas de administración de datos corporativos y los requisitos regulatorios son restricciones cada vez mayores sobre cómo se pueden recopilar, procesar y utilizar los datos confidenciales de los clientes. Esto incluye la recopilación, el procesamiento y el uso de los Datos de salud protegidos (PHI), que están sujetos a regulaciones como la Ley de Portabilidad y Responsabilidad del Seguro de Salud (HIPAA, por sus siglas en inglés).

Las secuencias de datos proporcionan tres métodos para ayudarle a gestionar de forma segura sus datos confidenciales:

* [Cifrado mejorado](#encryption)
* [Gobernanza de datos](#governance)
* [Registros de auditoría](#audit-logs)

### Cifrado mejorado {#encryption}

Todos los datos en tránsito a través de [!DNL Edge Network] se realizan a través de conexiones seguras y cifradas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Si la secuencia de datos introduce datos en Experience Platform, estos se cifran en reposo en el lago de datos de Experience Platform. Consulte el documento sobre [cifrado de datos en Experience Platform](/help/landing/governance-privacy-security/encryption.md) para obtener más información.

### Gobernanza de datos {#governance}

Las secuencias de datos utilizan las funciones integradas de control de datos de Experience Platform para evitar que los datos confidenciales se envíen a servicios no preparados para HIPAA. Al etiquetar campos específicos que contienen datos confidenciales en los esquemas de la secuencia de datos, puede tomar el control granular sobre qué campos de datos se pueden utilizar para fines específicos.

El siguiente vídeo proporciona una breve descripción sobre cómo se configuran y aplican las restricciones de uso de datos para secuencias de datos en la IU:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

En Experience Platform, puede aplicar [etiquetas de uso de datos confidenciales](/help/data-governance/labels/reference.md#sensitive) a esquemas y campos que contienen datos que su organización considera confidenciales. Por ejemplo, la etiqueta `RHD` se usa para denotar la Información médica protegida (PHI), y la etiqueta `S1` representa los datos de geolocalización.

>[!NOTE]
>
>Para obtener más información sobre cómo aplicar etiquetas de uso de datos en la ficha [!UICONTROL Schemas] de la interfaz de usuario de Experience Platform o de la recopilación de datos, consulte el [tutorial de etiquetado de esquemas](/help/xdm/tutorials/labels.md).

Al crear una secuencia de datos, si el esquema seleccionado contiene etiquetas de uso de datos confidenciales, solo puede configurar la secuencia de datos para enviar esos datos a destinos compatibles con HIPAA. Actualmente, el único destino compatible con HIPAA que admiten flujos de datos es [!DNL Adobe Experience Platform]. Otros servicios de destino, como [!DNL Adobe Target], [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], reenvío de eventos y destinos perimetrales, están deshabilitados para las secuencias de datos que contienen etiquetas de uso de datos confidenciales.

Si se utiliza un esquema en una secuencia de datos existente con servicios no preparados para HIPAA, intentar agregar una etiqueta de uso de datos confidencial al esquema genera un mensaje de infracción de directiva y se impide la acción. El mensaje especifica qué secuencia de datos activó la infracción y sugiere eliminar cualquier servicio no compatible con HIPAA de la secuencia de datos para resolver el problema.

### Registros de auditoría {#audit-logs}

En Experience Platform, las actividades de secuencia de datos se pueden monitorizar en forma de registros de auditoría. Los registros de auditoría indican **quién** realizó **qué** acción, y **cuándo**, junto con otros datos contextuales que pueden ayudarle a solucionar problemas relacionados con flujos de datos para ayudar a su empresa a cumplir con las directivas de administración de datos corporativos y los requisitos regulatorios.

Cada vez que un usuario crea, actualiza o elimina una secuencia de datos, se crea un registro de auditoría para registrar la acción. Lo mismo ocurre cada vez que un usuario crea, actualiza o elimina una asignación mediante [Preparación de datos para la recopilación de datos](/help/datastreams/data-prep.md). Independientemente de si se ha actualizado un conjunto de datos o una asignación, el registro de auditoría resultante se clasifica en el tipo de recurso [!UICONTROL Datastreams].

Consulte la documentación sobre [registros de auditoría](/help/landing/governance-privacy-security/audit-logs/overview.md) para obtener más información sobre cómo interpretar los registros de secuencias de datos y otros servicios compatibles.

## Próximos pasos {#next-steps}

En esta guía se proporciona una amplia descripción general de las secuencias de datos y su uso en la recopilación de datos y el procesamiento de datos confidenciales. Para ver los pasos sobre cómo configurar una nueva secuencia de datos, consulte la [guía de configuración de secuencia de datos](/help/datastreams/configure.md).
