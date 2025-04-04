---
keywords: Experience Platform;inicio;temas populares;Veeva CRM;veeva
solution: Experience Platform
title: Crear una conexión de Source de Veeva CRM en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Veeva CRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Veeva CRM] en la interfaz de usuario

Los conectores de Source en Adobe Experience Platform permiten introducir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Veeva CRM] mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Veeva CRM] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | Dirección URL de la instancia de origen [!DNL Veeva CRM]. |
| `username` | Nombre de usuario para la cuenta de usuario [!DNL Veeva CRM]. |
| `password` | Contraseña de la cuenta de usuario [!DNL Veeva CRM]. |
| `securityToken` | Token de seguridad para la cuenta de usuario [!DNL Veeva CRM]. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Conectar su cuenta de [!DNL Veeva CRM]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Veeva CRM] a [!DNL Experience Platform].

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL CRM], seleccione **[!UICONTROL Veeva CRM]** y luego seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/veeva/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Veeva CRM]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Veeva CRM] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Veeva CRM]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/veeva/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Veeva CRM]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Experience Platform](../../dataflow/crm.md).
