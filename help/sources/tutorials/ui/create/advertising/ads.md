---
title: Creación de una conexión de Source de Google Ads en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# Crear una conexión de origen de Google Ads en la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Google Ads] no está disponible temporalmente. El Adobe está trabajando para resolver los problemas con esta fuente.

>[!NOTE]
>
>La fuente de Google Ads está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre cómo usar fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una conexión de origen de Google Ads mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de Google Ads válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/advertising.md)

### Recopilar credenciales necesarias

Para acceder a la plataforma de cuenta de Google Ads, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de cliente | El ID de cliente es el número de cuenta que corresponde a la cuenta de cliente de Google Ads que desea administrar con la API de Google Ads. Este identificador sigue la plantilla de `123-456-7890`. |
| ID de cliente de inicio de sesión | El ID de cliente de inicio de sesión es el número de cuenta que corresponde a su cuenta de administrador de Google Ads y se utiliza para recuperar datos de informe de un cliente operativo específico. Para obtener más información sobre el identificador de cliente de inicio de sesión, lea la [Documentación de la API de Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Token de desarrollador | El token de desarrollador le permite acceder a la API de Google Ads. Puede utilizar el mismo token de desarrollador para realizar solicitudes en todas las cuentas de Google Ads. Recupere su token de desarrollador al [iniciar sesión en su cuenta de administrador](https://ads.google.com/home/tools/manager-accounts/) y luego navegar a la página del Centro de API. |
| Actualizar token | El token de actualización forma parte de la autenticación [!DNL OAuth2]. Este token le permite volver a generar los tokens de acceso una vez caducados. |
| ID de cliente | El ID de cliente se usa junto con el secreto de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |
| Secreto del cliente | El secreto de cliente se usa junto con el ID de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |

Lea el documento de información general de la API para [obtener más información sobre cómo empezar a usar Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Conecte su cuenta de Google Ads

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Advertising]**, seleccione **[!UICONTROL Google Ads]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes en la interfaz de usuario del Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

Aparecerá la página **[!UICONTROL Conectar con Google Ads]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de Google Ads con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** para continuar.

![Página de selección de cuentas existentes en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/ads/existing.png).

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y las credenciales de Google Ads. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/ads/new.png).

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de Google Ads. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para llevar datos publicitarios a la plataforma](../../dataflow/advertising.md).
