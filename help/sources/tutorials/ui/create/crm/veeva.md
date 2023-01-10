---
keywords: Experience Platform;inicio;temas populares;Veeva CRM;veeva
solution: Experience Platform
title: Crear una conexión de origen de Veeva CRM en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Veeva CRM mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---

# Cree un [!DNL Veeva CRM] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten la ingesta de datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Veeva CRM] conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Veeva CRM] cuenta, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar las credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La dirección URL del [!DNL Veeva CRM] instancia de origen. |
| `username` | El nombre de usuario de la variable [!DNL Veeva CRM] cuenta de usuario. |
| `password` | La contraseña de la variable [!DNL Veeva CRM] cuenta de usuario. |
| `securityToken` | El token de seguridad para la variable [!DNL Veeva CRM] cuenta de usuario. |

Para obtener más información, consulte esta [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Conecte su [!DNL Veeva CRM] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Veeva CRM] cuenta para [!DNL Platform].

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL CRM] categoría, seleccione **[!UICONTROL Véeva CRM]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/veeva/catalog.png)

La variable **[!UICONTROL Conectar cuenta de Veeva CRM]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Veeva CRM] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Veeva CRM] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/veeva/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Veeva CRM] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
