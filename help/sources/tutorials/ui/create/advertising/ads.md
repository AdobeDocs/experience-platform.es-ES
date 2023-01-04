---
keywords: Experience Platform;inicio;temas populares;Google Ads;Conector de origen de Google Ads;Conector de anuncios de google
title: Crear una conexión de origen de Google Ads en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# Crear una conexión de origen de Google Ads en la interfaz de usuario

>[!NOTE]
>
>La fuente de Google Ads está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Este tutorial proporciona los pasos para crear un conector de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida a Google Ads, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/advertising.md)

### Recopilar las credenciales necesarias

Para acceder a la plataforma de cuenta de Google Ads, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de cliente del cliente | El ID de cliente es el número de cuenta que corresponde a la cuenta de cliente de Google Ads que desea administrar con la API de Google Ads. Este ID sigue la plantilla de `123-456-7890`. |
| Token de desarrollador | El token de desarrollador le permite acceder a la API de Google Ads. Puede utilizar el mismo token de desarrollador para realizar solicitudes en todas sus cuentas de Google Ads. Recupere el token del desarrollador mediante [iniciar sesión en la cuenta de administrador](https://ads.google.com/home/tools/manager-accounts/) y, a continuación, vaya a la página Centro de API . |
| Actualizar token | El token de actualización forma parte de [!DNL OAuth2] autenticación. Este token le permite volver a generar los tokens de acceso una vez caducados. |
| ID del cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de [!DNL OAuth2] autenticación. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |
| Secreto de cliente | El secreto de cliente se utiliza en combinación con el ID de cliente como parte de [!DNL OAuth2] autenticación. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |

Lea el documento de información general de API para [más información sobre cómo empezar a usar Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conecte la cuenta de Google Ads

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL Publicidad]** categoría, seleccione **[!UICONTROL Publicidades de Google]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![Una imagen de la fuente de Google Ads en el catálogo de fuentes de la interfaz de usuario del Experience Platform](../../../../images/tutorials/create/ads/catalog.png).

La variable **[!UICONTROL Conexión a Google Ads]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Google Ads con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Imagen de una lista de cuentas existentes que puede utilizar para crear un flujo de datos de Google Ads con](../../../../images/tutorials/create/ads/existing.png).

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y las credenciales de Google Ads. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![Imagen de la nueva pantalla de conexión de la cuenta en la interfaz de usuario del Experience Platform](../../../../images/tutorials/create/ads/connect.png).

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de Google Ads. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos publicitarios a Platform](../../dataflow/advertising.md).
