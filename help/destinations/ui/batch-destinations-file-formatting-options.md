---
description: Obtenga información sobre cómo configurar las opciones de formato de archivo al activar datos en destinos basados en archivos
title: (Beta) Configurar opciones de formato de archivo para destinos basados en archivos
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 19%

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

## Configuración del formato de archivo para archivos CSV {#file-configuration}

Para mostrar las opciones de formato del archivo, inicie el [conectar con destino](/help/destinations/ui/connect-destination.md) flujo de trabajo. Select **Tipo de datos: Segmentos** y **Tipo de archivo: CSV** para mostrar la configuración de formato de archivo disponible para la exportación `CSV` archivos.

>[!IMPORTANT]
>
>Es posible que el destino al que se está conectando no tenga todas estas opciones disponibles. Depende del desarrollador de destino determinar qué opciones de formato de archivo desea admitir en su destino. El desarrollador de destino puede determinar qué opciones están disponibles al conectarse al destino. Las opciones necesarias se marcan con un asterisco en la IU del Experience Platform.
> 
>Los nuevos destinos de almacenamiento en la nube: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Almacenamiento de Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrizaje de datos](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Almacenamiento en la nube de Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) : actualmente solo admite las seis opciones de CSV que se indican a continuación.

![Imagen que muestra algunas de las opciones de formato de archivo disponibles.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitador"
>abstract="Utilice este control para establecer un separador para cada campo y valor. Vea la documentación para ver ejemplos de cada selección."

Utilice este control para establecer un separador para cada campo y valor de los archivos CSV exportados. Entre las opciones disponibles se encuentran:

* Dos puntos `(:)`
* Coma `(,)`
* Barra vertical `(|)`
* Punto y coma `(;)`
* Tabulación `(\t)`

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL Dos puntos`(:)`]** seleccionados: `male:John:Doe`
* Ejemplo de salida con **[!UICONTROL Coma`(,)`]** seleccionados: `male,John,Doe`
* Ejemplo de salida con **[!UICONTROL Tubería`(|)`]** seleccionados: `male|John|Doe`
* Ejemplo de salida con **[!UICONTROL Punto y coma`(;)`]** seleccionados: `male;John;Doe`
* Ejemplo de salida con **[!UICONTROL Tabulación`(\t)`]** seleccionados: `male \t John \t Doe`

### Carácter de comillas {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Carácter de comillas"
>abstract="Utilice esta opción si desea quitar las comillas dobles de las cadenas exportadas. Vea la documentación para ver ejemplos de cada selección."

Utilice esta opción si desea quitar las comillas dobles de las cadenas exportadas. Entre las opciones disponibles se encuentran:

* **[!UICONTROL Carácter nulo (\0000)]**. Utilice esta opción para eliminar las comillas dobles de los archivos CSV exportados.
* **[!UICONTROL Comillas dobles (&quot;)]**. Utilice esta opción para mantener comillas dobles en los archivos CSV exportados.

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL Carácter nulo (\0000)]** seleccionados: `Test,John,LastName`
* Ejemplo de salida con **[!UICONTROL Comillas dobles (&quot;)]** seleccionados: `"Test","John","LastName"`

### Carácter de escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Carácter de escape"
>abstract="Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya entrecomillado. Vea la documentación para ver ejemplos de cada selección."

Utilice esta opción para definir un carácter único para comillas de escape dentro de un valor ya citado. Por ejemplo, esta opción es útil cuando tiene una cadena entre comillas dobles donde parte de la cadena ya está entre comillas dobles. Esta opción determina con qué carácter se reemplazarán las comillas dobles interiores. Entre las opciones disponibles se encuentran:

* Barra invertida `(\)`
* Comilla simple `(')`

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL Barra invertida`(\)`]** seleccionados: `"Test,\"John\",LastName"`
* Ejemplo de salida con **[!UICONTROL Comilla simple`(')`]** seleccionados: `"Test,'"John'",LastName"`

### Salida de valor vacío {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Salida de valor vacío"
>abstract="Utilice esta opción para establecer cómo se deben representar los valores vacíos en los archivos CSV exportados. Vea la documentación para ver ejemplos de cada selección."

Utilice este control para establecer la representación de cadena de un valor vacío. Esta opción determina cómo se representan los valores vacíos en los archivos CSV exportados. Entre las opciones disponibles se encuentran:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Cadena vacía]**

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL null]** seleccionados: `male,NULL,TestLastName`. En este caso, el Experience Platform transforma el valor vacío en un valor nulo.
* Ejemplo de salida con **&quot;&quot;** seleccionados: `male,"",TestLastName`. En este caso, el Experience Platform transforma el valor vacío en un par de comillas dobles.
* Ejemplo de salida con **[!UICONTROL Cadena vacía]** seleccionados: `male,,TestLastName`. En este caso, el Experience Platform mantiene el valor vacío y lo exporta tal cual (sin comillas dobles).

>[!TIP]
>
>La diferencia entre el resultado del valor vacío y el resultado del valor nulo en la sección siguiente es que un valor vacío tiene un valor real que está vacío. El valor NULL no tiene ningún valor. Considere el valor vacío como un vaso vacío en la tabla y el valor nulo como si no tuviera el vidrio en la mesa.

### Salida de valor nulo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Salida de valor nulo"
>abstract="Utilice este control para establecer la representación de cadena de un valor nulo dentro de los archivos exportados. Vea la documentación para ver ejemplos de cada selección."

Utilice este control para establecer la representación de cadena de un valor nulo dentro de los archivos exportados. Esta opción determina cómo se representan los valores nulos en los archivos CSV exportados. Entre las opciones disponibles se encuentran:

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL Cadena vacía]**

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL null]** seleccionados: `male,NULL,TestLastName`. En este caso, no se produce ninguna transformación y el archivo CSV contiene el valor nulo.
* Ejemplo de salida con **&quot;&quot;** seleccionados: `male,"",TestLastName`. En este caso, Experience Platform reemplaza el valor nulo con comillas dobles alrededor de una cadena vacía.
* Ejemplo de salida con **[!UICONTROL Cadena vacía]** seleccionados: `male,,TestLastName`. En este caso, Experience Platform reemplaza el valor nulo por una cadena vacía (sin comillas dobles).

### Formato de compresión {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato de compresión"
>abstract="Define qué tipo de compresión se utilizará al guardar datos en un archivo. Las opciones compatibles son GZIP y NONE. Vea la documentación para ver ejemplos de cada selección."

Define qué tipo de compresión se utilizará al guardar datos en un archivo. Las opciones compatibles son GZIP y NONE. Esta opción determina si se exportarán o no archivos comprimidos.

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
