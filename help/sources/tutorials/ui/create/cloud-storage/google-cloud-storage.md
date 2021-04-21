---
keywords: Experience Platform;inicio;temas populares;Google Cloud Storage;google cloud storage;GCS;gcs
solution: Experience Platform
title: Crear una conexión de origen de almacenamiento de Google Cloud en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de almacenamiento de Google Cloud mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Google Cloud Storage] en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Google Cloud Storage] (en adelante denominado &quot;GCS&quot;) mediante la interfaz de usuario [!DNL Platform].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión GCS válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por coma. El valor de los encabezados de campo de los archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se admitirán los archivos DSV generales.
* Notación de objeto de JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a los datos de GCS en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Acceso a ID de clave | Cadena alfanumérica de 61 caracteres utilizada para autenticar su cuenta [!DNL Google Cloud Storage] en Platform. |
| Clave de acceso secreta | Una cadena de 40 caracteres codificada en base a 64 que se utiliza para autenticar su cuenta [!DNL Google Cloud Storage] en Platform. |

Para obtener más información sobre estos valores, consulte la guía [Google Cloud Storage HMAC keys](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para ver los pasos sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte [[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Conecte su cuenta [!DNL Google Cloud Storage]

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de GCS a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo **[!UICONTROL Sources]**. La pantalla **[!UICONTROL Catalog]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Databases]**, seleccione **[!UICONTROL Google Cloud Storage]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configure]**. De lo contrario, seleccione **[!UICONTROL Add data]** para crear un nuevo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Aparece la página **[!UICONTROL Connect to Google Cloud Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL New account]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y sus credenciales de GCS. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, deje que se establezca la nueva conexión.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de GCS con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Next]** para continuar.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de GCS. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
