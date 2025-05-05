---
title: Información general sobre el conector Source de Zendesk
description: Obtenga información sobre cómo conectar Zendesk a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# [!DNL Zendesk]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación de éxito de clientes de terceros. Los proveedores de éxito de clientes incluyen [!DNL Zendesk].

Este Adobe Experience Platform [sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=es) aprovecha [Zendesk Search API > Exportar resultados de búsqueda](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que devuelve información de usuarios a Experience Platform desde Zendesk para un procesamiento posterior.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Autenticar su cuenta de [!DNL Zendesk]

[!DNL Zendesk] usa tokens de portador como mecanismo de autenticación para comunicarse con la API [!DNL Zendesk].

Esta sección describe los pasos necesarios que se deben seguir para autenticar la cuenta de [!DNL Zendesk].

* El primer paso para autenticar su cuenta de [!DNL Zendesk] es asegurarse de que tiene la cuenta de soporte de [!DNL Zendesk]. Si todavía no tiene una, vea la [[!DNL Zendesk] página de registro](https://www.zendesk.com/register/) para registrarse y crear su cuenta de Zendesk.
* Una vez que se haya registrado correctamente, vaya al [[!DNL Zendesk] sitio web](https://www.zendesk.com/login/) y proporcione su **subdominio**.
* A continuación, seleccione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Finalmente, recupere su token de API de la sección **[!DNL API token]**.

![Token de API de Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) para obtener información sobre cómo recuperar el subdominio. Para obtener información sobre cómo generar el token de API, consulte la [[!DNL Zendesk] guía sobre cómo generar un nuevo token de API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

La siguiente documentación proporciona información sobre cómo conectar [!DNL Zendesk] a Experience Platform mediante API o la interfaz de usuario:

## Conectar [!DNL Zendesk] a Experience Platform mediante API

* [Cree una conexión de origen y un flujo de datos para [!DNL Zendesk] usando la API de Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Conectar [!DNL Zendesk] a Experience Platform mediante la interfaz de usuario

* [Crear una  [!DNL Zendesk &#x200B;]conexión de origen en la interfaz de usuario](../../tutorials/ui/create/customer-success/zendesk.md)
* [Crear un flujo de datos para una conexión de origen de éxito de cliente en la interfaz de usuario](../../tutorials/ui/dataflow/customer-success.md)
