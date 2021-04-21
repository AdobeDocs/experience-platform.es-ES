---
keywords: Experience Platform;inicio;temas populares;Google AdWords;conector fuente de Google AdWords;conector de Google AdWords
solution: Experience Platform
title: Crear una conexión de origen de Google AdWords en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Google AdWords mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Google AdWords] en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Google AdWords] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google AdWords] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Google AdWords] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Google AdWords] cuenta [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | El ID de cliente de la cuenta [!DNL AdWords]. |
| `developerToken` | El token de desarrollador asociado a la cuenta de administrador. |
| `refreshToken` | Token de actualización obtenido de [!DNL Google] para autorizar el acceso a [!DNL AdWords]. |
| `clientId` | El ID de cliente de la aplicación [!DNL Google] utilizada para adquirir el token de actualización. |
| `clientSecret` | El secreto de cliente de la aplicación [!DNL Google] utilizada para adquirir el token de actualización. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Conecte su cuenta [!DNL Google AdWords]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Google AdWords] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Advertising]**, seleccione **[!UICONTROL Google AdWords]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Google AdWords].

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

Aparece la página **[!UICONTROL Connect to Google AdWords]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Google AdWords]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Google AdWords] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Google AdWords]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos publicitarios en [!DNL Platform]](../../dataflow/advertising.md).
