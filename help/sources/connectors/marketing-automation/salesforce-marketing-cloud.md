---
solution: Experience Platform
title: Información general sobre Salesforce Marketing Cloud Source
description: Obtenga información sobre cómo conectar Salesforce Marketing Cloud a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto a finales de junio de 2025.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde sistemas de automatización de marketing de terceros. Los proveedores de automatización de marketing admiten [!DNL Salesforce Marketing Cloud].

## Requisitos previos

Para poder conectar el origen de [!DNL Salesforce Marketing Cloud] a Experience Platform, debe asegurarse de que los siguientes **ámbitos de permisos** estén aprovisionados para la combinación de ID de cliente y secreto de cliente de [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Puede solicitar ámbitos realizando una llamada al recurso `v2/userinfo` de la API [!DNL Salesforce Marketing Cloud]. Consulte el [[!DNL Salesforce Marketing Cloud] documento Ámbitos de permisos de integración de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obtener instrucciones sobre cómo solicitar y comparar ámbitos.

Para obtener más información sobre los ámbitos, incluida una lista de sus permisos y comportamientos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento de API de REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API:

* [Crear una conexión base de Salesforce Marketing Cloud mediante la API de Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Cree un flujo de datos para una fuente de automatización de marketing mediante la API de Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario:

* [Crear una conexión de origen de Salesforce Marketing Cloud en la interfaz de usuario](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Cree un flujo de datos para una conexión de origen de automatización de marketing en la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md)
