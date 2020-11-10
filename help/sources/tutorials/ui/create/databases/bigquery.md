---
keywords: Experience Platform;home;popular topics;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Creación de un conector de origen de Google Big Consulta en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen de Google Big Consulta (en adelante, "GBQ") mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Creación de un conector [!DNL Google Big Query] de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Google BigQuery] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google Big Query] (denominado en adelante &quot;GBQ&quot;) mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión GBQ válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta GBQ en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | ID de proyecto del [!DNL BigQuery] proyecto predeterminado con el que se realizará la consulta. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El autentificador de actualización obtenido de [!DNL Google] utilizado para autorizar el acceso a [!DNL BigQuery]. |

Para obtener más información sobre estos valores, consulte [este documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Conectar su cuenta GBQ

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta GBQ a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases]** de datos, seleccione **[!UICONTROL Google Big Consulta]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector GBQ.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Aparece la página **[!UICONTROL Conectar con la Consulta]** principal de Google. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales GBQ. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta GBQ con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta GBQ. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incluir [!DNL Platform]](../../dataflow/databases.md)datos.