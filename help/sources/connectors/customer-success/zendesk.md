---
keywords: Experience Platform;inicio;temas populares;Zendesk;zendesk
solution: Experience Platform
title: Información general sobre el conector de origen de Zendesk
description: Obtenga información sobre cómo conectar Zendesk a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Zendesk]

>[!NOTE]
>
>La variable [!DNL Zendesk] el origen está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de cliente de terceros. La compatibilidad con los proveedores de éxito de clientes incluye [!DNL Zendesk].

Esta Adobe Experience Platform [sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) aprovecha el [API de búsqueda de Zendesk > Exportar resultados de búsqueda](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que devuelve la información de los usuarios al Experience Platform desde Zendesk para su posterior procesamiento.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Autentique su [!DNL Zendesk] account

[!DNL Zendesk] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL Zendesk] API.

Esta sección describe los pasos previos que se deben completar para autenticar su [!DNL Zendesk] cuenta.

* El primer paso para autenticar su [!DNL Zendesk] es para asegurarse de que tiene [!DNL Zendesk] cuenta de asistencia técnica. Si todavía no tiene uno, consulte la [[!DNL Zendesk] página de registro](https://www.zendesk.com/register/) para registrar y crear su cuenta de Zendesk.
* Una vez que se haya registrado correctamente, vaya a la [[!DNL Zendesk] sitio web](https://www.zendesk.com/login/) y proporcione **subdominio**.
* A continuación, seleccione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Finalmente, recupere el token de API desde la variable **[!DNL API token]** para obtener más información.

![Token de la API de Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte la [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) para obtener información sobre cómo recuperar el subdominio. Para obtener información sobre la generación del token de API, consulte la [[!DNL Zendesk] guía sobre la generación de un nuevo token de API](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

La siguiente documentación proporciona información sobre cómo conectar [!DNL Zendesk] a Platform mediante API o la interfaz de usuario:

## Connect [!DNL Zendesk] a Platform mediante API

* [Crear una conexión de origen y un flujo de datos para [!DNL Zendesk] uso de la API de servicio de flujo](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] a Platform mediante la interfaz de usuario

* [Cree un [!DNL Zendesk ]conexión de origen en la interfaz de usuario](../../tutorials/ui/create/customer-success/zendesk.md)
* [Crear un flujo de datos para una conexión de origen de éxito del cliente en la interfaz de usuario](../../tutorials/ui/dataflow/customer-success.md)
