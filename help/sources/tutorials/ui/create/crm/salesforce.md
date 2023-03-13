---
keywords: Experience Platform;inicio;temas populares;Salesforce;salesforce
solution: Experience Platform
title: Crear una conexión de origen de Salesforce en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Salesforce mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Crear un [!DNL Salesforce] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Salesforce] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Salesforce] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La dirección URL del [!DNL Salesforce] instancia de origen. |
| `username` | El nombre de usuario de [!DNL Salesforce] cuenta de usuario. |
| `password` | La contraseña para el [!DNL Salesforce] cuenta de usuario. |
| `securityToken` | El token de seguridad para [!DNL Salesforce] cuenta de usuario. |

Para obtener más información sobre cómo empezar, consulte [este documento de Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Conecte su [!DNL Salesforce] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Salesforce] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Salesforce]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector de Salesforce.

![catalogar](../../../../images/tutorials/create/salesforce/catalog.png)

El **[!UICONTROL Conectar con Salesforce]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Salesforce] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/salesforce/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Salesforce] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/salesforce/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Salesforce] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/crm.md).
