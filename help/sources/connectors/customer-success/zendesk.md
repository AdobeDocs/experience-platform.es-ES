---
title: Descripción general del conector de origen de Zendesk
description: Obtenga información sobre cómo conectar Zendesk a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 2%

---

# [!DNL Zendesk]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de clientes de terceros. Los proveedores de éxito de los clientes incluyen [!DNL Zendesk].

Esta Adobe Experience Platform [orígenes](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es) aprovecha el [API de búsqueda de Zendesk > Exportar resultados de búsqueda](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que devuelve la información de los usuarios a Experience Platform desde Zendesk para un procesamiento posterior.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Autentique su [!DNL Zendesk] account

[!DNL Zendesk] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL Zendesk] API.

Esta sección describe los pasos necesarios para completar la autenticación de su [!DNL Zendesk] cuenta.

* El primer paso para autenticar su [!DNL Zendesk] La cuenta de es para garantizar que dispone de [!DNL Zendesk] cuenta de asistencia. Si todavía no dispone de uno, consulte la [[!DNL Zendesk] página de registro](https://www.zendesk.com/register/) para registrarse y crear su cuenta de Zendesk.
* Una vez que se haya registrado correctamente, vaya a [[!DNL Zendesk] sitio web](https://www.zendesk.com/login/) y proporcione su **subdominio**.
* A continuación, seleccione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Finalmente, recupere el token de API de la **[!DNL API token]** sección.

![Token de API de Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte la [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) para obtener información sobre cómo recuperar el subdominio. Para obtener información sobre la generación del token de API, consulte la [[!DNL Zendesk] guía sobre la generación de un nuevo token de API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Zendesk] Vaya a Platform mediante las API o la interfaz de usuario de:

## Connect [!DNL Zendesk] a Platform mediante API

* [Crear una conexión de origen y un flujo de datos para [!DNL Zendesk] uso de la API de Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] a Platform mediante la IU

* [Crear un [!DNL Zendesk ]conexión de origen en la interfaz de usuario](../../tutorials/ui/create/customer-success/zendesk.md)
* [Crear un flujo de datos para una conexión de origen de éxito de cliente en la interfaz de usuario](../../tutorials/ui/dataflow/customer-success.md)
