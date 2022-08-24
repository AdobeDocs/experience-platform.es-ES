---
keywords: Experience Platform;inicio;temas populares;Google Big Query;Google big query;GBQ;gbq
solution: Experience Platform
title: Crear una conexión de origen de consulta grande de Google en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen Google Big Query mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Cree un [!DNL Google Big Query] conexión de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Google Big Query] conexión de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Google BigQuery] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Google BigQuery] en Platform, debe proporcionar los siguientes valores de autenticación de OAuth 2.0:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | ID del proyecto predeterminado [!DNL Google BigQuery] proyecto con el que realizar la consulta. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] usado para autorizar el acceso a [!DNL Google BigQuery]. |

Para obtener más información sobre estos valores, consulte [this [!DNL Google BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Conecte su cuenta de Google BigQuery

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL Bases de datos] categoría, seleccione **[!UICONTROL Google BigQuery]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

La variable **[!UICONTROL Conectarse a Google Big Query]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Google BigQuery] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Google BigQuery] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Google BigQuery] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en Platform](../../dataflow/databases.md).
