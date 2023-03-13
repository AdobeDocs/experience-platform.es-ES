---
keywords: Experience Platform;inicio;temas populares;API REST genérica
title: Crear una conexión de origen API REST genérica en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de API REST genérica mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Crear un [!DNL Generic REST API] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Generic REST API] el origen está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Este tutorial proporciona los pasos para crear una [!DNL Generic REST API] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Generic REST API] en Platform, debe proporcionar credenciales válidas para el tipo de autenticación que elija. La API REST genérica admite código de actualización OAuth 2 y autenticación básica. Consulte las siguientes tablas para obtener información sobre las credenciales de los dos tipos de autenticación admitidos.

#### Código de actualización de OAuth 2

| Credencial | Descripción |
| --- | --- |
| Host | La URL de host de la fuente a la que realiza la solicitud. Este valor es obligatorio y no se puede omitir usando la anulación de parámetros de solicitud. |
| URL de prueba de autorización | (Opcional) La dirección URL de prueba de autorización se utiliza para validar credenciales al crear una conexión base. Si no se proporcionan, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| ID del cliente | (Opcional) El ID de cliente asociado con su cuenta de usuario. |
| Secreto de cliente | (Opcional) Secreto de cliente asociado a su cuenta de usuario. |
| Token de acceso | Credencial de autenticación principal utilizada para acceder a la aplicación. El token de acceso representa la autorización de la aplicación para acceder a determinados aspectos de los datos de un usuario. Este valor es obligatorio y no se puede omitir usando la anulación de parámetros de solicitud. |
| Actualizar token | (Opcional) Un token que se usa para generar un nuevo token de acceso cuando el token de acceso ha caducado. |
| URL de token de acceso | (Opcional) Punto final de URL utilizado para recuperar el token de acceso. |
| Solicitar anulación de parámetros | (Opcional) Una propiedad que le permite especificar qué parámetros de credencial se van a anular. |


#### Autenticación básica

| Credencial | Descripción |
| --- | --- |
| Host | La URL de host de la fuente a la que realiza la solicitud. |
| Nombre de usuario | El nombre de usuario que corresponde con su cuenta de usuario. |
| Una contraseña | La contraseña que corresponde a su cuenta de usuario. |

## Conecte su cuenta de API de REST genérica

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Protocolos] categoría, seleccionar **[!UICONTROL API REST genérica]** y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/generic-rest/catalog.png)

El **[!UICONTROL Conectar con la API REST genérica]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de API REST genérica con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/generic-rest/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción de opción para la nueva [!DNL Generic REST API] cuenta.

![nuevo](../../../../images/tutorials/create/generic-rest/new.png)

#### Autenticar con el código de actualización de OAuth 2

[!DNL Generic REST API] admite código de actualización OAuth 2 y autenticación básica. Para autenticarse con una autenticación OAuth2, seleccione **[!UICONTROL OAuth2RefreshCode]**, proporcione las credenciales de OAuth 2 y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autenticar con autenticación básica

Para utilizar la autenticación básica, seleccione **[!UICONTROL Autenticación básica]**, proporcione su host, nombre de usuario y contraseña y, a continuación, seleccione **[!UICONTROL Conectar con el origen]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de API de REST genérica. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/protocols.md).
