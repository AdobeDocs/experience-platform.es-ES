---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Fuente de la zona de aterrizaje de datos
topic-legacy: overview
description: Obtenga información sobre cómo conectar la zona de aterrizaje de datos a Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento de información aprovisionada por Adobe Experience Platform, lo que le permite acceder a un servicio de almacenamiento de archivos seguro y basado en la nube para introducir archivos en Platform. Tiene acceso a uno [!DNL Data Landing Zone] contenedores por entorno limitado, y el volumen total de datos en todos los contenedores se limita a los datos totales proporcionados con la licencia de productos y servicios de Platform. Todos los clientes de Platform y sus servicios de aplicación, como [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]y [!DNL Adobe Real-Time Customer Data Platform] se aprovisionan con uno [!DNL Data Landing Zone] contenedor por simulador de pruebas. Puede leer y escribir archivos en el contenedor a través de [!DNL Azure Storage Explorer] o su interfaz de línea de comandos.

[!DNL Data Landing Zone] admite la autenticación basada en SAS y sus datos están protegidos con [!DNL Azure Blob] mecanismos de seguridad del almacenamiento en reposo y en tránsito. La autenticación basada en SAS le permite acceder de forma segura a su [!DNL Data Landing Zone] a través de una conexión pública a Internet. No se requieren cambios de red para acceder a su [!DNL Data Landing Zone] contenedor, lo que significa que no necesita configurar ninguna lista de permitidos o configuración entre regiones para su red. Platform exige un tiempo de caducidad estricto de siete días en todos los archivos cargados en un [!DNL Data Landing Zone] contenedor. Todos los archivos se eliminan al cabo de siete días.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar los archivos o directorios de almacenamiento en la nube.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Puntos de código como `\uE000`, aunque válido en nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (como `0x00` a `0x1F`, `\u0081`, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).

## Administre el contenido de su [!DNL Data Landing Zone]

Puede usar [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) para administrar el contenido de su [!DNL Data Landing Zone] contenedor.

En el [!DNL Azure Storage Explorer] En la interfaz de usuario, seleccione el icono de conexión en el panel de navegación izquierdo. La variable **Seleccionar recurso** , proporcionando las opciones a las que conectarse. Select **[!DNL Blob container]** para conectarse a [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

A continuación, seleccione **URL de firma de acceso compartido (SAS)** como método de conexión y, a continuación, seleccione **Siguiente**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

Después de seleccionar el método de conexión, debe proporcionar una **nombre para mostrar** y **[!DNL Blob]URL de contenedor SAS** que corresponde a su [!DNL Data Landing Zone] contenedor.

>[!TIP]
>
>Puede recuperar su [!DNL Data Landing Zone] credenciales del catálogo de fuentes en la interfaz de usuario de Platform.

Proporcione su [!DNL Data Landing Zone] Dirección URL de SAS y, a continuación, seleccione **Siguiente**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

La variable **Resumen** , que le proporciona una descripción general de la configuración, incluida información sobre [!DNL Blob] y permisos. Cuando esté listo, seleccione **Connect**.

![summary](../../images/tutorials/create/dlz/summary.png)

Una conexión correcta actualiza su [!DNL Azure Storage Explorer] La interfaz de usuario de [!DNL Data Landing Zone] contenedor.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

Con [!DNL Data Landing Zone] contenedor conectado a [!DNL Azure Storage Explorer], ahora puede empezar a cargar archivos en su [!DNL Data Landing Zone] contenedor. Para cargar, seleccione **Cargar** y, a continuación, seleccione **Cargar archivos**.

![cargar](../../images/tutorials/create/dlz/upload.png)

Una vez que haya seleccionado el archivo que desea cargar, debe identificar la variable [!DNL Blob] escriba que desea cargarlo como y el directorio de destino deseado. Cuando termine, seleccione **Cargar**.

| [!DNL Blob] tipos | Descripción |
| --- | --- |
| Bloque [!DNL Blob] | Bloque [!DNL Blobs] están optimizados para cargar grandes cantidades de datos de forma eficaz. Bloque [!DNL Blobs] son la opción predeterminada para [!DNL Data Landing Zone]. |
| Anexar [!DNL Blob] | Anexar [!DNL Blobs] están optimizados para anexar datos al final del archivo. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Cargue archivos en su [!DNL Data Landing Zone] uso de la interfaz de la línea de comandos

También puede utilizar la interfaz de línea de comandos del dispositivo y acceder a los archivos de carga del [!DNL Data Landing Zone].

### Cargar un archivo mediante Bash

El siguiente ejemplo utiliza Bash y cURL para cargar un archivo en un [!DNL Data Landing Zone] con la variable [!DNL Azure Blob Storage] API de REST:

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

### Cargar un archivo con Python

El siguiente ejemplo utiliza [!DNL Microsoft's] SDK de Python v12 para cargar un archivo en un [!DNL Data Landing Zone]:

>[!TIP]
>
>Mientras que el ejemplo siguiente utiliza el URI SAS completo para conectarse a un [!DNL Azure Blob] , puede utilizar otros métodos y operaciones para autenticarse. Consulte esta [[!DNL Microsoft] documento sobre el SDK de Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) para obtener más información.

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

El siguiente ejemplo utiliza [!DNL Microsoft's] [!DNL AzCopy] utilidad para cargar un archivo en un [!DNL Data Landing Zone]:

>[!TIP]
>
>Mientras que el ejemplo siguiente está usando la variable `copy` puede utilizar otros comandos y opciones para cargar un archivo en su [!DNL Data Landing Zone], usando [!DNL AzCopy]. Consulte esta [[!DNL Microsoft AzCopy] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) para obtener más información.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connect [!DNL Data Landing Zone] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo obtener datos de su [!DNL Data Landing Zone] contenedor para Adobe Experience Platform mediante API o la interfaz de usuario.

### Uso de API

- [Cree un [!DNL Data Landing Zone] conexión de origen mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para un origen de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Connect [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Crear un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/batch/cloud-storage.md)
