---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Procesamiento de consentimiento en Adobe Experience Platform
description: Obtenga información sobre cómo procesar las señales de consentimiento del cliente en Adobe Experience Platform mediante el uso del estándar Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Procesamiento de consentimiento en Adobe Experience Platform

Adobe Experience Platform le permite procesar los datos de consentimiento que ha recopilado de sus clientes e integrarlos en sus perfiles de cliente almacenados. Los procesos descendentes pueden utilizar estos datos para determinar si la recopilación de datos se produce para un cliente específico o si sus perfiles se utilizan para fines específicos. Por ejemplo, los datos de consentimiento de un perfil determinado pueden determinar si se pueden incluir en un segmento de audiencia exportado o si pueden participar en canales de marketing específicos como correo electrónico, mensajes de texto o notificaciones push.

Este documento proporciona información general sobre cómo configurar las operaciones de datos de Platform para introducir datos de consentimiento del cliente generados por una plataforma de administración de consentimiento (CMP) e integrar esos datos en perfiles de clientes para casos de uso posteriores.

>[!NOTE]
>
>Este documento se centra en el procesamiento de datos de consentimiento mediante el uso del estándar de Adobe. Si procesa datos de consentimiento de conformidad con el marco de transparencia y consentimiento IAB (TCF) 2.0, consulte la guía de [Compatibilidad con TCF 2.0 en Adobe Real-time Customer Data Platform](../iab/overview.md).

## Requisitos previos

Esta guía requiere una comprensión práctica de los distintos servicios de Experience Platform implicados en el procesamiento de los datos de consentimiento:

* [Modelo de datos de experiencia (XDM)](/help/xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Servicio de identidad de Adobe Experience Platform](/help/identity-service/home.md): resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](/help/profile/home.md): Utiliza [!DNL Identity Service] funciones para crear perfiles detallados de los clientes a partir de los conjuntos de datos en tiempo real. El perfil del cliente en tiempo real extrae datos del lago de datos y conserva los perfiles de los clientes en su propio almacén de datos independiente.
* [SDK web de Adobe Experience Platform](/help/web-sdk/home.md): Una biblioteca JavaScript del lado del cliente que le permite integrar varios servicios de Platform en su sitio web del lado del cliente.
   * [Comandos de consentimiento de SDK](../../../../web-sdk/commands/setconsent.md): Información general sobre un caso de uso de los comandos de SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio de segmentación de Adobe Experience Platform](/help/segmentation/home.md): Permite dividir los datos del perfil del cliente en tiempo real en grupos de personas que comparten características similares y que responden de manera similar a las estrategias de marketing.

## Resumen del flujo de procesamiento de consentimiento {#summary}

A continuación se describe cómo se procesan los datos de consentimiento después de configurar correctamente el sistema:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos a través de un cuadro de diálogo en su sitio web.
1. Al cargar cada página (o cuando la CMP detecta un cambio en las preferencias de consentimiento), un script personalizado del sitio asigna las preferencias actuales a un objeto XDM estándar. A continuación, este objeto se pasa al SDK web de Platform `setConsent` comando.
1. Cuándo `setConsent` Cuando se llama a, el SDK web de Platform comprueba si los valores de consentimiento son diferentes de los que recibió por última vez. Si los valores son diferentes (o no hay ningún valor anterior), los datos de consentimiento/preferencia estructurados se envían a Adobe Experience Platform.
1. Los datos de consentimiento/preferencia se incorporan en una [!DNL Profile]Conjunto de datos habilitado para que contiene campos de consentimiento/preferencia.

Además de los comandos del SDK activados por los vínculos de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir a Experience Platform a través de cualquier dato XDM generado por el cliente que se cargue directamente en un [!DNL Profile]Conjunto de datos habilitado para.

### Aplicación del consentimiento

En la versión actual de compatibilidad con el procesamiento de consentimiento en Platform, solo el permiso de recopilación de datos (`collect.val`El SDK web de Platform aplica automáticamente ). Aunque se pueden recopilar y mantener consentimientos y preferencias más granulares en los perfiles de los clientes, estas señales adicionales deben aplicarse manualmente en sus propios procesos descendentes.

>[!NOTE]
>
>Para obtener más información sobre la estructura de los campos de consentimiento XDM mencionados anteriormente, consulte la guía de [[!UICONTROL Consentimientos y preferencias] tipo de datos](/help/xdm/data-types/consents.md).

Una vez configurado el sistema, el SDK web de Platform interpreta el valor de consentimiento de recopilación de datos para el usuario actual con el fin de determinar si los datos deben enviarse al Edge Network de Adobe Experience Platform, descartarse del cliente o conservarse hasta que el permiso de recopilación de datos se establezca en yes o no.

## Determine cómo generar datos de consentimiento de cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir a los clientes proporcionar consentimiento a medida que interactúan con el servicio. Una forma común de conseguirlo es mediante un cuadro de diálogo de consentimiento de cookies, similar al siguiente ejemplo:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Este cuadro de diálogo debe permitir al cliente adherirse o excluirse de casos de uso específicos de marketing y personalización para sus datos. Estos consentimientos y preferencias deben ajustarse al modelo de datos definido para [!DNL Profile]Conjunto de datos habilitado para en el siguiente paso.

## Adición de campos de consentimiento estandarizados a una [!DNL Profile]Conjunto de datos habilitado para {#dataset}

Los datos de consentimiento del cliente deben enviarse a una [!DNL Profile]Conjunto de datos habilitado para que contiene campos de consentimiento. Estos campos deben incluirse en el mismo esquema y conjunto de datos que se utiliza para capturar información de atributos sobre clientes individuales.

Consulte el tutorial sobre [configuración de un conjunto de datos para capturar datos de consentimiento](./dataset.md) para ver los pasos detallados sobre cómo añadir estos campos obligatorios a una [!DNL Profile]Conjunto de datos habilitado para antes de continuar con esta guía.

## Actualizar [!DNL Profile] combinar directivas para incluir datos de consentimiento {#merge-policies}

Una vez que haya creado una [!DNL Profile]Conjunto de datos habilitado para el procesamiento de datos de consentimiento. Debe asegurarse de que las políticas de combinación se hayan configurado para incluir siempre campos de consentimiento en cada perfil de cliente. Esto implica establecer la prioridad del conjunto de datos de modo que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos que puedan entrar en conflicto.

>[!NOTE]
>
>Si no tiene ningún conjunto de datos en conflicto, debe establecer la prioridad de la marca de tiempo para la política de combinación en su lugar. Esto ayuda a garantizar que el último consentimiento especificado por un cliente sea la configuración de consentimiento utilizada.

Para obtener más información sobre cómo trabajar con políticas de combinación, comience por leer el [resumen de políticas de combinación](../../../../profile/merge-policies/overview.md). Al configurar las políticas de combinación, debe asegurarse de que los perfiles incluyan todos los atributos de consentimiento requeridos proporcionados por el [!UICONTROL Consentimientos y preferencias] grupo de campos de esquema, como se describe en la guía de [preparación de conjuntos de datos](./dataset.md).

## Introducción de datos de consentimiento en Platform

Una vez que tenga los conjuntos de datos y las políticas de combinación para representar los campos de consentimiento requeridos en los perfiles de cliente, el siguiente paso es llevar los datos de consentimiento en sí a Platform.

Principalmente, debe utilizar el SDK web de Adobe Experience Platform para enviar datos de consentimiento a Platform cada vez que CMP detecte eventos de cambio de consentimiento. Si recopila datos de consentimiento en una plataforma móvil, debe utilizar el SDK móvil de Adobe Experience Platform. También puede optar por introducir los datos de consentimiento recopilados directamente asignándolos al esquema XDM del conjunto de datos de consentimiento y enviándolos a Platform mediante la ingesta por lotes.

En las subsecciones siguientes se proporcionan detalles sobre cada uno de estos métodos.

### Configuración del SDK web de Experience Platform para procesar datos de consentimiento {#web-sdk}

Una vez configurada la CMP para detectar eventos de cambio de consentimiento en el sitio web, se puede integrar el SDK web de Experience Platform para recibir la configuración de consentimiento actualizada y enviarla a Platform en cada carga de página y cada vez que se produzcan eventos de cambio de consentimiento. Consulte la guía de [configuración del SDK web para procesar datos de consentimiento del cliente](../sdk.md) para obtener más información.

### Configuración del SDK de Experience Platform Mobile para procesar datos de consentimiento {#mobile-sdk}

Si se requieren las preferencias de consentimiento del cliente en la aplicación móvil, puede integrar el SDK de Experience Platform Mobile para recuperar y actualizar la configuración de consentimiento y enviarlas a Platform cada vez que se invoque la API de consentimiento.

Consulte la documentación del SDK móvil para [configuración de la extensión móvil Consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) y [uso de la API de consentimiento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Para obtener más información sobre cómo gestionar los problemas de privacidad mediante el SDK móvil, consulte la sección [Privacidad y RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Ingesta directa de datos de consentimiento compatibles con XDM {#batch}

Puede introducir datos de consentimiento compatibles con XDM desde un archivo CSV mediante la ingesta por lotes. Esto puede resultar útil si tiene un registro de pendientes de datos de consentimiento recopilados anteriormente que aún no se han integrado en los perfiles de sus clientes.

Siga el tutorial de [asignación de un archivo CSV a XDM](../../../../ingestion/tutorials/map-csv/overview.md) para aprender a convertir los campos de datos a XDM e introducirlos en Platform. Al seleccionar la variable [!UICONTROL Destino] para la asignación, asegúrese de seleccionar la variable **[!UICONTROL Usar conjunto de datos existente]** y elija la opción [!DNL Profile]Conjunto de datos de consentimiento habilitado para que creó anteriormente.

## Prueba de la implementación {#test-implementation}

Después de haber introducido los datos de consentimiento del cliente en su [!DNL Profile]Conjunto de datos habilitado para, puede comprobar los perfiles actualizados para ver si contienen atributos de consentimiento.

>[!IMPORTANT]
>
>Para ver los atributos de un perfil existente en la interfaz de usuario de, debe conocer al menos un valor de identidad (y su área de nombres correspondiente) asociado a ese perfil.
>
>Si no tiene acceso a esta información, puede optar por introducir sus propios datos de consentimiento de prueba y asociarlos con un valor de identidad o área de nombres que conozca en su lugar.

Consulte la sección sobre [exploración de perfiles por identidad](../../../../profile/ui/user-guide.md#browse) en el [!DNL Profile] Guía de la interfaz de usuario para ver pasos específicos sobre cómo buscar los detalles de un perfil.

Los nuevos atributos de consentimiento no aparecerán en el panel de un perfil de forma predeterminada. Por lo tanto, debe navegar hasta el **[!UICONTROL Atributos]** en la página de detalles de un perfil para confirmar que se han introducido según lo esperado. Consulte la guía en la [tablero de perfiles](../../../../profile/ui/profile-dashboard.md) para aprender a personalizar el tablero para adaptarlo a sus necesidades.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Pasos siguientes

En esta guía se explica cómo configurar las operaciones de Platform para que procesen los datos de consentimiento del cliente mediante el estándar de Adobe y que estos atributos se representen en los perfiles de cliente. Ahora puede integrar las preferencias de consentimiento del cliente como factor determinante en la calificación de segmentos y otros casos de uso descendentes.

Para obtener más información sobre las funciones relacionadas con la privacidad de Experience Platform, consulte la información general sobre [gobernanza, privacidad y seguridad en Platform](../../overview.md).
