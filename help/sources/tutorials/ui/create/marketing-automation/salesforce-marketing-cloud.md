---
keywords: Experience Platform;inicio;temas populares;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Crear una conexión de origen de Marketing Cloud de Salesforce en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Marketing Cloud de Salesforce mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Salesforce Marketing Cloud] en la interfaz de usuario

>[!NOTE]
>
> El origen [!DNL Salesforce Marketing Cloud] está en versión beta. Consulte [sources overview](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona pasos para crear un conector de origen [!DNL Salesforce Marketing Cloud] mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Salesforce Marketing Cloud], puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL Salesforce Marketing Cloud] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El servidor host de la aplicación. Este suele ser su subdominio. |
| `clientId` | El ID de cliente asociado con su aplicación [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | El secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte su cuenta [!DNL Salesforce Marketing Cloud]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Salesforce Marketing Cloud] a Platform.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los conectores mostrados.

En la categoría [!UICONTROL Marketing Automation], seleccione **[!UICONTROL Marketing Cloud de Salesforce]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Aparece la página **[!UICONTROL Connect to Salesforce Marketing Cloud]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL Salesforce Marketing Cloud]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Salesforce Marketing Cloud] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Salesforce Marketing Cloud]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del sistema de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
