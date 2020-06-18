---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen HubSpot en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# Creación de un conector de origen HubSpot en la interfaz de usuario

> [!NOTE]
> El conector HubSpot está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen HubSpot mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes del Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base de HubSpot, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/marketing-automation.md)de automatización de marketing.

### Recopilar las credenciales necesarias

Para acceder a su cuenta de HubSpot en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | ID de cliente asociado a la aplicación HubSpot. |
| `clientSecret` | El secreto de cliente asociado a la aplicación HubSpot. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |

Para obtener más información sobre cómo empezar, consulte este documento [de HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Conectar la cuenta de HubSpot

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular su cuenta de HubSpot a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría de automatización *de* marketing, seleccione **HubSpot** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **de** Connect.

![catálogo](../../../../images/tutorials/create/hubspot/catalog.png)

Aparece la página *Conectar con HubSpot* . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de HubSpot. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de HubSpot con la que desea conectarse y, a continuación, seleccione **Siguiente** para continuar.

![existente](../../../../images/tutorials/create/hubspot/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base a su cuenta de HubSpot. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar datos del sistema de automatización de marketing a Platform](../../dataflow/marketing-automation.md).