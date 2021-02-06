---
keywords: Experience Platform;inicio;temas populares;Google AdWords;Google AdWords conector de origen;Google AdWords conector;Google adwords
solution: Experience Platform
title: Creación de una conexión de origen de Google AdWords en la interfaz de usuario
topic: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen Google AdWords mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Crear una conexión de origen [!DNL Google AdWords] en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Google AdWords] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google AdWords] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Google AdWords] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL Google AdWords] [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | ID de cliente de la cuenta [!DNL AdWords]. |
| `developerToken` | El testigo del programador asociado a la cuenta del administrador. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] para autorizar el acceso a [!DNL AdWords]. |
| `clientId` | ID de cliente de la aplicación [!DNL Google] utilizada para adquirir el autentificador de actualización. |
| `clientSecret` | El secreto de cliente de la aplicación [!DNL Google] utilizada para adquirir el autentificador de actualización. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Conectar su cuenta [!DNL Google AdWords]

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta [!DNL Google AdWords] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Publicidad]**, seleccione **[!UICONTROL Google AdWords]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector [!DNL Google AdWords].

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

Aparece la página **[!UICONTROL Conectar con Google AdWords]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales [!DNL Google AdWords]. Cuando termine, seleccione **[!UICONTROL Conectar]** y, a continuación, deje transcurrir algún tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Google AdWords] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta [!DNL Google AdWords]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de publicidad a [!DNL Platform]](../../dataflow/advertising.md).