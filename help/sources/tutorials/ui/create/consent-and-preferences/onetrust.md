---
keywords: Experience Platform;inicio;temas populares;onetrust;OneTrust
solution: Experience Platform
title: Crear una conexión de OneTrust Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de OneTrust mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL OneTrust Integration] en la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL OneTrust Integration] solo admite la ingesta de datos de preferencias y consentimiento, no de cookies.

Este tutorial proporciona los pasos para crear una conexión de origen [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) para introducir datos de consentimiento históricos y programados en Adobe Experience Platform mediante la interfaz de usuario de Experience Platform.

## Requisitos previos

>[!IMPORTANT]
>
>El conector de origen y la documentación de [!DNL OneTrust Integration] fueron creados por el equipo de [!DNL OneTrust Integration]. Para cualquier consulta o solicitud de actualización, comuníquese directamente con el [[!DNL OneTrust] equipo](https://my.onetrust.com/s/contactsupport?language=en_US).

Para poder conectar [!DNL OneTrust Integration] a Experience Platform, primero debe recuperar el token de acceso. Para obtener instrucciones detalladas sobre cómo encontrar el token de acceso, consulte la [[!DNL OneTrust Integration] guía de OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

El token de acceso no se actualiza automáticamente una vez que caduca porque [!DNL OneTrust] no admite tokens de actualización de sistema a sistema. Por lo tanto, es necesario asegurarse de que el token de acceso se actualice en la conexión antes de que caduque. La duración máxima configurable de un token de acceso es de un año. Para obtener más información sobre cómo actualizar el token de acceso, consulte el [[!DNL OneTrust] documento sobre la administración de las credenciales de cliente de OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Recopilar credenciales necesarias

Para conectar [!DNL OneTrust Integration] a Experience Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Nombre de host | Entorno del cual se deben extraer los datos de [!DNL OneTrust Integration]. | `app.onetrust.com` |
| URL de prueba de autorización | (Opcional) La dirección URL de prueba de autorización se utiliza para validar credenciales al crear una conexión base. Si no se proporcionan, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. | |
| Token de acceso | El token de acceso que corresponde a su cuenta de [!DNL OneTrust Integration]. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obtener más información sobre estas credenciales, consulte la [[!DNL OneTrust Integration] documentación de autenticación](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conectar su cuenta de [!DNL OneTrust Integration]

>[!NOTE]
>
>Las especificaciones de la API [!DNL OneTrust Integration] se están compartiendo con Adobe para la ingesta de datos.

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources] para obtener un catálogo de orígenes disponibles en Experience Platform.

Utilice el menú *[!UICONTROL Categorías]* para filtrar orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la categoría [!UICONTROL Consentimiento y preferencias] para la tarjeta de origen [!DNL OneTrust Integration]. Para empezar, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes de IU de Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de integración de OneTrust]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL OneTrust Integration] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso de autenticación de cuenta existente en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/onetrust/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![El nuevo paso de autenticación de cuenta en el flujo de trabajo de orígenes.](../../../../images/tutorials/create/onetrust/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL OneTrust Integration]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de consentimiento en Experience Platform](../../dataflow/consent-and-preferences.md).
