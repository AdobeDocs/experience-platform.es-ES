---
title: Conexión de la cuenta de Salesforce mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Salesforce y llevar los datos de CRM al Experience Platform mediante la interfaz de usuario.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 8d62cf4ca0071e84baa9399e0a25f7ebfb096c1a
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# Conecte su [!DNL Salesforce] cuenta de al Experience Platform mediante la interfaz de usuario de

Este tutorial proporciona pasos sobre cómo conectar su [!DNL Salesforce] y llevar los datos de CRM a Adobe Experience Platform mediante la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un [!DNL Salesforce] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para datos CRM](../../dataflow/crm.md).

### Recopilar credenciales necesarias {#gather-required-credentials}

El [!DNL Salesforce] El origen de admite la autenticación básica y la credencial de cliente de OAuth2.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Debe proporcionar valores para las siguientes credenciales para conectar su [!DNL Salesforce] cuenta que utiliza autenticación básica.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | La dirección URL del [!DNL Salesforce] instancia de origen. |
| Nombre de usuario | El nombre de usuario de [!DNL Salesforce] cuenta de usuario. |
| Una contraseña | La contraseña para el [!DNL Salesforce] cuenta de usuario. |
| Token de seguridad | El token de seguridad para [!DNL Salesforce] cuenta de usuario. |
| Versión de API | (Opcional) La versión de la API de REST de [!DNL Salesforce] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre la autenticación, consulte [esta [!DNL Salesforce] guía de autenticación](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial de cliente de OAuth2]

Debe proporcionar valores para las siguientes credenciales para conectar su [!DNL Salesforce] cuenta con credencial de cliente de OAuth2.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | La dirección URL del [!DNL Salesforce] instancia de origen. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce]. |
| Secreto de cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce]. |
| Versión de API | La versión de la API de REST de [!DNL Salesforce] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce], lea la [[!DNL Salesforce] Guía de flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para conectar su [!DNL Salesforce] cuenta para el Experience Platform.

## Conecte su [!DNL Salesforce] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *CRM* categoría, seleccionar **[!DNL Salesforce]**, y luego seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las fuentes del catálogo de fuentes muestran el **[!UICONTROL Configuración de]** cuando una fuente determinada aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de la interfaz de usuario de Experience Platform con la tarjeta de origen de Salesforce seleccionada.](../../../../images/tutorials/create/salesforce/catalog.png)

El **[!UICONTROL Conectar con Salesforce]** página. En esta página, puede usar credenciales nuevas o existentes.

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione la cuenta que desee utilizar en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas de Salesforce autenticadas que ya existen en su organización.](../../../../images/tutorials/create/salesforce/existing.png)

### Crear una nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y proporcione un nombre y una descripción para su nuevo [!DNL Salesforce] cuenta.

![Interfaz en la que se puede crear una nueva cuenta de Salesforce al proporcionar las credenciales de autenticación adecuadas.](../../../../images/tutorials/create/salesforce/new.png)

A continuación, seleccione el tipo de autenticación que desee utilizar para la nueva cuenta.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para la autenticación básica, seleccione **[!UICONTROL Autenticación básica]** y, a continuación, proporcione valores para las siguientes credenciales:

* URL de entorno
* Nombre de usuario
* Una contraseña
* Versión de API (opcional)

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación básica para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB Credencial de cliente de OAuth2]

Para la credencial de cliente de OAuth 2, seleccione **[!UICONTROL Credencial de cliente de OAuth2]** y, a continuación, proporcione valores para las siguientes credenciales:

* URL de entorno
* ID de cliente
* Secreto de cliente
* Versión de API

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de OAuth para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/crm.md).
