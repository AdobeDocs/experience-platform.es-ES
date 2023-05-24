---
title: Crear una conexión de origen de Google Cloud Storage en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Google Cloud Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Crear un [!DNL Google Cloud Storage] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Google Cloud Storage] conexión de origen mediante la IU de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Google Cloud Storage] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

[!DNL Experience Platform] admite la ingesta de los siguientes formatos de archivo desde almacenamientos externos:

* Valores separados por delimitadores (DSV): cualquier valor de un solo carácter puede utilizarse como delimitador para archivos de datos con formato DSV.
* Notación de objetos JavaScript (JSON): los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato Parquet deben ser compatibles con XDM.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Google Cloud Storage] En Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| ID de clave de acceso | Una cadena alfanumérica de 61 caracteres utilizada para autenticar su [!DNL Google Cloud Storage] a Platform. |
| Clave de acceso secreta | Una cadena de 40 caracteres codificada en base 64 que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform. |
| Nombre del segmento | El nombre de su [!DNL Google Cloud Storage] cubo. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| Ruta de carpeta | La ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para obtener información sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] descripción general](../../../../connectors/cloud-storage/google-cloud-storage.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Google Cloud Storage] a Platform.

## Conecte su [!DNL Google Cloud Storage] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL Almacenamiento de Google Cloud]** y luego seleccione **[!UICONTROL Añadir datos]**.

![La pantalla IU de Platform muestra la página del catálogo de fuentes.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

El **[!UICONTROL Conectar con Google Cloud Storage]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Google Cloud Storage] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La pantalla IU de Platform muestra la página de cuenta existente de un origen de Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Google Cloud Storage] credenciales. Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre de la ruta de acceso a la subcarpeta.

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La pantalla IU de Platform muestra la nueva página de cuenta de un origen de Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Google Cloud Storage] cuenta. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
