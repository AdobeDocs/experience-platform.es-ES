---
keywords: Experience Platform;inicio;temas populares;onetrust;OneTrust
solution: Experience Platform
title: (Beta) Crear una conexión de origen de OneTrust en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de OneTrust mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# (Beta) Cree un [!DNL OneTrust Integration] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>La variable [!DNL OneTrust Integration] el origen está en versión beta. Sus características y documentación están sujetas a cambios. Para obtener información sobre el uso de fuentes con etiqueta beta, consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions).

Este tutorial proporciona los pasos para crear un [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) conexión de origen para introducir datos de consentimiento históricos y programados en Adobe Experience Platform mediante la interfaz de usuario de Platform.

## Requisitos previos

>[!IMPORTANT]
>
>La variable [!DNL OneTrust Integration] el conector de origen y la documentación fueron creados por el [!DNL OneTrust Integration] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con el [[!DNL OneTrust] equipo](https://my.onetrust.com/s/contactsupport?language=en_US) directamente.

Antes de conectarse [!DNL OneTrust Integration] en Platform, primero debe recuperar el token de acceso. Para obtener instrucciones detalladas sobre cómo encontrar el token de acceso, consulte la [[!DNL OneTrust Integration] Guía de OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

El token de acceso no se actualiza automáticamente una vez caducado porque los tokens de actualización de sistema a sistema no son compatibles con [!DNL OneTrust]. Por lo tanto, es necesario asegurarse de que el token de acceso se actualiza en la conexión antes de que caduque. La duración máxima configurable para un token de acceso es de un año. Para obtener más información sobre la actualización del token de acceso, consulte la [[!DNL OneTrust] documento sobre la administración de las credenciales de cliente de OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Recopilar las credenciales necesarias

Para conectarse [!DNL OneTrust Integration] a Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Nombre del host | El entorno desde el que se puede [!DNL OneTrust Integration] los datos deben extraerse de . | `https://uat.onetrust.com/` |
| URL de prueba de autorización | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |  |
| Token de acceso | El token de acceso que corresponde a su [!DNL OneTrust Integration] cuenta. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obtener más información sobre estas credenciales, consulte la [[!DNL OneTrust Integration] documentación de autenticación](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conecte su [!DNL OneTrust Integration] account

>[!NOTE]
>
>La variable [!DNL OneTrust Integration] Las especificaciones de API se están compartiendo con Adobe para la ingesta de datos.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el *[!UICONTROL Consentimiento y preferencias]* categoría, seleccione [!DNL OneTrust Integration]y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/onetrust/catalog.png)

La variable **[!UICONTROL Conectar la cuenta de integración de OneTrust]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL OneTrust Integration] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/onetrust/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/onetrust/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL OneTrust Integration] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de consentimiento en Platform](../../dataflow/consent-and-preferences.md).
