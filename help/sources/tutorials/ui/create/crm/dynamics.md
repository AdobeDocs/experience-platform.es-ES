---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics;dynamics
solution: Experience Platform
title: Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft Dynamics mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Crear un [!DNL Microsoft Dynamics] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Microsoft Dynamics] (en lo sucesivo, &quot;[!DNL Dynamics]&quot;) mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Dynamics] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para una fuente CRM](../../dataflow/crm.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Dynamics] origen, debe proporcionar valores para las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación básica]

| Credencial | Descripción |
| --- | --- |
| `serviceUri` | La URL de servicio de su [!DNL Dynamics] ejemplo. |
| `username` | El nombre de usuario de su [!DNL Dynamics] cuenta de usuario. |
| `password` | La contraseña de su [!DNL Dynamics] cuenta. |

>[!TAB Autenticación de clave y principal de servicio]

| Credencial | Descripción |
| --- | --- |
| `servicePrincipalId` | El ID de cliente de su [!DNL Dynamics] cuenta. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |

>[!ENDTABS]

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conecte su [!DNL Dynamics] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla de muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL CRM] categoría, seleccionar **[!UICONTROL Microsoft Dynamics]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con Microsoft Dynamics seleccionado.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

El **[!UICONTROL Conectar la cuenta de Microsoft Dynamics]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Dynamics] cuenta que desee utilizar y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nueva cuenta

>[!TIP]
>
>Una vez creado, no se puede cambiar el tipo de autenticación de una [!DNL Dynamics] conexión base. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL Dynamics] cuenta.

![La nueva interfaz de creación de cuentas.](../../../../images/tutorials/create/ms-dynamics/new.png)

Puede utilizar la autenticación básica o la autenticación de clave y principal de servicio al crear una [!DNL Dynamics] cuenta.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para crear un [!DNL Dynamics] cuenta con autenticación básica, seleccione [!UICONTROL Autenticación básica] y, a continuación, proporcione valores para su [!UICONTROL URI de servicio], [!UICONTROL Nombre de usuario], y [!UICONTROL Contraseña]. **Nota**: Autenticación básica en [!DNL Dynamics] pueden bloquearse mediante la autenticación de doble factor, que actualmente no es compatible con Platform. En este caso, se recomienda utilizar la autenticación basada en claves para crear un conector de origen utilizando [!DNL Dynamics].

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y luego dejar algo de tiempo para que la nueva cuenta se establezca.

![Interfaz de autenticación básica.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Autenticación de clave y principal de servicio]

Para crear un [!DNL Dynamics] cuenta con autenticación de clave y principal de servicio, seleccione **[!UICONTROL Autenticación de clave y principal de servicio]** y, a continuación, proporcione valores para su [!UICONTROL ID principal de servicio] y [!UICONTROL Clave principal de servicio].

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y luego dejar algo de tiempo para que la nueva cuenta se establezca.

![Interfaz de autenticación de clave principal de servicio.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Dynamics] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
