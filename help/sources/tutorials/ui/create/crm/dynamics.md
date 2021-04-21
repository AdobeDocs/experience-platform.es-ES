---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;Dynamics;dinámica
solution: Experience Platform
title: Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft Dynamics mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Microsoft Dynamics] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Microsoft Dynamics] (denominada en adelante &quot;[!DNL Dynamics]&quot;) mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una cuenta [!DNL Dynamics] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos para una fuente de CRM](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La URL de servicio de su instancia [!DNL Dynamics]. |
| `username` | El nombre de usuario de su cuenta de usuario [!DNL Dynamics]. |
| `password` | La contraseña de su cuenta [!DNL Dynamics]. |
| `servicePrincipalId` | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte su cuenta [!DNL Dynamics]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Dynamics] a Platform.

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL CRM]**, seleccione **[!UICONTROL Microsoft Dynamics]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector [!DNL Dynamics].

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Aparece la página **[!UICONTROL Connect to Dynamics]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, proporcione un nombre y una descripción opcional para su nueva cuenta [!DNL Dynamics].

El conector [!DNL Dynamics] proporciona diferentes tipos de autenticación para el acceso. En [!UICONTROL Account authentication] seleccione **[!UICONTROL Basic authentication]** para utilizar credenciales basadas en contraseña.

Cuando termine, seleccione **[!UICONTROL Connect to source]** y, a continuación, deje que se establezca algún tiempo para la nueva cuenta.

![autenticación básica](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Como alternativa, puede seleccionar **[!UICONTROL Service-principal and key authentication]** y conectar su cuenta [!DNL Dynamics] mediante una combinación de [!UICONTROL Service principal ID] y [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> La autenticación básica en [!DNL Dynamics] puede bloquearse con la autenticación de dos factores, que actualmente no es compatible con Platform. En este caso, se recomienda utilizar la autenticación basada en claves para crear un conector de origen utilizando [!DNL Dynamics].

![autenticación basada en claves](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credencial | Descripción |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| [!UICONTROL Service principal key] | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta [!DNL Dynamics] con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Dynamics]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
