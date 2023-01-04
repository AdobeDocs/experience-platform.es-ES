---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Procesamiento de consentimiento en Adobe Experience Platform
topic-legacy: getting started
description: Aprenda a procesar las señales de consentimiento del cliente en Adobe Experience Platform mediante el estándar Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---

# Procesamiento de consentimiento en Adobe Experience Platform

Adobe Experience Platform le permite procesar los datos de consentimiento que ha recopilado de sus clientes e integrarlos en los perfiles de clientes almacenados. Los procesos descendentes pueden utilizar estos datos para determinar si la recopilación de datos se produce para un cliente específico o si sus perfiles se utilizan para fines específicos. Por ejemplo, los datos de consentimiento de un perfil en particular pueden determinar si se pueden incluir en un segmento de audiencia exportado o si pueden participar en canales de marketing específicos, como correo electrónico, mensajes de texto o notificaciones push.

Este documento proporciona información general sobre cómo configurar las operaciones de datos de Platform para introducir datos de consentimiento del cliente generados por una plataforma de administración de consentimiento (CMP) e integrar esos datos en perfiles del cliente para casos de uso posteriores.

>[!NOTE]
>
>Este documento se centra en el procesamiento de datos de consentimiento mediante el estándar de Adobe. Si está procesando datos de consentimiento de conformidad con el marco de transparencia y consentimiento IAB (TCF) 2.0, consulte la guía de [Compatibilidad con TCF 2.0 en Adobe Real-time Customer Data Platform](../iab/overview.md).

## Requisitos previos

Esta guía requiere una comprensión práctica de los distintos servicios de Experience Platform involucrados en el procesamiento de datos de consentimiento:

* [Modelo de datos de experiencia (XDM)](../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Servicio de identidad de Adobe Experience Platform](../../../../identity-service/home.md): Resuelve el desafío fundamental que plantea la fragmentación de los datos de experiencia del cliente al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../../../../profile/home.md): Usos [!DNL Identity Service] funciones para crear perfiles de cliente detallados a partir de sus conjuntos de datos en tiempo real. El perfil del cliente en tiempo real extrae datos del lago de datos y mantiene los perfiles del cliente en su propio almacén de datos independiente.
* [SDK web de Adobe Experience Platform](../../../../edge/home.md): Una biblioteca JavaScript del lado del cliente que le permite integrar varios servicios de Platform en su sitio web de cliente.
   * [Comandos de consentimiento SDK](../../../../edge/consent/supporting-consent.md): Una descripción general del caso de uso de los comandos del SDK relacionados con el consentimiento que se muestran en esta guía.
* [Servicio de segmentación de Adobe Experience Platform](../../../../segmentation/home.md): Permite dividir los datos del perfil del cliente en tiempo real en grupos de individuos que comparten características similares y que responderán de manera similar a las estrategias de marketing.

## Resumen del flujo de procesamiento de consentimiento {#summary}

A continuación se describe cómo se procesan los datos de consentimiento una vez configurado correctamente el sistema:

1. Un cliente proporciona sus preferencias de consentimiento para la recopilación de datos mediante un cuadro de diálogo en el sitio web.
1. En cada carga de página (o cuando su CMP detecta un cambio en las preferencias de consentimiento), un script personalizado del sitio asigna las preferencias actuales a un objeto XDM estándar. Este objeto se pasa entonces al SDK web de Platform `setConsent` comando.
1. When `setConsent` , el SDK web de Platform comprueba si los valores de consentimiento son diferentes de los recibidos por última vez. Si los valores son diferentes (o no hay ningún valor anterior), los datos estructurados de consentimiento/preferencia se envían a Adobe Experience Platform.
1. Los datos de consentimiento/preferencia se incorporan en un [!DNL Profile]Conjunto de datos habilitado para , cuyo esquema contiene campos de consentimiento/preferencia.

Además de los comandos del SDK activados por los enlaces de cambio de consentimiento de CMP, los datos de consentimiento también pueden fluir en el Experience Platform a través de cualquier dato XDM generado por el cliente que se cargue directamente en un [!DNL Profile]conjunto de datos habilitado para .

### Cumplimiento del consentimiento

En la versión actual de la compatibilidad con el procesamiento de consentimiento en Platform, solo el permiso de recopilación de datos (`collect.val`) se aplica automáticamente mediante el SDK web de Platform. Aunque se pueden recopilar y mantener consentimientos y preferencias más granulares en los perfiles de cliente, estas señales adicionales deben aplicarse manualmente en sus propios procesos descendentes.

>[!NOTE]
>
>Para obtener más información sobre la estructura de los campos de consentimiento XDM mencionados anteriormente, consulte la guía de [[!UICONTROL Consentimientos y preferencias] tipo de datos](../../../../xdm/data-types/consents.md).

Una vez configurado el sistema, el SDK web de la plataforma interpreta el valor del consentimiento de la recopilación de datos para el usuario actual a fin de determinar si los datos deben enviarse a la red perimetral de Adobe Experience Platform, dejarse caer del cliente o persistir hasta que el permiso de recopilación de datos se establezca en sí o no.

## Determinar cómo generar datos de consentimiento del cliente dentro de su CMP {#consent-data}

Dado que cada sistema CMP es único, debe determinar la mejor manera de permitir que sus clientes den su consentimiento mientras interactúan con su servicio. Una forma común de conseguirlo es mediante un cuadro de diálogo de consentimiento de cookie, similar al siguiente ejemplo:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Este cuadro de diálogo debe permitir al cliente activar o desactivar casos de uso de marketing y personalización específicos para sus datos. Estos consentimientos y preferencias deben ajustarse al modelo de datos definido para la variable [!DNL Profile]conjunto de datos habilitado para en el siguiente paso.

## Añadir campos de consentimiento estandarizado a un [!DNL Profile]conjunto de datos habilitado {#dataset}

Los datos de consentimiento del cliente deben enviarse a un [!DNL Profile]conjunto de datos habilitado para , cuyo esquema contiene campos de consentimiento. Estos campos deben incluirse en el mismo esquema y conjunto de datos que utiliza para capturar información de atributos sobre clientes individuales.

Consulte el tutorial en [configuración de un conjunto de datos para capturar datos de consentimiento](./dataset.md) para ver los pasos detallados sobre cómo agregar estos campos obligatorios a un [!DNL Profile]conjunto de datos habilitado para .

## Actualizar [!DNL Profile] combinar directivas para incluir datos de consentimiento {#merge-policies}

Una vez que haya creado un [!DNL Profile]conjunto de datos habilitado para procesar datos de consentimiento, debe asegurarse de que las políticas de combinación se hayan configurado para incluir siempre campos de consentimiento en cada perfil del cliente. Esto implica establecer la prioridad del conjunto de datos para que el conjunto de datos de consentimiento tenga prioridad sobre otros conjuntos de datos potencialmente conflictivos.

>[!NOTE]
>
>Si no tiene conjuntos de datos en conflicto, debe establecer la prioridad de la marca de tiempo para la política de combinación. Esto ayuda a garantizar que el consentimiento más reciente especificado por un cliente sea la configuración de consentimiento que se utiliza.

Para obtener más información sobre cómo trabajar con políticas de combinación, comience por leer la [información general sobre políticas de combinación](../../../../profile/merge-policies/overview.md). Al configurar las políticas de combinación, debe asegurarse de que los perfiles incluyan todos los atributos de consentimiento necesarios proporcionados por la variable [!UICONTROL Consentimientos y preferencias] grupo de campos de esquema, tal como se describe en la guía de [preparación del conjunto de datos](./dataset.md).

## Incorporar datos de consentimiento a Platform

Una vez que tenga sus conjuntos de datos y políticas de combinación para representar los campos de consentimiento requeridos en sus perfiles de cliente, el siguiente paso es introducir los datos de consentimiento en Platform.

Principalmente, debe utilizar el SDK web de Adobe Experience Platform para enviar datos de consentimiento a Platform siempre que su CMP detecte eventos de cambio de consentimiento. Si recopila datos de consentimiento en una plataforma móvil, debe utilizar el SDK de Adobe Experience Platform Mobile. También puede optar por ingerir los datos de consentimiento recopilados directamente asignándolos al esquema XDM de su conjunto de datos de consentimiento y enviándolos a Platform mediante la ingesta por lotes.

En las subsecciones siguientes se proporcionan detalles sobre cada uno de estos métodos.

### Configuración del SDK web del Experience Platform para procesar los datos de consentimiento {#web-sdk}

Una vez que haya configurado su CMP para que detecte eventos de cambio de consentimiento en su sitio web, puede integrar el SDK web del Experience Platform para que reciba la configuración de consentimiento actualizada y la envíe a Platform en cada carga de página y cada vez que se produzcan eventos de cambio de consentimiento. Consulte la guía de [configuración del SDK web para procesar datos de consentimiento del cliente](../sdk.md) para obtener más información.

### Configuración del SDK de Experience Platform Mobile para procesar los datos de consentimiento {#mobile-sdk}

Si las preferencias de consentimiento del cliente son necesarias en su aplicación móvil, puede integrar el SDK móvil de Experience Platform para recuperar y actualizar la configuración de consentimiento y enviarla a Platform siempre que se llame a la API de consentimiento.

Consulte la documentación del SDK móvil para [configuración de la extensión móvil de consentimiento](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) y [uso de la API de consentimiento](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). Para obtener más información sobre cómo gestionar los problemas de privacidad mediante el SDK de Mobile, consulte la sección . [Privacidad y RGPD](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### Ingesta directa de datos de consentimiento compatibles con XDM {#batch}

Puede ingerir datos de consentimiento compatibles con XDM desde un archivo CSV mediante la ingesta por lotes. Esto puede resultar útil si tiene una acumulación de datos de consentimiento recopilados anteriormente que aún no se han integrado en sus perfiles de cliente.

Siga el tutorial en [asignación de un archivo CSV a XDM](../../../../ingestion/tutorials/map-csv/overview.md) para aprender a convertir los campos de datos a XDM e introducirlos en Platform. Al seleccionar la variable [!UICONTROL Destino] para la asignación, asegúrese de seleccionar la variable **[!UICONTROL Usar conjunto de datos existente]** y seleccione [!DNL Profile]conjunto de datos de consentimiento habilitado para .

## Probar la implementación {#test-implementation}

Una vez introducidos los datos de consentimiento del cliente en su [!DNL Profile]El conjunto de datos habilitado para , puede comprobar los perfiles actualizados para ver si contienen atributos de consentimiento.

>[!IMPORTANT]
>
>Para ver los atributos de un perfil existente en la interfaz de usuario, debe conocer al menos un valor de identidad (y su área de nombres correspondiente) asociado a ese perfil.
>
>Si no tiene acceso a esta información, puede optar por ingerir sus propios datos de consentimiento de prueba y asociarlos a un valor de identidad/área de nombres que conozca.

Consulte la sección sobre [exploración de perfiles por identidad](../../../../profile/ui/user-guide.md#browse) en el [!DNL Profile] Guía de la interfaz de usuario para ver los pasos específicos sobre cómo buscar los detalles de un perfil.

De forma predeterminada, los nuevos atributos de consentimiento no aparecen en el panel de un perfil. Por lo tanto, debe navegar hasta la **[!UICONTROL Atributos]** en la página de detalles de un perfil para confirmar que se han introducido tal como se esperaba. Consulte la guía de [panel de perfiles](../../../../profile/ui/profile-dashboard.md) para aprender a personalizar el tablero según sus necesidades.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Pasos siguientes

Esta guía explica cómo configurar las operaciones de Platform para procesar los datos de consentimiento del cliente mediante el estándar de Adobe y hacer que esos atributos se representen en los perfiles del cliente. Ahora puede integrar las preferencias de consentimiento del cliente como factor determinante en la calificación de segmentos y otros casos de uso descendente.

Para obtener más información sobre las funcionalidades relacionadas con la privacidad de Experience Platform, consulte la descripción general de [administración, privacidad y seguridad en Platform](../../overview.md).
