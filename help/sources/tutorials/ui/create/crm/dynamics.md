---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics;dynamics
solution: Experience Platform
title: Crear una conexión de Source de Microsoft Dynamics en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Microsoft Dynamics mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Microsoft Dynamics] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de [!DNL Microsoft Dynamics] (denominada en adelante como &quot;[!DNL Dynamics]&quot;) mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Dynamics] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para un origen CRM](../../dataflow/crm.md).

### Recopilar credenciales necesarias

Para autenticar el origen de [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

>[!BEGINTABS]

>[!TAB Autenticación básica]

| Credencial | Descripción |
| --- | --- |
| `serviceUri` | La URL de servicio de su instancia [!DNL Dynamics]. |
| `username` | El nombre de usuario de su cuenta de usuario [!DNL Dynamics]. |
| `password` | Contraseña de su cuenta de [!DNL Dynamics]. |

>[!TAB Autenticación de clave y principal de servicio]

| Credencial | Descripción |
| --- | --- |
| `servicePrincipalId` | Identificador de cliente de su cuenta de [!DNL Dynamics]. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |

>[!ENDTABS]

Para obtener más información sobre cómo empezar, consulte [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Conectar su cuenta de [!DNL Dynamics]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL CRM], seleccione **[!UICONTROL Microsoft Dynamics]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con Microsoft Dynamics seleccionado.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Microsoft Dynamics]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, selecciona la cuenta de [!DNL Dynamics] que quieras usar y luego selecciona **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nueva cuenta

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Dynamics]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Para crear una nueva cuenta, selecciona **[!UICONTROL Nueva cuenta]** y, a continuación, proporciona un nombre y una descripción opcional para la nueva cuenta de [!DNL Dynamics].

![La nueva interfaz de creación de cuentas.](../../../../images/tutorials/create/ms-dynamics/new.png)

Puede usar autenticación básica o autenticación de clave y principal de servicio al crear una cuenta de [!DNL Dynamics].

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para crear una cuenta de [!DNL Dynamics] con autenticación básica, selecciona [!UICONTROL Autenticación básica] y, a continuación, proporciona los valores de tu [!UICONTROL URI de servicio], [!UICONTROL Nombre de usuario] y [!UICONTROL Contraseña]. **Nota**: la autenticación básica en [!DNL Dynamics] puede ser bloqueada por la autenticación de doble factor, que actualmente no es compatible con Platform. En este caso, se recomienda utilizar la autenticación basada en claves para crear un conector de origen con [!DNL Dynamics].

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que la nueva cuenta se establezca.

![Interfaz de autenticación básica.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Autenticación de clave y principal de servicio]

Para crear una cuenta de [!DNL Dynamics] con autenticación de clave y principal de servicio, seleccione **[!UICONTROL Autenticación de clave y principal de servicio]** y, a continuación, proporcione valores para su [!UICONTROL ID principal de servicio] y [!UICONTROL clave principal de servicio].

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que la nueva cuenta se establezca.

![Interfaz de autenticación de clave principal de servicio.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Dynamics]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](../../dataflow/crm.md).
