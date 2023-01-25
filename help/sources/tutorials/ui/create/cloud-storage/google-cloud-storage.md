---
title: Crear una conexión de origen de almacenamiento en la nube de Google en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Cloud Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Cree un [!DNL Google Cloud Storage] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Google Cloud Storage] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL Google Cloud Storage] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite los siguientes formatos de archivo que se van a introducir desde almacenes externos:

* Valores separados por delimitadores (DSV): Cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* Notación de objeto de JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Google Cloud Storage] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Acceso a ID de clave | Una cadena alfanumérica de 61 caracteres que se usa para autenticar su [!DNL Google Cloud Storage] a Platform. |
| Clave de acceso secreta | Una cadena de 40 caracteres codificada en base a 64 que se usa para autenticar su [!DNL Google Cloud Storage] a Platform. |
| Nombre del depósito | El nombre de su [!DNL Google Cloud Storage] cubo. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| Ruta de carpeta | Ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para ver los pasos sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] información general](../../../../connectors/cloud-storage/google-cloud-storage.md).

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Google Cloud Storage] a Platform.

## Conecte su [!DNL Google Cloud Storage] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccione **[!UICONTROL Almacenamiento en la nube de Google]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![La pantalla de la interfaz de usuario de Platform muestra la página del catálogo de fuentes.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

La variable **[!UICONTROL Conectarse a Google Cloud Storage]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL Google Cloud Storage] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La pantalla de la interfaz de usuario de Platform muestra la página de cuenta existente para una fuente de almacenamiento en la nube de Google](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL Google Cloud Storage] credenciales. Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre de la ruta a la subcarpeta.

Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![La pantalla de la interfaz de usuario de Platform muestra la nueva página de cuenta de una fuente de Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Google Cloud Storage] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
