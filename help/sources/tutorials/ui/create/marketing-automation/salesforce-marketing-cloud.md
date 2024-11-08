---
title: Conecte su cuenta de Marketing Cloud de Salesforce con el Experience Platform a través de la interfaz de usuario
description: Obtenga información sobre cómo conectar su cuenta de Marketing Cloud de Salesforce a Experience Platform a través de la interfaz de usuario.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 2%

---

# Conecte su cuenta de [!DNL Salesforce Marketing Cloud] al Experience Platform mediante la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto a finales de mayo de 2025.

Este tutorial proporciona pasos sobre cómo conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform a través de la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Salesforce Marketing Cloud], puede omitir el resto de este documento y continuar con el tutorial de [introducción de datos de automatización de marketing al Experience Platform mediante la interfaz de usuario](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL Salesforce Marketing Cloud] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | Servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al escribir el valor `host`, debe especificar `{subdomain}.rest.marketingcloudapis.com`. Por ejemplo, si la dirección URL de host es `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, debe escribir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor de host. |
| ID de cliente | Identificador de cliente asociado con la aplicación [!DNL Salesforce Marketing Cloud]. |
| Secreto del cliente | Secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |

Para obtener más información acerca de la autenticación de [!DNL Salesforce Marketing Cloud], visite la [[!DNL Salesforce] documentación de autenticación](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conectar su cuenta de [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. El [!UICONTROL catálogo] muestra una variedad de orígenes admitidos por el Experience Platform.

Puede seleccionar la categoría adecuada de la lista de categorías. También puede utilizar la barra de búsqueda para filtrar por un origen específico.

En la categoría [!UICONTROL Automatización de marketing], seleccione **[!UICONTROL Marketing Cloud de Salesforce]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

![El catálogo de orígenes con el origen de Marketing Cloud de Salesforce seleccionado.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con el Marketing Cloud de Salesforce]**. En esta página, puede crear una cuenta nueva o utilizar una cuenta existente.

### Nueva cuenta

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre para tu cuenta, una descripción opcional y las credenciales de autenticación que corresponden a tu cuenta de [!DNL Salesforce Marketing Cloud].

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta donde puede autenticar una nueva cuenta para el Marketing Cloud de Salesforce.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Cuenta existente

Si ya tiene una cuenta, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar en la lista que aparece.

![Interfaz de cuenta existente donde puede seleccionar una lista de cuentas de Marketing Cloud de Salesforce existentes.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión entre su cuenta de [!DNL Salesforce Marketing Cloud] y el Experience Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing al Experience Platform](../../dataflow/marketing-automation.md).
