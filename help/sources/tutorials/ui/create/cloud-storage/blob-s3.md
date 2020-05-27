---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Azure Blob o Amazon S3 en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---


# Creación de un conector de origen de Azure Blob o Amazon S3 en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen de Azure Blob (en adelante denominado &quot;Blob&quot;) o Amazon S3 (en adelante denominado &quot;S3&quot;) mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   - [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
- [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión base Blob o S3, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Formatos de archivo compatibles

La plataforma de experiencia admite los siguientes formatos de archivo para la ingesta desde almacenamientos externos:

- Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas. El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se proporcionará compatibilidad con archivos DSV generales.
- Notación de objetos JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
- Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder a su almacenamiento Blob en la plataforma, debe proporcionar un valor válido para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión necesaria para acceder a los datos del almacenamiento Blob. El patrón de la cadena de conexión Blob es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obtener más información sobre cómo empezar, visite [este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)de Azure Blob.

Del mismo modo, el acceso al bucket S3 en la plataforma requiere que proporcione los valores válidos para las siguientes credenciales:

| Credencial | Descripción |
| ---------- | ----------- |
| `s3AccessKey` | ID de la clave de acceso para el almacenamiento S3. |
| `s3SecretKey` | ID de clave secreta para el almacenamiento S3. |

Para obtener más información sobre cómo empezar, visite [este documento](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)de AWS.

## Conectar la cuenta de Blob o S3

Con las credenciales del almacenamiento de nube listas, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular la cuenta de Blob o S3 a Platform.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo de fuentes. La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *Cloud Almacenamiento* , seleccione **Azure Blob Almacenamiento** o **Amazon S3** para mostrar una barra de información en la parte derecha de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para la vista de la documentación o la conexión con la fuente. Para crear una nueva conexión base de entrada, haga clic en **Conectar origen**.

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

En el formulario de entrada, proporcione la conexión base con un nombre, una descripción opcional y las credenciales de Blob o S3. Por último, haga clic en **Conectar** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión base a su cuenta de Azure Blob o Amazon S3. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/batch/cloud-storage.md).