---
keywords: Experience Platform;inicio;temas populares;ServiceNow;servicenow
solution: Experience Platform
title: Crear una conexión de origen de ServiceNow en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de ServiceNow mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Cree un [!DNL ServiceNow] conexión de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL ServiceNow] conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL ServiceNow] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar las credenciales necesarias

Para acceder a su [!DNL ServiceNow] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El punto final de la variable [!DNL ServiceNow] servidor. |
| `username` | El nombre de usuario utilizado para conectarse a la variable [!DNL ServiceNow] para la autenticación. |
| `password` | La contraseña para conectarse a la variable [!DNL ServiceNow] para la autenticación. |

Para obtener más información sobre cómo empezar, consulte [this [!DNL ServiceNow] documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Conecte su [!DNL ServiceNow] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL ServiceNow] cuenta para [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL Éxito del cliente]** categoría, seleccione **[!UICONTROL ServiceNow]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Conectar origen]** para crear un [!DNL ServiceNow] conector.

![](../../../../images/tutorials/create/servicenow/catalog.png)

La variable **[!UICONTROL Conectarse a ServiceNow]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL ServiceNow] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![](../../../../images/tutorials/create/servicenow/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL ServiceNow] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL ServiceNow] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos [!DNL Platform]](../../dataflow/customer-success.md).
