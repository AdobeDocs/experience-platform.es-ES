---
keywords: Experience Platform;inicio;temas populares;Salesforce Service Cloud;Salesforce service cloud
solution: Experience Platform
title: Cree una conexión de origen de Salesforce Cloud en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Salesforce Cloud mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Crear un [!DNL Salesforce Service Cloud] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Salesforce Service Cloud] (en lo sucesivo, &quot;SSC&quot;) que utiliza el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión SSC válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

Para acceder a su cuenta SSC el [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `username` | El nombre de usuario de la cuenta de usuario. |
| `password` | Contraseña de la cuenta de usuario. |
| `securityToken` | El token de seguridad de la cuenta de usuario. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Salesforce Service Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Conecte su [!DNL Salesforce Service Cloud] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta SSC a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Éxito del cliente]** categoría, seleccionar **[!UICONTROL Salesforce Service Cloud]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector SSC.

![catalogar](../../../../images/tutorials/create/ssc/catalog.png)

El **[!UICONTROL Conectar con Salesforce Service Cloud]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de CSS. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/ssc/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta SSC con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de SSC. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos de éxito del cliente a [!DNL Platform]](../../dataflow/customer-success.md).
