---
keywords: Experience Platform;inicio;temas populares;Salesforce Service Cloud;nube de servicio de salesforce
solution: Experience Platform
title: Crear una conexión de origen de nube de Salesforce Service en la interfaz de usuario
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Salesforce Service Cloud mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a0b016e8adc519bc79701f9fd850b6ddf7d46127
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Salesforce Service Cloud] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Salesforce Service Cloud] (en adelante denominado &quot;SSC&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión SSC válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta SSC en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `username` | El nombre de usuario de la cuenta de usuario. |
| `password` | La contraseña de la cuenta de usuario. |
| `securityToken` | Token de seguridad de la cuenta de usuario. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Salesforce Service Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Conecte su cuenta [!DNL Salesforce Service Cloud]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta SSC a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Customer Success]**, seleccione **[!UICONTROL Salesforce Service Cloud]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector SSC.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

Aparece la página **[!UICONTROL Connect to Salesforce Service Cloud]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales de SSC. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta SSC con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de SSC. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir los datos de éxito del cliente en [!DNL Platform]](../../dataflow/customer-success.md).