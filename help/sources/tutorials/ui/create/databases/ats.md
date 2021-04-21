---
keywords: Experience Platform;inicio;temas populares;Azure Table Storage;almacenamiento de tablas azure;ats;ATS
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de tablas de Azure en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Table Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure Table Storage] en la interfaz de usuario

>[!NOTE]
>
>El conector [!DNL Azure Table Storage] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Azure Table Storage] (en adelante denominado &quot;ATS&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión ATS válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Para acceder a su cuenta ATS en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena de conexión para conectarse a la instancia [!DNL Azure Table Storage]. La cadena de conexión para conectarse a la instancia ATS. El patrón de cadena de conexión para ATS es `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Azure Table Storage] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Conecte su cuenta [!DNL Azure Table Storage]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de ATS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Azure Table Storage]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector ATS.

![catálogo](../../../../images/tutorials/create/ats/catalog.png)

Aparece la página **[!UICONTROL Connect to Azure Table Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales de ATS. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/ats/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta ATS con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de ATS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
