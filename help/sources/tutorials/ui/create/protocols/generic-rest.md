---
keywords: Experience Platform;inicio;temas populares;API genérica de REST
title: Crear una conexión de origen de API de REST genérica en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de API de REST genérica mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Cree un [!DNL Generic REST API] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> La variable [!DNL Generic REST API] el origen está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial proporciona los pasos para crear un [!DNL Generic REST API] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Generic REST API] en Platform, debe proporcionar credenciales válidas para el tipo de autenticación que elija. La API genérica de REST es compatible tanto con el código de actualización de OAuth 2 como con la autenticación básica. Consulte las siguientes tablas para obtener información sobre las credenciales de los dos tipos de autenticación admitidos.

#### Código de actualización de OAuth 2

| Credencial | Descripción |
| --- | --- |
| Host | La dirección URL de host de la fuente a la que realiza la solicitud. Este valor es obligatorio y no se puede evitar utilizando la anulación de parámetros de solicitud. |
| URL de prueba de autorización | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| ID del cliente | (Opcional) El ID de cliente asociado a su cuenta de usuario. |
| Secreto de cliente | (Opcional) El secreto de cliente asociado a su cuenta de usuario. |
| Token de acceso | La credencial de autenticación principal utilizada para acceder a su aplicación. El token de acceso representa la autorización de la aplicación para acceder a aspectos concretos de los datos de un usuario. Este valor es obligatorio y no se puede evitar utilizando la anulación de parámetros de solicitud. |
| Actualizar token | (Opcional) Token que se utiliza para generar un nuevo token de acceso cuando el token de acceso ha caducado. |
| Acceso a la dirección URL del token | (Opcional) El extremo URL utilizado para recuperar el token de acceso. |
| Anulación de parámetros de solicitud | (Opcional) Una propiedad que le permite especificar qué parámetros de credencial desea anular. |


#### Autenticación básica

| Credencial | Descripción |
| --- | --- |
| Host | La dirección URL de host de la fuente a la que realiza la solicitud. |
| Nombre de usuario | El nombre de usuario que corresponde a su cuenta de usuario. |
| Contraseña | La contraseña que corresponde a su cuenta de usuario. |

## Conecte la cuenta de API de REST genérica

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Protocolos] categoría, seleccione **[!UICONTROL API de REST genérica]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/generic-rest/catalog.png)

La variable **[!UICONTROL Conectarse a la API de REST genérica]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de API de REST genérica con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/generic-rest/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción de la opción para la nueva [!DNL Generic REST API] cuenta.

![new](../../../../images/tutorials/create/generic-rest/new.png)

#### Autenticar mediante el código de actualización de OAuth 2

[!DNL Generic REST API] admite tanto el código de actualización de OAuth 2 como la autenticación básica. Para autenticarse con una autenticación OAuth2, seleccione **[!UICONTROL OAuth2RefreshCode]**, proporcione sus credenciales de OAuth 2 y, a continuación, seleccione **[!UICONTROL Conectar a origen]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autenticar mediante autenticación básica

Para utilizar la autenticación básica, seleccione **[!UICONTROL Autenticación básica]**, proporcione el host, el nombre de usuario y la contraseña y, a continuación, seleccione **[!UICONTROL Conectar a origen]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de API de REST genérica. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/protocols.md).
