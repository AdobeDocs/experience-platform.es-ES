---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen FTP o SFTP en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creación de un conector de origen FTP o SFTP en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos externos de forma programada. Este tutorial proporciona los pasos para crear un conector de origen FTP o SFTP mediante la interfaz de usuario de la plataforma.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)de modelo de datos de experiencia (XDM): Marco normalizado mediante el cual la plataforma de experiencias organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [Perfil](../../../../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una conexión FTP o SFTP válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/cloud-storage.md).

### Formatos de archivo compatibles

La plataforma de experiencia admite los siguientes formatos de archivo para la ingesta desde fuentes externas:

* Valores separados por delimitadores (DSV): Actualmente, la compatibilidad con archivos de datos con formato DSV está limitada a valores separados por comas (CSV). El valor de los encabezados de campo dentro de archivos con formato DSV solo debe consistir en caracteres alfanuméricos y guiones bajos. En el futuro se prestará apoyo al DSV general.
* Notación de objetos JavaScript (JSON): Los archivos de datos con formato JSON deben ser compatibles con XDM.
* Apache Parquet: Los archivos de datos con formato de parqué deben ser compatibles con XDM.

### Recopilar las credenciales necesarias

Para acceder al servidor FTP o SFTP en la plataforma, debe proporcionar el nombre **de** host del servidor, un nombre **de** usuario y una **contraseña**.

## Conectar con el servidor

Con las credenciales del servidor listas, puede seguir los pasos a continuación para crear una nueva conexión de base de entrada para vincular el servidor FTP o SFTP a la plataforma.

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo de fuentes. La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de base de entrada y cada origen muestra el número de conexiones de base existentes asociadas a ellos.

En la categoría *Cloud Almacenamiento* , seleccione **FTP** o **SFTP** para mostrar una barra de información en la parte derecha de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para la vista de la documentación o la conexión con la fuente. Para crear una nueva conexión base de entrada, haga clic en **Conectar origen**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

En el formulario de entrada, proporcione la conexión base con un nombre, una descripción opcional y sus credenciales de FTP o SFTP. Por último, haga clic en **Conectar** y, a continuación, espere un poco de tiempo para que se establezca la nueva conexión base.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

Una vez establecida la conexión de base con el servidor FTP o SFTP, puede continuar en la siguiente sección y configurar un flujo de datos para llevar datos a Platform.

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su servidor FTP o SFTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos a Platform](../../dataflow/cloud-storage.md).
