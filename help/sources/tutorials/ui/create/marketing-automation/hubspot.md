---
keywords: Experience Platform;inicio;temas populares;hubspot;hubspot
solution: Experience Platform
title: Crear una conexión de origen de HubSpot en la interfaz de usuario de
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de HubSpot mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Crear un [!DNL HubSpot] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL HubSpot] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un [!DNL HubSpot] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL HubSpot] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | El ID de cliente asociado con su [!DNL HubSpot] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL HubSpot] aplicación. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El token de actualización obtenido al autenticar inicialmente la integración de OAuth. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL HubSpot] documento](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Conecte su [!DNL HubSpot] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL HubSpot] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Automatización de marketing]** categoría, seleccionar **[!UICONTROL HubSpot]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL HubSpot] conector.

![catalogar](../../../../images/tutorials/create/hubspot/catalog.png)

El **[!UICONTROL Conectar con HubSpot]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL HubSpot] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/hubspot/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL HubSpot] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/hubspot/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL HubSpot] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para incorporar datos del sistema de automatización de marketing a [!DNL Platform]](../../dataflow/marketing-automation.md).
