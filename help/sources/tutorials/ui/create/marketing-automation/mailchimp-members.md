---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Crear una conexión de origen de miembros de MailChimp mediante la IU de Platform
description: Aprenda a conectar Adobe Experience Platform con los miembros de MailChimp mediante la IU de Platform.
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 4%

---

# Crear una conexión de origen [!DNL Mailchimp Members] mediante la interfaz de usuario de Platform

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Mailchimp] para la ingesta de datos de [!DNL Mailchimp Members] en Adobe Experience Platform mediante la interfaz de usuario.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Recopilar credenciales necesarias

Para poder llevar los datos de [!DNL Mailchimp Members] a Platform, primero debe proporcionar las credenciales de autenticación adecuadas que se correspondan con la cuenta de [!DNL Mailchimp].

El origen [!DNL Mailchimp Members] admite código de actualización OAuth 2 y autenticación básica. Consulte las tablas siguientes para obtener más información sobre estos tipos de autenticación.

### Código de actualización de OAuth 2

| Credenciales | Descripción |
| --- | --- |
| Dominio | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| URL de prueba de autorización | La dirección URL de prueba de autorización se usa para validar credenciales al conectar [!DNL Mailchimp] a Platform. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| Token de acceso | El token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

Para obtener más información sobre el uso de OAuth 2 para autenticar su cuenta de [!DNL Mailchimp] en Platform, consulte este [[!DNL Mailchimp] documento sobre el uso de OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticación básica

| Credenciales | Descripción |
| --- | --- |
| Dominio | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| Nombre de usuario | El nombre de usuario que corresponde con su cuenta de MailChimp. Esto es necesario para la autenticación básica. |
| Contraseña | La contraseña que corresponde a su cuenta de MailChimp. Esto es necesario para la autenticación básica. |

## Conectar su cuenta de [!DNL Mailchimp Members] a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Automatización de marketing], selecciona **[!UICONTROL Campaña de Mailchimp]** y, a continuación, selecciona **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/mailchimp-members/catalog.png)

Aparecerá la página **[!UICONTROL Conectar la cuenta de campañas de Mailchimp]**. En esta página, puede seleccionar si está accediendo a una cuenta existente u optando por crear una nueva cuenta.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Mailchimp Members] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/mailchimp-members/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción para los detalles de conexión de origen de [!DNL Mailchimp Members].

![nuevo](../../../../images/tutorials/create/mailchimp-members/new.png)


#### Autenticar con OAuth 2

Para usar OAuth 2, seleccione [!UICONTROL Código de actualización de OAuth 2], proporcione valores para su dominio, URL de prueba de autorización y token de acceso y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![oauth](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### Autenticar con autenticación básica

Para usar la autenticación básica, selecciona [!UICONTROL Autenticación básica], proporciona valores para tu dominio, nombre de usuario y contraseña y, a continuación, selecciona **[!UICONTROL Conectar con el origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![básico](../../../../images/tutorials/create/mailchimp-members/basic.png)

### Seleccionar [!DNL Mailchimp Members] datos

Una vez autenticado el origen, debe proporcionar `listId` que corresponda a su cuenta de [!DNL Mailchimp Members].

En la página [!UICONTROL Seleccionar datos], escriba su `listId` y, a continuación, seleccione **[!UICONTROL Explorar]**.

![explorar](../../../../images/tutorials/create/mailchimp-members/explore.png)

La página se actualiza en un árbol de esquema interactivo que le permite explorar e inspeccionar la jerarquía de los datos. Seleccione **[!UICONTROL Siguiente]** para continuar.

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## Pasos siguientes

Con la cuenta [!DNL Mailchimp] autenticada y los datos [!DNL Mailchimp Members] seleccionados, ahora puede empezar a crear un flujo de datos para llevar los datos a Platform. Para ver los pasos detallados sobre cómo crear un flujo de datos, consulte la documentación de [creación de un flujo de datos para llevar los datos de automatización de marketing a la plataforma](../../dataflow/marketing-automation.md).
