---
keywords: Experience Platform;inicio;temas populares;Veeva CRM;veeva
solution: Experience Platform
title: Crear una conexión de origen de Veeva CRM en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Veeva CRM mediante la interfaz de usuario de Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Veeva CRM] en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Veeva CRM] mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una cuenta [!DNL Veeva CRM] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La dirección URL de la instancia de origen [!DNL Veeva CRM]. |
| `username` | El nombre de usuario de la cuenta de usuario [!DNL Veeva CRM]. |
| `password` | La contraseña de la cuenta de usuario [!DNL Veeva CRM]. |
| `securityToken` | Token de seguridad para la cuenta de usuario [!DNL Veeva CRM]. |

Para obtener más información sobre la introducción, consulte [este documento de Veeva CRM]

## Conecte su cuenta [!DNL Veeva CRM]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta [!DNL Veeva CRM] a [!DNL Platform].

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría [!UICONTROL CRM], seleccione **[!UICONTROL Veva CRM]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/veeva/catalog.png)

Aparece la página **[!UICONTROL Connect Veeva CRM account]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la cuenta [!DNL Veeva CRM] con la que desea crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL New account]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales [!DNL Veeva CRM]. Cuando termine, seleccione **[!UICONTROL Connect to source]** y, a continuación, deje que se establezca la nueva conexión.

![new](../../../../images/tutorials/create/veeva/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta [!DNL Veeva CRM]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
