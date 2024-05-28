---
title: Conectar su cuenta de Salesforce Service Cloud mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Salesforce Service Cloud y a llevar los datos de éxito de los clientes a Experience Platform mediante la interfaz de usuario.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 3%

---

# Conecte su [!DNL Salesforce Service Cloud] cuenta de al Experience Platform mediante la interfaz de usuario de

Este tutorial proporciona pasos sobre cómo conectar su [!DNL Salesforce Service Cloud] y llevar los datos de éxito de los clientes a Adobe Experience Platform mediante la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Salesforce Service Cloud] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración correcta de un flujo de datos para un cliente](../../dataflow/customer-success.md)

### Recopilar credenciales necesarias

El [!DNL Salesforce Service Cloud] El origen de admite la autenticación básica y la credencial de cliente de OAuth2.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Debe proporcionar valores para las siguientes credenciales para conectar su [!DNL Salesforce Service Cloud] cuenta que utiliza autenticación básica.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | La dirección URL del [!DNL Salesforce Service Cloud] instancia de origen. |
| Nombre de usuario | El nombre de usuario de [!DNL Salesforce Service Cloud] cuenta de usuario. |
| Contraseña | La contraseña para el [!DNL Salesforce Service Cloud] cuenta de usuario. |
| Token de seguridad | El token de seguridad para [!DNL Salesforce Service Cloud] cuenta de usuario. |
| Versión de API | (Opcional) La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre la autenticación, consulte [esta [!DNL Salesforce Service Cloud] guía de autenticación](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Credencial de cliente de OAuth2]

Debe proporcionar valores para las siguientes credenciales para conectar su [!DNL Salesforce Service Cloud] cuenta con credencial de cliente de OAuth2.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | La dirección URL del [!DNL Salesforce Service Cloud] instancia de origen. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce Service Cloud]. |
| Secreto del cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce Service Cloud]. |
| Versión de API | La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce Service Cloud], lea la [[!DNL Salesforce Service Cloud] Guía de flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para conectar su [!DNL Salesforce Service Cloud] cuenta para el Experience Platform.

## Conecte su [!DNL Salesforce Service Cloud] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

Seleccionar **[!DNL Salesforce Service Cloud]** en el *[!UICONTROL Éxito del cliente]* y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las fuentes del catálogo de fuentes muestran el **[!UICONTROL Configuración de]** cuando una fuente determinada aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de la interfaz de usuario de Experience Platform con la tarjeta de fuente de Salesforce Cloud seleccionada.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

El **[!UICONTROL Conectar con Salesforce Service Cloud]** página. En esta página, puede usar credenciales nuevas o existentes.

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione la cuenta que desee en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas autenticadas de Salesforce Service Cloud que ya existen en su organización.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Crear una nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y proporcione un nombre y una descripción para su nuevo [!DNL Salesforce Service Cloud] cuenta.

![Interfaz en la que puede crear una nueva cuenta de Salesforce Cloud proporcionando las credenciales de autenticación adecuadas.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

A continuación, seleccione el tipo de autenticación que desee utilizar para la nueva cuenta.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para la autenticación básica, seleccione **[!UICONTROL Autenticación básica]** y, a continuación, proporcione valores para las siguientes credenciales:

* URL de entorno
* Nombre de usuario
* Contraseña
* Versión de API (opcional)

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de autenticación básica para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Credencial de cliente de OAuth2]

Para la credencial de cliente de OAuth 2, seleccione **[!UICONTROL Credencial de cliente de OAuth2]** y, a continuación, proporcione valores para las siguientes credenciales:

* URL de entorno
* ID de cliente
* Secreto del cliente
* Versión de API

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![Interfaz de OAuth para la creación de cuentas de Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce Service Cloud] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para llevar los datos de éxito del cliente a Experience Platform](../../dataflow/customer-success.md).
