---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Google Ads en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc

---


# Creación de un conector de origen de Google Ads en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de Google Ads mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base de Google Ads, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a la plataforma de cuentas de Google Ads, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | ID de cliente de la cuenta de anuncios. |
| `developerToken` | El testigo del programador asociado a la cuenta del administrador. |
| `refreshToken` | El autentificador de actualización obtenido de Google para autorizar el acceso a los anuncios. |
| `clientId` | ID de cliente de la aplicación de Google utilizada para adquirir el autentificador de actualización. |
| `clientSecret` | El secreto de cliente de la aplicación de Google utilizado para adquirir el autentificador de actualización. |

Para obtener más información sobre cómo empezar, consulte este documento [de](https://developers.google.com/adwords/api/docs/guides/authentication)Google Ads.

## Conectar la cuenta de Google Ads

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular su cuenta de Google Ads a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo *Fuentes* . La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *Publicidad* , seleccione Publicidades de **Google** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para conectarse con la fuente o la vista de la misma. Para crear una nueva conexión base de entrada, seleccione Origen **de** Connect.

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

Aparece la página *Conectar con publicidades* de Google. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **Nueva cuenta**. En el formulario de entrada que aparece, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de Google Ads. Cuando termine, seleccione **Connect** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Google Ads con la que desee conectarse y, a continuación, seleccione **Siguiente** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base a su cuenta de Google Ads. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir datos de publicidad en Platform](../../dataflow/advertising.md).