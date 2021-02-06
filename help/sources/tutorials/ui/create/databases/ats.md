---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de tabla de Azure;almacenamiento de tabla de Azure;ats;ATS
solution: Experience Platform
title: Creación de una conexión de origen de Almacenamiento de tabla de Azure en la interfaz de usuario
topic: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Almacenamiento de tabla de Azure mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# Crear una conexión de origen [!DNL Azure Table Storage] en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Azure Table Storage] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Azure Table Storage] (en adelante denominado &quot;ATS&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión ATS válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta de ATS en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena de conexión para conectarse a la instancia [!DNL Azure Table Storage]. La cadena de conexión que se conecta a la instancia de ATS. El patrón de cadena de conexión para ATS es `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obtener más información sobre cómo empezar, consulte [this [!DNL Azure Table Storage] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Conectar su cuenta [!DNL Azure Table Storage]

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de ATS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Almacenamiento de tabla de Azure]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector ATS.

![catálogo](../../../../images/tutorials/create/ats/catalog.png)

Aparece la página **[!UICONTROL Conectar con el Almacenamiento de tabla de Azure]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales de ATS. Cuando termine, seleccione **[!UICONTROL Conectar]** y, a continuación, deje transcurrir algún tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ats/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta ATS con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de ATS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a [!DNL Platform]](../../dataflow/databases.md).