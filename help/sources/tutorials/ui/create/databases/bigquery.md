---
keywords: Experience Platform;inicio;temas populares;Google Big Query;Google big query;GBQ;gbq
solution: Experience Platform
title: Crear una conexión de origen de consulta grande de Google en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Google Big Query utilizando la interfaz de usuario de Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Google Big Query] en la interfaz de usuario

>[!NOTE]
>
> El conector [!DNL Google BigQuery] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google Big Query] (en adelante denominado &quot;BigQuery&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión BigQuery válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta de BigQuery en [!DNL Platform], debe proporcionar los siguientes valores de autenticación de OAuth 2.0:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | El ID del proyecto predeterminado [!DNL BigQuery] con el que realizar la consulta. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] utilizado para autorizar el acceso a [!DNL BigQuery]. |

Para obtener más información sobre estos valores, consulte [este documento BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Conecte su cuenta de Google BigQuery

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de BigQuery a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Google Big Query]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector BigQuery.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Aparece la página **[!UICONTROL Connect to Google Big Query]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales de BigQuery. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta BigQuery con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta GBQ. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
