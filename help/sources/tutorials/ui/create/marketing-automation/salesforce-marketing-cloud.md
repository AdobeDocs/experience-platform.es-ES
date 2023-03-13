---
keywords: Experience Platform;inicio;temas populares;Salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Crear una conexión de origen de Marketing Cloud de Salesforce en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Marketing Cloud de Salesforce mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Crear un [!DNL Salesforce Marketing Cloud] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Salesforce Marketing Cloud] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Salesforce Marketing Cloud] conector de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un [!DNL Salesforce Marketing Cloud] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Salesforce Marketing Cloud] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al introducir su `host` , solo necesita especificar el subdominio y no la dirección URL completa. Por ejemplo, si la dirección URL del host es `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, entonces solo necesita introducir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` como valor de host. |
| `clientId` | El ID de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte su [!DNL Salesforce Marketing Cloud] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Salesforce Marketing Cloud] a Platform.

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los conectores mostrados.

En el [!UICONTROL Automatización de marketing] categoría, seleccionar **[!UICONTROL Marketing Cloud de Salesforce]** y luego seleccione **[!UICONTROL Configuración de]**.

![catalogar](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

El **[!UICONTROL Conectar con Salesforce Marketing Cloud]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Salesforce Marketing Cloud] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Salesforce Marketing Cloud] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce Marketing Cloud] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para incorporar datos del sistema de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
