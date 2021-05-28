---
keywords: Experience Platform;inicio;temas populares;ServiceNow;servicenow
solution: Experience Platform
title: Crear una conexión de origen de ServiceNow en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de ServiceNow mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL ServiceNow] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL ServiceNow] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL ServiceNow] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/customer-success.md)

### Recopilar las credenciales necesarias

Para acceder a su cuenta [!DNL ServiceNow] en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El extremo del servidor [!DNL ServiceNow]. |
| `username` | El nombre de usuario utilizado para conectarse al servidor [!DNL ServiceNow] para la autenticación. |
| `password` | La contraseña para conectarse al servidor [!DNL ServiceNow] para la autenticación. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL ServiceNow] documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Conecte su cuenta [!DNL ServiceNow]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL ServiceNow] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Orígenes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Orígenes]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Customer Success]**, seleccione **[!UICONTROL ServiceNow]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Connect source]** para crear un nuevo conector [!DNL ServiceNow].

![](../../../../images/tutorials/create/servicenow/catalog.png)

Aparece la página **[!UICONTROL Connect to ServiceNow]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales [!DNL ServiceNow]. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/servicenow/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL ServiceNow] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL ServiceNow]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/customer-success.md).
