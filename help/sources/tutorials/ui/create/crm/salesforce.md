---
title: Conexión de la cuenta de Salesforce mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Salesforce y llevar los datos de CRM al Experience Platform mediante la interfaz de usuario.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

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

Para autenticar su [!DNL Salesforce] cuenta contra Experience Platform, debe proporcionar valores que correspondan a lo siguiente [!DNL Salesforce] credenciales:

| Credencial | Descripción |
| --- | --- |
| `environmentUrl` | La dirección URL del [!DNL Salesforce] instancia de origen. |
| `username` | El nombre de usuario de [!DNL Salesforce] cuenta de usuario. |
| `password` | La contraseña para el [!DNL Salesforce] cuenta de usuario. |
| `securityToken` | El token de seguridad para [!DNL Salesforce] cuenta de usuario. |
| `apiVersion` | (Opcional) La versión de la API de REST de [!DNL Salesforce] instancia de que está utilizando. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre la autenticación, consulte [esta [!DNL Salesforce] guía de autenticación](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para conectar su [!DNL Salesforce] cuenta para el Experience Platform.

## Conecte su [!DNL Salesforce] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder al espacio de trabajo de orígenes. El *[!UICONTROL Catálogo]* La pantalla muestra una variedad de fuentes disponibles en el catálogo de fuentes de Experience Platform.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar una fuente específica utilizando la opción de búsqueda.

Seleccionar **[!UICONTROL CRM]** en la lista de categorías de fuentes y, a continuación, seleccione **[!UICONTROL Añadir datos]** desde el [!DNL Salesforce] Tarjeta de.

![El catálogo de fuentes de la interfaz de usuario de Experience Platform con la tarjeta de origen de Salesforce seleccionada.](../../../../images/tutorials/create/salesforce/catalog.png)

El **[!UICONTROL Conectar con Salesforce]** página. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Usar una cuenta de Salesforce existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione la cuenta que desee utilizar en la lista que aparece. Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas de Salesforce autenticadas que ya existen en su organización.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Crear una nueva cuenta de Salesforce]

Para usar una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y proporcione un nombre, una descripción y su [!DNL Salesforce] credenciales de autenticación. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y espere unos segundos para que se establezca la nueva conexión.

![Interfaz en la que se puede crear una nueva cuenta de Salesforce al proporcionar las credenciales de autenticación adecuadas.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/crm.md).
