---
keywords: Experience Platform;home;popular topics;Google Cloud Storage;google cloud storage;GCS;gcs
solution: Experience Platform
title: Conector de origen de Almacenamiento de Google Cloud (IU)
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen de Google Cloud Almacenamiento (en lo sucesivo, "GCS") mediante la interfaz de usuario de la plataforma.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---


# Creación de un conector [!DNL Google Cloud Storage] de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google Cloud Storage] (en adelante, &quot;GCS&quot;) mediante la interfaz [!DNL Platform] de usuario.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!Perfil del cliente en tiempo real de DNL]](../../../../../profile/home.md): Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión GCS válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
* Notación de objetos JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a los datos de GCS en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de clave de acceso | ID de clave de acceso de la [!DNL Google Cloud Storage] cuenta. |
| Clave de acceso secreta | El secreto de cliente de la [!DNL Google Cloud Storage] cuenta. |

Para obtener más información sobre cómo empezar, consulte la guía [de autenticación de](https://cloud.google.com/docs/authentication/production) servidor a servidor para [!DNL Google Cloud Storage].

## Conectar su [!DNL Google Cloud Storage] cuenta

Una vez recopiladas las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de GCS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Fuentes]** . La pantalla **[!UICONTROL Catálogo]** muestra una serie de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]** , seleccione Almacenamiento **[!UICONTROL de]** Google Cloud. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Aparece la página **[!UICONTROL Conectar con el Almacenamiento]** de Google Cloud. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales de GCS. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de GCS con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta GCS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).