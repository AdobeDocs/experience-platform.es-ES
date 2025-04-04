---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
solution: Experience Platform
title: Crear una conexión de origen de MailChimp Campaigns mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar Adobe Experience Platform a campañas de MailChimp mediante la interfaz de usuario de Experience Platform.
exl-id: e8e1ed32-4277-44c9-aafc-6bb9e0a1fe0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 4%

---

# Crear una conexión de origen [!DNL Mailchimp Campaigns] mediante la interfaz de usuario de Experience Platform

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Mailchimp] para la ingesta de datos de [!DNL Mailchimp Campaigns] en Adobe Experience Platform mediante la interfaz de usuario.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Recopilar credenciales necesarias

Para poder llevar los datos de [!DNL Mailchimp Campaigns] a Experience Platform, primero debe proporcionar las credenciales de autenticación adecuadas que se correspondan con la cuenta de [!DNL Mailchimp].

El origen [!DNL Mailchimp Campaigns] admite código de actualización OAuth 2 y autenticación básica. Consulte las tablas siguientes para obtener más información sobre estos tipos de autenticación.

### Código de actualización de OAuth 2

| Credenciales | Descripción |
| --- | --- |
| Dominio | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| URL de prueba de autorización | La dirección URL de prueba de autorización se usa para validar credenciales al conectar [!DNL Mailchimp] a Experience Platform. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| Token de acceso | El token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

Para obtener más información sobre el uso de OAuth 2 para autenticar su cuenta de [!DNL Mailchimp] en Experience Platform, consulte este [[!DNL Mailchimp] documento sobre el uso de OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticación básica

| Credenciales | Descripción |
| --- | --- |
| Dominio | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| Nombre de usuario | El nombre de usuario que corresponde con su cuenta de MailChimp. Esto es necesario para la autenticación básica. |
| Contraseña | La contraseña que corresponde a su cuenta de MailChimp. Esto es necesario para la autenticación básica. |

## Conecte su cuenta de [!DNL Mailchimp Campaigns] a Experience Platform

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Automatización de marketing], selecciona **[!UICONTROL Campaña de Mailchimp]** y, a continuación, selecciona **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/mailchimp-campaigns/catalog.png)

Aparecerá la página **[!UICONTROL Conectar la cuenta de campañas de Mailchimp]**. En esta página, puede seleccionar si está accediendo a una cuenta existente u optando por crear una nueva cuenta.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Mailchimp Campaigns] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/mailchimp-campaigns/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción para los detalles de conexión de origen de [!DNL Mailchimp Campaigns].

![nuevo](../../../../images/tutorials/create/mailchimp-campaigns/new.png)

#### Autenticar con OAuth 2

Para usar OAuth 2, seleccione [!UICONTROL Código de actualización de OAuth 2], proporcione valores para su dominio, URL de prueba de autorización y token de acceso y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![oauth](../../../../images/tutorials/create/mailchimp-campaigns/oauth.png)

#### Autenticar con autenticación básica

Para usar la autenticación básica, selecciona [!UICONTROL Autenticación básica], proporciona valores para tu dominio, nombre de usuario y contraseña y, a continuación, selecciona **[!UICONTROL Conectar con el origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![básico](../../../../images/tutorials/create/mailchimp-campaigns/basic.png)

### Seleccionar [!DNL Mailchimp Campaigns] datos

Una vez autenticado el origen, debe proporcionar `campaignId` que corresponda a su cuenta de [!DNL Mailchimp Campaigns].

En la página [!UICONTROL Seleccionar datos], escriba su `campaignId` y, a continuación, seleccione **[!UICONTROL Explorar]**.

![explorar](../../../../images/tutorials/create/mailchimp-campaigns/explore.png)

La página se actualiza en un árbol de esquema interactivo que le permite explorar e inspeccionar la jerarquía de los datos. Seleccione **[!UICONTROL Siguiente]** para continuar.

![select-data](../../../../images/tutorials/create/mailchimp-campaigns/select-data.png)

## Pasos siguientes

Con la cuenta de [!DNL Mailchimp] autenticada y los datos de [!DNL Mailchimp Campaigns] seleccionados, ahora puede empezar a crear un flujo de datos para llevar los datos a Experience Platform. Para ver los pasos detallados sobre cómo crear un flujo de datos, consulte la documentación de [creación de un flujo de datos para llevar los datos de automatización de marketing a Experience Platform](../../dataflow/marketing-automation.md).
