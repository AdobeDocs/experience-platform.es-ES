---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: Creación de un conector de origen HubSpot en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen HubSpot mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Creación de un conector [!DNL HubSpot] de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL HubSpot] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de [!DNL HubSpot] origen mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL HubSpot] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

### Recopilar las credenciales necesarias

Para acceder a su [!DNL HubSpot] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | ID de cliente asociado a la [!DNL HubSpot] aplicación. |
| `clientSecret` | El secreto de cliente asociado a la [!DNL HubSpot] aplicación. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El autentificador de actualización obtenido al autenticar inicialmente la integración de OAuth. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL HubSpot] documento](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Conectar su [!DNL HubSpot] cuenta

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL HubSpot] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL de automatización]** de marketing, seleccione **[!UICONTROL HubSpot]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL HubSpot] conector.

![catálogo](../../../../images/tutorials/create/hubspot/catalog.png)

Aparece la página **[!UICONTROL Conectar con HubSpot]** . En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL HubSpot] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL HubSpot] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hubspot/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su [!DNL HubSpot] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar [!DNL Platform]](../../dataflow/marketing-automation.md)datos del sistema de automatización de marketing.