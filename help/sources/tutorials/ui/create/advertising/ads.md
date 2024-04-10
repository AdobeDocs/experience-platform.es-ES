---
title: Crear una conexión de origen de Google Ads en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Crear una conexión de origen de Google Ads en la interfaz de usuario

>[!WARNING]
>
>El [!DNL Google Ads] el origen no está disponible temporalmente. El Adobe está trabajando para resolver los problemas con esta fuente.

>[!NOTE]
>
>La fuente de Google Ads está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una conexión de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de Google Ads válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/advertising.md)

### Recopilar credenciales necesarias

Para acceder a la plataforma de cuenta de Google Ads, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de cliente | El ID de cliente es el número de cuenta que corresponde a la cuenta de cliente de Google Ads que desea administrar con la API de Google Ads. Este ID sigue la plantilla de `123-456-7890`. |
| ID de cliente de inicio de sesión | El ID de cliente de inicio de sesión es el número de cuenta que corresponde a su cuenta de administrador de Google Ads y se utiliza para recuperar datos de informe de un cliente operativo específico. Para obtener más información sobre el ID de cliente de inicio de sesión, lea la [Documentación de la API de Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Token de desarrollador | El token de desarrollador le permite acceder a la API de Google Ads. Puede utilizar el mismo token de desarrollador para realizar solicitudes en todas las cuentas de Google Ads. Recuperar el token de desarrollador de [inicio de sesión en su cuenta de manager](https://ads.google.com/home/tools/manager-accounts/) y, a continuación, vaya a la página Centro de API. |
| Actualizar token | El token de actualización forma parte de [!DNL OAuth2] autenticación. Este token le permite volver a generar los tokens de acceso una vez caducados. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de [!DNL OAuth2] autenticación. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |
| Secreto de cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de [!DNL OAuth2] autenticación. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |

Lea el documento de información general de API para [más información sobre cómo empezar a usar Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conecte su cuenta de Google Ads

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Publicidad]** categoría, seleccionar **[!UICONTROL Google Ads]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes en la interfaz de usuario de Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

El **[!UICONTROL Conectar con Google Ads]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de Google Ads con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La página de selección de cuentas existentes en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/ads/existing.png).

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Google Ads. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/ads/new.png).

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Google Ads. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos publicitarios en Platform](../../dataflow/advertising.md).
