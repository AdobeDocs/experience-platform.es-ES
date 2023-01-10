---
keywords: Experience Platform;inicio;temas populares;shopify;Shopify
solution: Experience Platform
title: Crear una conexión de origen de Shopify en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen Shopify mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Cree un [!DNL Shopify] conexión de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Shopify] conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene un [!DNL Shopify] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos para un conector de comercio electrónico](../../dataflow/ecommerce.md).

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Shopify] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El punto final del [!DNL Shopify] servidor. |
| `accessToken` | El token de acceso para su [!DNL Shopify] cuenta de usuario. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Conecte su [!DNL Shopify] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Shopify] cuenta para [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL comercio electrónico]** categoría, seleccione **[!UICONTROL Shopify]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un [!DNL Shopify] conector.

![catálogo](../../../../images/tutorials/create/shopify/catalog.png)

La variable **[!UICONTROL Conectarse a Shopify]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Shopify] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Shopify] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/shopify/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Shopify] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir los datos de comercio electrónico en [!DNL Platform]](../../dataflow/ecommerce.md).
