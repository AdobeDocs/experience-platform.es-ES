---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Source de zona de aterrizaje de datos
description: Aprenda a conectar la zona de aterrizaje de datos a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: cb37eda87b8fcc0d0284db7a0bab8d48eab5aae6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Esta página es específica para el conector [!DNL Data Landing Zone] *source* en el Experience Platform. Para obtener información sobre cómo conectarse al conector [!DNL Data Landing Zone] *destination*, consulte la [[!DNL Data Landing Zone] página de documentación de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] es una interfaz de almacenamiento de [!DNL Azure Blob] aprovisionada por Adobe Experience Platform, que le permite acceder a una función de almacenamiento de archivos segura y basada en la nube para traer archivos a Platform. Tiene acceso a un contenedor [!DNL Data Landing Zone] por zona protegida, y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con su licencia de productos y servicios de Platform. Todos los clientes de Platform y sus aplicaciones, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] y [!DNL Adobe Real-Time Customer Data Platform], se han aprovisionado con un contenedor de [!DNL Data Landing Zone] por zona protegida. Puede leer y escribir archivos en su contenedor a través de [!DNL Azure Storage Explorer] o de la interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con mecanismos de seguridad de almacenamiento estándar de [!DNL Azure Blob] en reposo y en tránsito. La autenticación basada en SAS le permite tener acceso de forma segura a su contenedor de [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para tener acceso al contenedor de [!DNL Data Landing Zone], lo que significa que no es necesario configurar listas de permitidos ni configuraciones entre regiones para la red. Platform exige una caducidad estricta de siete días para todos los archivos cargados en un contenedor de [!DNL Data Landing Zone]. Todos los archivos se eliminan a los siete días.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar los archivos o directorios de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (como `0x00` a `0x1F`, `\u0081`, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Administrar el contenido de la zona de aterrizaje de datos{#manage-the-contents-of-your-data-landing-zone}

Puede usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para administrar el contenido de su contenedor de [!DNL Data Landing Zone].

En la interfaz de usuario de [!DNL Azure Storage Explorer], seleccione el icono de conexión en el panel de navegación izquierdo. Aparecerá la ventana **Seleccionar recurso**, que le proporcionará las opciones para conectarse a. Seleccione **[!DNL Blob container]** para conectarse a [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

A continuación, seleccione **URL de firma de acceso compartido (SAS)** como método de conexión y, a continuación, seleccione **Siguiente**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Después de seleccionar el método de conexión, debe proporcionar **nombre para mostrar** y la URL de SAS de contenedor **[!DNL Blob]** que corresponda a su contenedor [!DNL Data Landing Zone].

>[!TIP]
>
>Puede recuperar sus credenciales de [!DNL Data Landing Zone] del catálogo de fuentes en la interfaz de usuario de Platform.

Proporcione su URL SAS [!DNL Data Landing Zone] y seleccione **Siguiente**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

Aparece la ventana **Resumen**, que le proporciona una descripción general de la configuración, incluida información sobre el extremo y los permisos de [!DNL Blob]. Cuando esté listo, seleccione **Conectar**.

![resumen](../../images/tutorials/create/dlz/summary.png)

Una conexión correcta actualiza la interfaz de usuario de [!DNL Azure Storage Explorer] con el contenedor de [!DNL Data Landing Zone].

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Con el contenedor [!DNL Data Landing Zone] conectado a [!DNL Azure Storage Explorer], ahora puede empezar a cargar archivos en el contenedor [!DNL Data Landing Zone]. Para cargar, selecciona **Cargar** y luego selecciona **Cargar archivos**.

![cargar](../../images/tutorials/create/dlz/upload.png)

Una vez que haya seleccionado el archivo que desea cargar, debe identificar el tipo de [!DNL Blob] con el que desea cargarlo y el directorio de destino deseado. Cuando termine, seleccione **Cargar**.

| [!DNL Blob] tipos | Descripción |
| --- | --- |
| Bloquear [!DNL Blob] | Los bloques [!DNL Blobs] están optimizados para cargar grandes cantidades de datos de manera eficiente. El bloque [!DNL Blobs] es la opción predeterminada para [!DNL Data Landing Zone]. |
| Anexar [!DNL Blob] | Anexar [!DNL Blobs] está optimizado para anexar datos al final del archivo. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Cargar archivos en su [!DNL Data Landing Zone] mediante la interfaz de línea de comandos

También puede usar la interfaz de línea de comandos de su dispositivo y acceder a cargar archivos en su [!DNL Data Landing Zone].

### Carga de un archivo mediante Bash

El siguiente ejemplo usa Bash y cURL para cargar un archivo en un [!DNL Data Landing Zone] con la API REST [!DNL Azure Blob Storage]:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Carga de un archivo mediante Python

El siguiente ejemplo usa [!DNL Microsoft's] Python v12 SDK para cargar un archivo en un [!DNL Data Landing Zone]:

>[!TIP]
>
>Aunque el ejemplo siguiente utiliza el URI SAS completo para conectarse a un contenedor de [!DNL Azure Blob], puede utilizar otros métodos y operaciones para autenticarse. Consulte este [[!DNL Microsoft] documento sobre el SDK de Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) para obtener más información.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Cargar un archivo mediante [!DNL AzCopy]

El siguiente ejemplo utiliza la utilidad [!DNL Microsoft's] [!DNL AzCopy] para cargar un archivo en un [!DNL Data Landing Zone]:

>[!TIP]
>
>Aunque el ejemplo siguiente utiliza el comando `copy`, puede usar otros comandos y opciones para cargar un archivo en su [!DNL Data Landing Zone], usando [!DNL AzCopy]. Consulte este [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) para obtener más información.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Conectar [!DNL Data Landing Zone] a [!DNL Platform]

La siguiente documentación proporciona información sobre cómo obtener datos del contenedor de [!DNL Data Landing Zone] a Adobe Experience Platform mediante API o la interfaz de usuario.

### Uso de API

- [Crear una conexión de origen  [!DNL Data Landing Zone]  mediante la API de Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Cree un flujo de datos para una fuente de almacenamiento en la nube mediante la API de Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Uso de la IU

- [Conectar  [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Cree un flujo de datos para una conexión de almacenamiento en la nube en la IU](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>Actualmente no se admiten vínculos privados al conectarse al Experience Platform mediante [!DNL Data Landing Zone]. Los únicos métodos admitidos para el acceso son los enumerados [aquí](#manage-the-contents-of-your-data-landing-zone).

