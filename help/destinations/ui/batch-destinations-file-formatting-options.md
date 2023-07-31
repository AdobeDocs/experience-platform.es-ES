---
description: Obtenga información sobre cómo configurar las opciones de formato de archivo al activar datos en destinos basados en archivos
title: (Beta) Configurar las opciones de formato de archivo para los destinos basados en archivos
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 3b5f4abd516259402e9b3c4cfbcc17e32f18b6f5
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 19%

---

# (Beta) Configurar las opciones de formato de archivo para los destinos basados en archivos

>[!IMPORTANT]
> 
>Las opciones de formato de archivo descritas en este documento solo están disponibles actualmente para archivos CSV.

La opción para configurar varias opciones de formato de archivo para los archivos exportados está disponible al [conectar](/help/destinations/ui/connect-destination.md) a un destino basado en archivos, como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect), o [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Puede configurar varias opciones de formato de archivo para los archivos exportados mediante la interfaz de usuario de Experience Platform. Puede modificar varias propiedades de los archivos exportados para que coincidan con los requisitos del sistema de recepción de archivos de su lado, a fin de leer e interpretar de forma óptima los archivos recibidos del Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuración de formato de archivo para archivos CSV {#file-configuration}

Para mostrar las opciones de formato de archivo, inicie [conectar con destino](/help/destinations/ui/connect-destination.md) flujo de trabajo. Seleccionar **Tipo de datos: Segmentos** y **Tipo de archivo: CSV** para mostrar la configuración de formato de archivo disponible para el `CSV` archivos.

>[!IMPORTANT]
>
>Es posible que el destino al que se está conectando no tenga todas estas opciones disponibles. Depende del desarrollador de destino determinar qué opciones de formato de archivo desea admitir en su destino. El desarrollador de destino puede determinar qué opciones están disponibles al conectarse al destino. Las opciones requeridas se marcan con un asterisco en la interfaz de usuario de Experience Platform.
> 
>Los destinos de almacenamiento en la nube creados en Adobe: [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Zona de aterrizaje de datos](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [Almacenamiento de Google Cloud](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - actualmente solo admite las seis opciones de CSV que se resaltan a continuación.

![Imagen que muestra algunas de las opciones de formato de archivo disponibles.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitador"
>abstract="Utilice este control para establecer un separador para cada campo y valor. Vea la documentación para ver ejemplos de cada selección."

Utilice este control para definir un separador para cada campo y valor de los archivos CSV exportados. Entre las opciones disponibles se encuentran:

* Dos puntos `(:)`
* Coma `(,)`
* Barra vertical `(|)`
* Punto y coma `(;)`
* Tabulación `(\t)`

#### Ejemplos

Vea los ejemplos siguientes del contenido en los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL Dos puntos`(:)`]** seleccionados: `male:John:Doe`
* Ejemplo de salida con **[!UICONTROL Coma`(,)`]** seleccionados: `male,John,Doe`
* Ejemplo de salida con **[!UICONTROL Tubería`(|)`]** seleccionados: `male|John|Doe`
* Ejemplo de salida con **[!UICONTROL Punto y coma`(;)`]** seleccionados: `male;John;Doe`
* Ejemplo de salida con **[!UICONTROL Ficha`(\t)`]** seleccionados: `male \t John \t Doe`

### Carácter de comillas {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Carácter de comillas"
>abstract="Utilice esta opción si desea quitar las comillas dobles de las cadenas exportadas. Vea la documentación para ver ejemplos de cada selección."

Utilice esta opción si desea quitar las comillas dobles de las cadenas exportadas. Entre las opciones disponibles se encuentran:

* **[!UICONTROL Carácter nulo (\0000)]**. Utilice esta opción para eliminar comillas dobles de los archivos CSV exportados.
* **[!UICONTROL Comillas dobles (&quot;)]**. Utilice esta opción para mantener las comillas dobles en los archivos CSV exportados.

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL Carácter nulo (\0000)]** seleccionados: `Test,John,LastName`
* Ejemplo de salida con **[!UICONTROL Comillas dobles (&quot;)]** seleccionados: `"Test","John","LastName"`

### Carácter de escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Carácter de escape"
>abstract="Define un carácter único que se utiliza para las comillas de escape dentro de un valor ya entrecomillado. Vea la documentación para ver ejemplos de cada selección."

Utilice esta opción para establecer un solo carácter para las comillas de escape dentro de un valor ya citado. Por ejemplo, esta opción es útil cuando tiene una cadena entre comillas dobles donde parte de la cadena ya está entre comillas dobles. Esta opción determina con qué carácter se reemplazarán las comillas dobles interiores. Entre las opciones disponibles se encuentran:

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

* **[!UICONTROL Nulo (nulo)]**
* **Cadena vacía entre comillas dobles (&quot;&quot;)**
* **[!UICONTROL Cadena vacía]**

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL null]** seleccionados: `male,NULL,TestLastName`. En este caso, Experience Platform transforma el valor vacío en un valor nulo.
* Ejemplo de salida con **&quot;&quot;** seleccionados: `male,"",TestLastName`. En este caso, Experience Platform transforma el valor vacío en un par de comillas dobles.
* Ejemplo de salida con **[!UICONTROL Cadena vacía]** seleccionados: `male,,TestLastName`. En este caso, el Experience Platform mantiene el valor vacío y lo exporta tal cual (sin comillas dobles).

>[!TIP]
>
>La diferencia entre el resultado del valor vacío y el resultado del valor nulo en la sección siguiente es que un valor vacío tiene un valor real que está vacío. El valor NULL no tiene ningún valor. Piense en el valor vacío como un vaso vacío en la tabla y en el valor nulo como si no tuviera el vaso en la tabla.

### Salida de valor nulo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Salida de valor nulo"
>abstract="Utilice este control para establecer la representación de cadena de un valor nulo dentro de los archivos exportados. Vea la documentación para ver ejemplos de cada selección."

Utilice este control para establecer la representación de cadena de un valor nulo dentro de los archivos exportados. Esta opción determina cómo se representan los valores nulos en los archivos CSV exportados. Entre las opciones disponibles se encuentran:

* **[!UICONTROL Nulo (nulo)]**
* **Cadena vacía entre comillas dobles (&quot;&quot;)**
* **[!UICONTROL Cadena vacía]**

#### Ejemplos

Vea los ejemplos siguientes del contenido de los archivos CSV exportados con cada una de las selecciones en la interfaz de usuario.

* Ejemplo de salida con **[!UICONTROL null]** seleccionados: `male,NULL,TestLastName`. En este caso, no se produce ninguna transformación y el archivo CSV contiene el valor nulo.
* Ejemplo de salida con **&quot;&quot;** seleccionados: `male,"",TestLastName`. En este caso, Experience Platform reemplaza el valor nulo con comillas dobles alrededor de una cadena vacía.
* Ejemplo de salida con **[!UICONTROL Cadena vacía]** seleccionados: `male,,TestLastName`. En este caso, Experience Platform reemplaza el valor nulo con una cadena vacía (sin comillas dobles).

### Formato de compresión {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato de compresión"
>abstract="Define qué tipo de compresión se utilizará al guardar datos en un archivo. Las opciones compatibles son GZIP y NONE. Vea la documentación para ver ejemplos de cada selección."

Define qué tipo de compresión se utilizará al guardar datos en un archivo. Las opciones compatibles son GZIP y NONE. Esta opción determina si va a exportar archivos comprimidos o no.

### Codificación

*No se muestra en la captura de pantalla IU*. Especifica la codificación (conjunto de caracteres) de los archivos CSV guardados. Las opciones son UTF-8 o UTF-16.

### Casilla de escape

*No se muestra en la captura de pantalla IU*. Un indicador que indica si los valores que contienen comillas siempre deben incluirse entre comillas.

El valor predeterminado es omitir todos los valores que contengan un carácter de comillas.

### Separador de líneas

*No se muestra en la captura de pantalla IU*. Define el separador de líneas que se debe utilizar para escribir. La longitud máxima es de 1 carácter.

### Ignorar espacio inicial

*No se muestra en la captura de pantalla IU*. Un indicador que indica si se deben omitir o no los espacios en blanco iniciales de los valores exportados.

Ejemplo de salida con **[!UICONTROL Verdadero]** seleccionados: `"male","John","TestLastName"`
Ejemplo de salida con **[!UICONTROL Falso]** seleccionados: `" male","John","TestLastName"`

### Ignorar espacio final

No se muestra en la captura de pantalla de la IU. Un indicador que indica si se deben omitir o no los espacios en blanco finales de los valores exportados.

Ejemplo de salida con **[!UICONTROL Verdadero]** seleccionados: `"male","John","TestLastName"`
Ejemplo de salida con **[!UICONTROL Falso]** seleccionados: `"male ","John","TestLastName"`

### Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo configurar las opciones de exportación de archivos para los archivos de datos CSV a fin de adaptar el contenido del archivo a los requisitos del sistema de recepción de archivos descendente. A continuación, puede leer el [tutorial de activación de destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md) para comenzar a exportar archivos a su ubicación de almacenamiento en la nube preferida.
