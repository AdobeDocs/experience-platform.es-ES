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

# Crear un [!DNL Veeva CRM] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos CRM de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Veeva CRM] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Veeva CRM] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/crm.md).

### Recopilar credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La dirección URL del [!DNL Veeva CRM] instancia de origen. |
| `username` | El nombre de usuario de [!DNL Veeva CRM] cuenta de usuario. |
| `password` | La contraseña para el [!DNL Veeva CRM] cuenta de usuario. |
| `securityToken` | El token de seguridad para [!DNL Veeva CRM] cuenta de usuario. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Conecte su [!DNL Veeva CRM] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Veeva CRM] cuenta a [!DNL Platform].

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL CRM] categoría, seleccionar **[!UICONTROL Veeva CRM]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/veeva/catalog.png)

El **[!UICONTROL Conectar la cuenta de Veeva CRM]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Veeva CRM] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y su [!DNL Veeva CRM] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/veeva/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Veeva CRM] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/crm.md).
