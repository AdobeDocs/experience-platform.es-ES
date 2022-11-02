---
description: Obtenga información sobre cómo configurar las opciones de formato de archivo al activar datos en destinos basados en archivos
title: (Beta) Configurar opciones de formato de archivo para destinos basados en archivos
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# (Beta) Configurar opciones de formato de archivo para destinos basados en archivos

>[!IMPORTANT]
>
>La variable **[!UICONTROL Opciones de formato de archivo]** en Adobe Experience Platform se encuentra en versión beta. La documentación y la funcionalidad están sujetas a cambios.
>Póngase en contacto con su representante de Adobe para obtener acceso a esta funcionalidad.
> 
>Las opciones de formato de archivo descritas en este documento están disponibles actualmente solo para archivos CSV.

La opción para configurar varias opciones de formato de archivo para los archivos exportados está disponible cuando [connect](/help/destinations/ui/connect-destination.md) a un destino basado en archivos, como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)o [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Puede configurar varias opciones de formato de archivo para los archivos exportados mediante la IU del Experience Platform. Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos de su lado, a fin de leer e interpretar de forma óptima los archivos recibidos del Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuración de formato de archivo {#file-configuration}

>[!IMPORTANT]
>
>Es posible que el destino al que se está conectando no tenga todas estas opciones disponibles. Depende del desarrollador de destino determinar qué opciones de formato de archivo desea admitir en su destino. El desarrollador de destino puede determinar qué opciones están disponibles al conectarse al destino. Las opciones necesarias se marcan con un asterisco en la IU del Experience Platform.

Para mostrar las opciones de formato del archivo, inicie el [conectar con destino](/help/destinations/ui/connect-destination.md) flujo de trabajo y seleccione segmentos como **Tipo de archivo**. En esta sección se describe la configuración de formato de archivo disponible para la exportación `CSV` archivos.

![Imagen que muestra algunas de las opciones de formato de archivo disponibles.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador

Define un separador para cada campo y valor. Por ejemplo, `,` para valores separados por comas o `/t` para valores separados por tabulaciones.

### Carácter de comillas

Define un carácter único que se utiliza para escapar los valores entre comillas, donde el separador puede formar parte del valor.

### Carácter de escape

Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya citado.

### Salida de valor vacío

Define la representación de cadena de un valor vacío.

### Salida de valor nulo

Define la representación de cadena de un valor nulo dentro de los archivos exportados.

Ejemplo de salida con **[!UICONTROL null]** seleccionados: `male,NULL,TestLastName`
Ejemplo de salida con **&quot;&quot;** seleccionados: `male,"",TestLastName`
Ejemplo de salida con **[!UICONTROL Cadena vacía]** seleccionados: `male,,TestLastName`

### Formato de compresión

Define qué códec de compresión se utilizará al guardar datos en un archivo. Las opciones compatibles son GZIP y NONE .

### Codificación

*No se muestra en la captura de pantalla de la interfaz de usuario*. Especifica la codificación (charset) de los archivos CSV guardados. Las opciones son UTF-8 o UTF-16.

### Cargar para omitir comillas

*No se muestra en la captura de pantalla de la interfaz de usuario*. Un indicador que indica si los valores que contienen comillas siempre deben estar entre comillas.

El valor predeterminado es omitir todos los valores que contengan un carácter de comillas.

### Separador de líneas

*No se muestra en la captura de pantalla de la interfaz de usuario*. Define el separador de líneas que debe utilizarse para escribir. La longitud máxima es 1 carácter.

### Ignorar espacios en blanco iniciales

*No se muestra en la captura de pantalla de la interfaz de usuario*. Un indicador que indica si se deben omitir los espacios en blanco iniciales de los valores que se exportan.

Ejemplo de salida con **[!UICONTROL True]** seleccionados: `"male","John","TestLastName"`
Ejemplo de salida con **[!UICONTROL False]** seleccionados: `" male","John","TestLastName"`

### Ignorar espacios en blanco finales

No se muestra en la captura de pantalla de la interfaz de usuario. Un indicador que indica si se deben omitir o no los espacios en blanco finales de los valores que se exportan.

Ejemplo de salida con **[!UICONTROL True]** seleccionados: `"male","John","TestLastName"`
Ejemplo de salida con **[!UICONTROL False]** seleccionados: `"male ","John","TestLastName"`

### Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo configurar las opciones de exportación de archivos para los archivos de datos CSV a fin de adaptar el contenido del archivo a los requisitos del sistema de recepción de archivos descendentes. A continuación, puede leer el [tutorial de activación de destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) para empezar a exportar archivos a su ubicación de almacenamiento en la nube preferida.
