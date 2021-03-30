---
keywords: Experience Platform;inicio;temas populares;shopify;Shopify
solution: Experience Platform
title: Crear una conexión de origen de Shopify en la interfaz de usuario
topic: sobre validación
type: Tutorial
description: Aprenda a crear una conexión de origen Shopify mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Shopify] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Shopify] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Shopify], puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos para un conector de comercio electrónico](../../dataflow/ecommerce.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL Shopify] en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El punto final del servidor [!DNL Shopify]. |
| `accessToken` | El token de acceso de su cuenta de usuario [!DNL Shopify]. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conecte su cuenta [!DNL Shopify]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Shopify] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL eCommerce]**, seleccione **[!UICONTROL Shopify]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Shopify].

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

Aparece la página **[!UICONTROL Connect to Shopify]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Shopify]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Shopify] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Shopify]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir los datos de comercio electrónico en [!DNL Platform]](../../dataflow/ecommerce.md).