---
keywords: Experience Platform;home;popular topics;Google AdWords;Google AdWords source connector;google adwords connector
solution: Experience Platform
title: Creación de un conector de origen de Google AdWords en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen Google AdWords mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# Creación de un conector [!DNL Google AdWords] de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Google AdWords] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL Google AdWords] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL Google AdWords] [configuración de un flujo de datos](../../dataflow/payments.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Google AdWords] cuenta [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | ID de cliente de la [!DNL AdWords] cuenta. |
| `developerToken` | El testigo del programador asociado a la cuenta del administrador. |
| `refreshToken` | Distintivo de actualización obtenido de [!DNL Google] para autorizar el acceso a [!DNL AdWords]. |
| `clientId` | El ID de cliente de la [!DNL Google] aplicación utilizada para adquirir el autentificador de actualización. |
| `clientSecret` | El secreto de cliente de la [!DNL Google] aplicación que se utiliza para adquirir el autentificador de actualización. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Conectar su [!DNL Google AdWords] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Google AdWords] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Publicidad]** , seleccione **[!UICONTROL Google AdWords]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL Google AdWords] conector.

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

Aparece la página **[!UICONTROL Conectar con Google AdWords]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL Google AdWords] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Google AdWords] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL Google AdWords] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir [!DNL Platform]](../../dataflow/advertising.md)datos de publicidad.