---
keywords: Experience Platform;inicio;temas populares;onetrust;OneTrust
solution: Experience Platform
title: Crear una conexión de origen de OneTrust en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de OneTrust mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Crear un [!DNL OneTrust Integration] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL OneTrust Integration] La fuente solo admite la ingesta de datos de consentimiento y preferencias, y no cookies.

Este tutorial proporciona los pasos para crear una [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) conexión de origen para introducir datos de consentimiento históricos y programados en Adobe Experience Platform mediante la interfaz de usuario de Platform.

## Requisitos previos

>[!IMPORTANT]
>
>El [!DNL OneTrust Integration] el conector de origen y la documentación fueron creados por el [!DNL OneTrust Integration] equipo. Para cualquier consulta o solicitud de actualización, póngase en contacto con el [[!DNL OneTrust] equipo](https://my.onetrust.com/s/contactsupport?language=en_US) directamente.

Antes de conectarse [!DNL OneTrust Integration] En Platform, primero debe recuperar el token de acceso. Para obtener instrucciones detalladas sobre cómo encontrar el token de acceso, consulte la [[!DNL OneTrust Integration] Guía de OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

El token de acceso no se actualiza automáticamente una vez caducado porque no admite tokens de actualización de sistema a sistema [!DNL OneTrust]. Por lo tanto, es necesario asegurarse de que el token de acceso se actualice en la conexión antes de que caduque. La duración máxima configurable de un token de acceso es de un año. Para obtener más información sobre cómo actualizar el token de acceso, consulte la [[!DNL OneTrust] documento sobre la administración de las credenciales del cliente de OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Recopilar credenciales necesarias

Para poder conectarse [!DNL OneTrust Integration] En Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Nombre de host | El entorno desde el que se ejecuta la variable [!DNL OneTrust Integration] es necesario extraer los datos de. | `app.onetrust.com` |
| URL de prueba de autorización | (Opcional) La dirección URL de prueba de autorización se utiliza para validar credenciales al crear una conexión base. Si no se proporcionan, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |  |
| Token de acceso | El token de acceso que corresponde a su [!DNL OneTrust Integration] cuenta. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Para obtener más información sobre estas credenciales, consulte la [[!DNL OneTrust Integration] documentación de autenticación](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Conecte su [!DNL OneTrust Integration] account

>[!NOTE]
>
>El [!DNL OneTrust Integration] Las especificaciones de la API se comparten con el Adobe para la ingesta de datos.

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] espacio de trabajo para un catálogo de fuentes disponibles en Experience Platform.

Utilice el *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la [!UICONTROL Consentimiento y preferencias] categoría para [!DNL OneTrust Integration] tarjeta de origen. Para empezar, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de IU de Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

El **[!UICONTROL Conectar cuenta de integración de OneTrust]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL OneTrust Integration] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![El paso de autenticación de cuenta existente en el flujo de trabajo de fuentes.](../../../../images/tutorials/create/onetrust/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![El nuevo paso de autenticación de cuenta en el flujo de trabajo de fuentes.](../../../../images/tutorials/create/onetrust/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL OneTrust Integration] cuenta. Ahora puede continuar con el siguiente tutorial y [Configuración de un flujo de datos para introducir datos de consentimiento en Platform](../../dataflow/consent-and-preferences.md).
