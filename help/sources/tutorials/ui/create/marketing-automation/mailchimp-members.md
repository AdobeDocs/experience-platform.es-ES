---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Creación de una conexión de origen de miembros de MailChimp mediante la interfaz de usuario de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a miembros de MailChimp mediante la interfaz de usuario de Platform.
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Cree un [!DNL Mailchimp Members] conexión de origen mediante la interfaz de usuario de Platform

Este tutorial proporciona los pasos para crear un [!DNL Mailchimp] conector de origen a ingesta [!DNL Mailchimp Members] datos a Adobe Experience Platform mediante la interfaz de usuario.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Recopilar las credenciales necesarias

Para traer su [!DNL Mailchimp Members] datos a Platform, primero debe proporcionar las credenciales de autenticación adecuadas que se correspondan con su [!DNL Mailchimp] cuenta.

La variable [!DNL Mailchimp Members] source es compatible tanto con el código de actualización de OAuth 2 como con la autenticación básica. Consulte las tablas siguientes para obtener más información sobre estos tipos de autenticación.

### Código de actualización de OAuth 2

| Credenciales | Descripción |
| --- | --- |
| Domain | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la dirección URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| URL de prueba de autorización | La URL de prueba de autorización se utiliza para validar las credenciales al conectar [!DNL Mailchimp] a Platform. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| Token de acceso | Token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

Para obtener más información sobre el uso de OAuth 2 para autenticar su [!DNL Mailchimp] a Platform, consulte esta [[!DNL Mailchimp] documento sobre el uso de OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Autenticación básica

| Credenciales | Descripción |
| --- | --- |
| Domain | La URL raíz utilizada para conectarse a la API de MailChimp. El formato de la dirección URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| Nombre de usuario | El nombre de usuario que corresponde a su cuenta de MailChimp. Esto es necesario para la autenticación básica. |
| Contraseña | La contraseña que corresponde a su cuenta de MailChimp. Esto es necesario para la autenticación básica. |

## Conecte su [!DNL Mailchimp Members] cuenta a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Automatización de marketing] categoría, seleccione **[!UICONTROL Campaña Mailchimp]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/mailchimp-members/catalog.png)

La variable **[!UICONTROL Conectar la cuenta de Campañas Mailchimp]** se abre. En esta página, puede seleccionar si accede a una cuenta existente o si decide crear una nueva.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Mailchimp Members] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/mailchimp-members/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción para su [!DNL Mailchimp Members] detalles de conexión de origen.

![new](../../../../images/tutorials/create/mailchimp-members/new.png)


#### Autenticar con OAuth 2

Para utilizar OAuth 2, seleccione [!UICONTROL Código de actualización de OAuth 2], proporcione valores para su dominio, la URL de prueba de autorización, el token de acceso y, a continuación, seleccione **[!UICONTROL Conectar a origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![oauth](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### Autenticar mediante autenticación básica

Para utilizar la autenticación básica, seleccione [!UICONTROL Autenticación básica], proporcione valores para su dominio, nombre de usuario y contraseña, y luego seleccione **[!UICONTROL Conectar a origen]**. Espere unos momentos para que sus credenciales se validen y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![basic](../../../../images/tutorials/create/mailchimp-members/basic.png)

### Select [!DNL Mailchimp Members] data

Una vez autenticado el origen, debe proporcionar la variable `listId` que corresponde a su [!DNL Mailchimp Members] cuenta.

En el [!UICONTROL Seleccionar datos] , introduzca su `listId` y, a continuación, seleccione **[!UICONTROL Explorar]**.

![explorar](../../../../images/tutorials/create/mailchimp-members/explore.png)

La página se actualiza en un árbol de esquema interactivo que le permite explorar e inspeccionar la jerarquía de los datos. Select **[!UICONTROL Siguiente]** para continuar.

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## Pasos siguientes

Con [!DNL Mailchimp] cuenta autenticada y su [!DNL Mailchimp Members] datos seleccionados, ahora puede empezar a crear un flujo de datos para llevar los datos a Platform. Para ver los pasos detallados sobre cómo crear un flujo de datos, consulte la documentación de [creación de un flujo de datos para traer datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
