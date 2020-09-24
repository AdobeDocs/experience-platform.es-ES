---
keywords: Experience Platform;home;popular topics;Azure Blob;azure blob;Azure blob connector
solution: Experience Platform
title: Creación de un conector de origen de blob de Azure en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un blob de Azure (en adelante denominado "Blob") mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Creación de un conector [!DNL Azure Blob] de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un [!DNL Azure Blob] (en adelante denominado &quot;[!DNL Blob]&quot;) mediante la interfaz de [!DNL Platform] usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [!DNL Blob] configuración de un flujo de datos [](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
- Notación de objetos JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
- Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Blob] almacenamiento en [!DNL Platform], debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión necesaria para acceder a los datos del almacenamiento Blob. El patrón de cadena de [!DNL Blob] conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obtener más información sobre cómo empezar, visite [ [!DNL Azure Blob] este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

## Conectar la cuenta de Blob

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Blob] cuenta a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]** , seleccione Almacenamiento **[!UICONTROL de]** Azure Blob. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo [!DNL Blob]conector.

![catálogo](../../../../images/tutorials/create/blob/catalog.png)

Aparece la página **[!UICONTROL Conectar con el Almacenamiento]** de blob de Azure. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus [!DNL Blob] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/blob/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Blob] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/blob/existing.png)

## Próximos pasos y recursos adicionales

Siguiendo este tutorial, ha establecido una conexión con su [!DNL Blob] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).