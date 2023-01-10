---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;Dynamics;dinámica
solution: Experience Platform
title: Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft Dynamics mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Cree un [!DNL Microsoft Dynamics] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Microsoft Dynamics] (en lo sucesivo, &quot;el[!DNL Dynamics]&quot;) conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Dynamics] cuenta, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos para un origen CRM](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La URL de servicio de su [!DNL Dynamics] instancia. |
| `username` | El nombre de usuario de su [!DNL Dynamics] cuenta de usuario. |
| `password` | La contraseña de su [!DNL Dynamics] cuenta. |
| `servicePrincipalId` | El ID de cliente de su [!DNL Dynamics] cuenta. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

Para obtener más información, consulte [this [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte su [!DNL Dynamics] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Dynamics] a Platform.

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL CRM]** categoría, seleccione **[!UICONTROL Microsoft Dynamics]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un [!DNL Dynamics] conector.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La variable **[!UICONTROL Conectarse a Dynamics]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre y una descripción opcional para el nuevo [!DNL Dynamics] cuenta.

La variable [!DNL Dynamics] connector proporciona diferentes tipos de autenticación para el acceso. En [!UICONTROL Autenticación de la cuenta] select **[!UICONTROL Autenticación básica]** para utilizar credenciales basadas en contraseña.

Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y después dejar un tiempo para que la nueva cuenta se establezca.

![autenticación básica](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

También puede seleccionar **[!UICONTROL Autenticación de clave y entidad de seguridad de servicio]** y conecte su [!DNL Dynamics] cuenta con una combinación de [!UICONTROL ID de principal de servicio] y [!UICONTROL Clave principal del servicio].

>[!IMPORTANT]
>
> Autenticación básica en [!DNL Dynamics] puede bloquearse con la autenticación de dos factores, que actualmente no es compatible con Platform. En este caso, se recomienda utilizar la autenticación basada en claves para crear un conector de origen utilizando [!DNL Dynamics].

![autenticación basada en claves](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credencial | Descripción |
| ---------- | ----------- |
| [!UICONTROL ID de principal de servicio] | El ID de cliente de su [!DNL Dynamics] cuenta. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| [!UICONTROL Clave principal del servicio] | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Dynamics] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Dynamics] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
