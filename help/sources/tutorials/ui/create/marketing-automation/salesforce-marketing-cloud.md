---
keywords: Experience Platform;inicio;temas populares;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Crear una conexión de origen de Marketing Cloud de Salesforce en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de Marketing Cloud de Salesforce mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Cree un [!DNL Salesforce Marketing Cloud] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> La variable [!DNL Salesforce Marketing Cloud] el origen está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Salesforce Marketing Cloud] conector de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene un [!DNL Salesforce Marketing Cloud] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Salesforce Marketing Cloud] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al introducir el `host` , solo debe especificar el subdominio y no la dirección URL completa. Por ejemplo, si la dirección URL del host es `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, solo necesita introducir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` como valor de host. |
| `clientId` | El ID de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte su [!DNL Salesforce Marketing Cloud] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Salesforce Marketing Cloud] a Platform.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los conectores mostrados.

En el [!UICONTROL Automatización de marketing] categoría, seleccione **[!UICONTROL Marketing Cloud de Salesforce]** y, a continuación, seleccione **[!UICONTROL Configuración]**.

![catálogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

La variable **[!UICONTROL Conectarse al Marketing Cloud de Salesforce]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Salesforce Marketing Cloud] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Salesforce Marketing Cloud] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce Marketing Cloud] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del sistema de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
