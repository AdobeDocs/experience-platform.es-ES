---
keywords: Experience Platform;inicio;temas populares;salesforce marketing cloud;Marketing Cloud de Salesforce;automatización de marketing
solution: Experience Platform
title: Información general de origen de Marketing Cloud de Salesforce
description: Obtenga información sobre cómo conectar el Marketing Cloud de Salesforce a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# (Beta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>La variable [!DNL Salesforce Marketing Cloud] el origen está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona asistencia para la ingesta de datos desde sistemas de automatización de marketing de terceros. La compatibilidad con los proveedores de automatización de marketing incluye: [!DNL Salesforce Marketing Cloud].

## Requisitos previos

Antes de poder conectar su [!DNL Salesforce Marketing Cloud] de origen a Platform, debe asegurarse de que: **ámbitos de permisos** se aprovisionan a su [!DNL Salesforce Marketing Cloud] combinación de ID de cliente y secreto de cliente:

* `campaign_read`
* `list_and_subscribers_read`

Puede solicitar ámbitos realizando una llamada a la función `v2/userinfo` recurso de [!DNL Salesforce Marketing Cloud] API. Consulte la [[!DNL Salesforce Marketing Cloud] Documento de ámbitos de permiso de integración de API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) para obtener instrucciones sobre cómo solicitar y comparar ámbitos.

Para obtener más información sobre ámbitos, incluida una lista de sus permisos y comportamientos relacionados, consulte esta [[!DNL Salesforce Marketing Cloud] Documento de API de REST](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Connect [!DNL Salesforce Marketing Cloud] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Platform mediante API:

* [Creación de una conexión base de Marketing Cloud de Salesforce mediante la API de servicio de flujo](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Exploración de tablas de datos mediante la API de servicio de flujo](../../tutorials/api/explore/tabular.md)
* [Creación de un flujo de datos para una fuente de automatización de marketing mediante la API de servicio de flujo](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] a Platform mediante la interfaz de usuario

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Platform mediante la interfaz de usuario:

* [Crear una conexión de origen de Marketing Cloud de Salesforce en la interfaz de usuario](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Crear un flujo de datos para una conexión de origen de automatización de marketing en la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md)
