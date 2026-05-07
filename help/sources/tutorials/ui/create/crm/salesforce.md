---
title: Conectar su cuenta de Salesforce mediante la interfaz de usuario de Experience Platform
description: Obtenga información sobre cómo conectar su cuenta de Salesforce y llevar los datos de CRM a Experience Platform mediante la interfaz de usuario.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 11e9e1a25a45f4011f15b1e28753a98d4158012c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 3%

---

# Conecte su cuenta de [!DNL Salesforce] a Experience Platform mediante la interfaz de usuario

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Salesforce] e introducir los datos de CRM en Adobe Experience Platform mediante la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta [!DNL Salesforce] autenticada, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para datos CRM](../../dataflow/crm.md).

### Recopilar credenciales necesarias {#gather-required-credentials}

El origen [!DNL Salesforce] admite la autenticación mediante la credencial de cliente OAuth2.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | Dirección URL de la instancia de origen [!DNL Salesforce]. El formato de la URL del entorno es `https://[domain].my.salesforce.com`. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| Secreto del cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| Versión de API | La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, Experience Platform utilizará automáticamente la última versión disponible. |
| Incluir objetos eliminados | Un valor booleano que se utiliza para determinar si se deben incluir los registros eliminados. Si se establece en true, se pueden incluir registros eliminados de forma suave en la consulta [!DNL Salesforce] e ingerirlos desde la cuenta en Experience Platform. Si no especifica la configuración, el valor predeterminado es `false`. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce], lea la [[!DNL Salesforce] guía sobre flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Conectar su cuenta de [!DNL Salesforce]

En la interfaz de usuario de Experience Platform, vaya a **[!UICONTROL Sources]** desde el menú izquierdo para abrir el área de trabajo [!UICONTROL Sources]. Utilice el catálogo de la izquierda para examinar las categorías o utilice la barra de búsqueda para encontrar rápidamente el origen que desea conectar.

Seleccione **[!DNL Salesforce]** en la categoría *[!UICONTROL CRM]* y luego seleccione **[!UICONTROL Add data]**.

>[!TIP]
>
>En el catálogo de orígenes verá **[!UICONTROL Set up]** si no hay ninguna cuenta conectada o **[!UICONTROL Add data]** si una cuenta ya está autenticada.

![El catálogo de orígenes en la interfaz de usuario de Experience Platform con la tarjeta de origen de Salesforce seleccionada.](../../../../images/tutorials/create/salesforce/catalog.png)

Aparecerá la página **[!UICONTROL Connect to Salesforce]**. En esta página, puede usar credenciales nuevas o existentes.

### Usar una cuenta existente

Para usar una cuenta existente, seleccione **[!UICONTROL Existing account]** y luego seleccione la cuenta que desee usar en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Next]** para continuar.

![Una lista de cuentas de Salesforce autenticadas que ya existen en su organización.](../../../../images/tutorials/create/salesforce/existing.png)

### Crear una nueva cuenta

Para crear una nueva cuenta, seleccione **[!UICONTROL New account]** y proporcione un nombre y una descripción para la nueva cuenta de [!DNL Salesforce].

Para la credencial de cliente de OAuth 2, seleccione **[!UICONTROL OAuth2 Client Credential]** y proporcione valores para las siguientes credenciales:

* URL de entorno
* ID de cliente
* Secreto del cliente
* Versión de API
* Incluir objetos de eliminación

Cuando termine, seleccione **[!UICONTROL Connect to source]**.


![Interfaz en la que puede crear una nueva cuenta de Salesforce proporcionando las credenciales de autenticación adecuadas.](../../../../images/tutorials/create/salesforce/new.png)

### Omitir vista previa de datos de ejemplo {#skip-preview-of-sample-data}

Durante el paso de selección de datos, puede encontrar un tiempo de espera al ingerir tablas o archivos de datos grandes. Puede omitir la previsualización de datos para evitar el tiempo de espera y seguir viendo el esquema, aunque sin datos de ejemplo. Para omitir la vista previa de datos, habilite la opción **[!UICONTROL Skip previewing sample data]**.

El resto del flujo de trabajo sigue siendo el mismo. La única advertencia es que omitir la previsualización de datos puede impedir que los campos calculados y requeridos se validen automáticamente durante el paso de asignación y, a continuación, tendrá que validar manualmente esos campos durante la asignación.

## Próximos pasos

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Salesforce]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Experience Platform]](../../dataflow/crm.md).
