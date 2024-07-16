---
title: Crear una conexión de Source de Google Cloud Storage en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Cloud Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# Crear una conexión de origen [!DNL Google Cloud Storage] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de [!DNL Google Cloud Storage] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Google Cloud Storage] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite la ingesta de los siguientes formatos de archivo desde almacenes externos:

* Valores separados por delimitadores (DSV): cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* Notación de objetos de JavaScript (JSON): los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato Parquet deben ser compatibles con XDM.

### Recopilar credenciales necesarias

Para tener acceso a los datos de [!DNL Google Cloud Storage] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de clave de acceso | Cadena alfanumérica de 61 caracteres usada para autenticar su cuenta de [!DNL Google Cloud Storage] en Platform. |
| Clave de acceso secreta | Cadena de 40 caracteres codificada en base 64 que se usa para autenticar la cuenta de [!DNL Google Cloud Storage] en Platform. |
| Nombre del segmento | Nombre de su cubo de [!DNL Google Cloud Storage]. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| Ruta de carpeta | La ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estos valores, consulte la guía [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para ver los pasos sobre cómo generar tu propio identificador de clave de acceso y clave de acceso secreta, consulta la [[!DNL Google Cloud Storage] descripción general](../../../../connectors/cloud-storage/google-cloud-storage.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Google Cloud Storage] a Platform.

## Conectar su cuenta de [!DNL Google Cloud Storage]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL Almacenamiento en la nube de Google]** y luego seleccione **[!UICONTROL Agregar datos]**.

![Pantalla de IU de Platform que muestra la página del catálogo de orígenes.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Google Cloud Storage]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL Google Cloud Storage] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La pantalla de la interfaz de usuario de Platform muestra la página de la cuenta existente para un origen de Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Google Cloud Storage]. Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre de la ruta de acceso a la subcarpeta.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![La pantalla de IU de Platform muestra la nueva página de cuenta para un origen de Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Google Cloud Storage]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
