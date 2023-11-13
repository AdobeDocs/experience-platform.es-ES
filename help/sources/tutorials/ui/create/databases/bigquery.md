---
title: Creación de una conexión de origen de Google Big Query en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Google Big Query mediante la interfaz de usuario de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Crear un [!DNL Google Big Query] conexión de origen en la interfaz de usuario

>[!IMPORTANT]
>
>El [!DNL Google BigQuery] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Google Big Query] conexión de origen mediante la interfaz de usuario de Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Google BigQuery] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Google BigQuery] en Platform, debe proporcionar los siguientes valores de autenticación OAuth 2.0:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | El ID del proyecto predeterminado [!DNL Google BigQuery] proyecto con el que consultar. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] se utiliza para autorizar el acceso a [!DNL Google BigQuery]. |

Para obtener más información, consulte [esta [!DNL Google BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Conecte su cuenta de Google BigQuery

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccionar **[!UICONTROL Google BigQuery]** y luego seleccione **[!UICONTROL Añadir datos]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

El **[!UICONTROL Conectar con Google Big Query]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Google BigQuery] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Google BigQuery] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Google BigQuery] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/databases.md).
