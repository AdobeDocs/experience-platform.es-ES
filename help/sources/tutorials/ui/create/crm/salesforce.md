---
title: Conexión de la cuenta de Salesforce mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Salesforce y a llevar los datos de CRM al Experience Platform mediante la interfaz de usuario de.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# Conecte su cuenta de [!DNL Salesforce] al Experience Platform mediante la interfaz de usuario

Este tutorial proporciona pasos sobre cómo conectar su cuenta de [!DNL Salesforce] y llevar los datos de CRM a Adobe Experience Platform mediante la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta [!DNL Salesforce] autenticada, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para datos CRM](../../dataflow/crm.md).

### Recopilar credenciales necesarias {#gather-required-credentials}

El origen [!DNL Salesforce] admite la autenticación básica y la credencial de cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Debe proporcionar valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Salesforce] mediante la autenticación básica.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | Dirección URL de la instancia de origen [!DNL Salesforce]. El formato de la URL del entorno es `https://[domain].my.salesforce.com`. |
| Nombre de usuario | Nombre de usuario para la cuenta de usuario [!DNL Salesforce]. |
| Contraseña | Contraseña de la cuenta de usuario [!DNL Salesforce]. |
| Token de seguridad | Token de seguridad para la cuenta de usuario [!DNL Salesforce]. |
| Versión de API | (Opcional) La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre la autenticación, consulte [esta [!DNL Salesforce] guía de autenticación](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial de cliente de OAuth2]

Debe proporcionar valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Salesforce] mediante la credencial de cliente de OAuth2.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | Dirección URL de la instancia de origen [!DNL Salesforce]. El formato de la URL del entorno es `https://[domain].my.salesforce.com`. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| Secreto del cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| Versión de API | La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce], lea la [[!DNL Salesforce] guía sobre flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para conectar su cuenta de [!DNL Salesforce] al Experience Platform.

## Conectar su cuenta de [!DNL Salesforce]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

Seleccione **[!DNL Salesforce]** en la categoría *[!UICONTROL CRM]* y luego seleccione **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes en la interfaz de usuario del Experience Platform con la tarjeta de origen de Salesforce seleccionada.](../../../../images/tutorials/create/salesforce/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a Salesforce]**. En esta página, puede usar credenciales nuevas o existentes.

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas de Salesforce autenticadas que ya existen en su organización.](../../../../images/tutorials/create/salesforce/existing.png)

### Crear una nueva cuenta

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre y una descripción para tu nueva cuenta de [!DNL Salesforce].

![Interfaz en la que puede crear una nueva cuenta de Salesforce proporcionando las credenciales de autenticación adecuadas.](../../../../images/tutorials/create/salesforce/new.png)

A continuación, seleccione el tipo de autenticación que desee utilizar para la nueva cuenta.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para la autenticación básica, seleccione **[!UICONTROL Autenticación básica]** y proporcione valores para las siguientes credenciales:

* URL de entorno
* Nombre de usuario
* Contraseña
* Versión de API (opcional)

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]**.

![Interfaz de autenticación básica para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB Credencial de cliente de OAuth2]

Para la credencial de cliente de OAuth 2, seleccione **[!UICONTROL Credencial de cliente de OAuth2]** y, a continuación, proporcione valores para las siguientes credenciales:

* URL de entorno
* ID de cliente
* Secreto del cliente
* Versión de API

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]**.

![Interfaz de OAuth para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

### Omitir vista previa de datos de ejemplo {#skip-preview-of-sample-data}

Durante el paso de selección de datos, puede encontrar un tiempo de espera al ingerir tablas o archivos de datos grandes. Puede omitir la previsualización de datos para evitar el tiempo de espera y seguir viendo el esquema, aunque sin datos de ejemplo. Para omitir la vista previa de datos, active la opción **[!UICONTROL Omitir vista previa de datos de ejemplo]**.

El resto del flujo de trabajo sigue siendo el mismo. La única advertencia es que omitir la previsualización de datos puede impedir que los campos calculados y requeridos se validen automáticamente durante el paso de asignación y, a continuación, tendrá que validar manualmente esos campos durante la asignación.

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Salesforce]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/crm.md).
