---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Crear una conexión de Source de Zoho CRM en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen Zoho CRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Zoho CRM] en la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL Zoho CRM] quedará obsoleto a finales de mayo de 2025. Como alternativa, puede utilizar el origen [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Los conectores de Source en Adobe Experience Platform permiten introducir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Zoho CRM] mediante la interfaz de usuario [!DNL Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Zoho CRM] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

Para conectar [!DNL Zoho CRM] a Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Punto de conexión | Extremo del servidor [!DNL Zoho CRM] al que realiza la solicitud. |
| URL de cuentas | La dirección URL de cuentas se utiliza para generar los tokens de acceso y actualización. La dirección URL debe ser específica del dominio. |
| ID de cliente | Identificador de cliente que corresponde con su cuenta de usuario [!DNL Zoho CRM]. |
| Secreto del cliente | Secreto de cliente que corresponde a su cuenta de usuario [!DNL Zoho CRM]. |
| Token de acceso | El token de acceso autoriza el acceso seguro y temporal a su cuenta de [!DNL Zoho CRM]. |
| Actualizar token | Un token de actualización es un token que se utiliza para generar un nuevo token de acceso, una vez que el token de acceso ha caducado. |

Para obtener más información sobre estas credenciales, consulte la documentación sobre la [[!DNL Zoho CRM] autenticación](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conectar su cuenta de [!DNL Zoho CRM]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Zoho CRM] a [!DNL Platform].

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL CRM], seleccione **[!UICONTROL Zoho CRM]** y luego seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/zoho/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta Zoho CRM]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Zoho CRM] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/zoho/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Zoho CRM]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

>[!TIP]
>
>El dominio URL de las cuentas debe corresponder con la ubicación de dominio adecuada. A continuación se indican los distintos dominios y las direcciones URL de sus cuentas correspondientes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![nuevo](../../../../images/tutorials/create/zoho/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Zoho CRM]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en la plataforma](../../dataflow/crm.md).
