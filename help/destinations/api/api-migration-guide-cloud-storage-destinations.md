---
solution: Experience Platform
title: Guía de migración de API para destinos de almacenamiento en la nube
description: Obtenga información acerca de los cambios en el flujo de trabajo para activar los destinos de almacenamiento en la nube como parte de la migración a las nuevas tarjetas de destino de almacenamiento en la nube con funcionalidad adicional.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: b651d15260adbcd37fa396fa0b325a9674a92133
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Guía de migración de API para destinos de almacenamiento en la nube

>[!IMPORTANT]
>
>* La funcionalidad descrita en esta página está disponible para los clientes que han adquirido los paquetes Real-Time CDP Prime y Ultimate. Póngase en contacto con el representante del Adobe para obtener más información.

## Contexto de migración {#migration-context}

Inicio [Octubre de 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations), puede utilizar las nuevas funciones de exportación de archivos para acceder a la funcionalidad de personalización mejorada al exportar archivos fuera del Experience Platform:

* Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través de [nuevo paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Capacidad para seleccionar [tipo de archivo](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) del archivo exportado.
* Capacidad para [personalizar el formato de los archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Esta funcionalidad es compatible con las tarjetas de almacenamiento en la nube beta que se enumeran a continuación:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Tenga en cuenta que, actualmente en la interfaz de usuario de Experience Platform, puede ver dos tarjetas de destino en paralelo de los tres destinos. A continuación se muestran las [!DNL Amazon S3] destinos nuevos y heredados. En todos los casos, las tarjetas marcadas con **Beta** son las nuevas tarjetas de destino.

![Imagen de las dos tarjetas de destino de Amazon S3 en una vista en paralelo.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Aunque estos destinos con funcionalidad mejorada se ofrecieron inicialmente como una versión beta, *El Adobe ahora está trasladando a todos los clientes de Real-Time CDP a los nuevos destinos de almacenamiento en la nube*. Para clientes que ya estaban utilizando [!DNL Amazon S3], [!DNL Azure Blob], o SFTP, esto significa que los flujos de datos existentes se migrarán a las nuevas tarjetas. Siga leyendo para obtener más información sobre los cambios específicos como parte de la migración.

## A quién se aplica esta página {#who-this-applies-to}

Si ya está utilizando [API de Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/) para exportar perfiles a los destinos de almacenamiento en la nube de Amazon S3, Azure Blob o SFTP, se le aplica esta guía de migración de API.

Si tiene scripts ejecutándose en su [!DNL Amazon S3], [!DNL Azure Blob], o las ubicaciones de almacenamiento en la nube SFTP sobre los archivos exportados desde el Experience Platform, tenga en cuenta que algunos parámetros cambian con respecto a las especificaciones de conexión y flujo de las nuevas tarjetas, así como con respecto al paso de asignación.

Por ejemplo, si estuviera utilizando una secuencia de comandos para filtrar los flujos de datos de destino a [!DNL Amazon S3] destino, según las especificaciones de conexión del [!DNL Amazon S3] destino, tenga en cuenta que las especificaciones de conexión cambiarán, por lo que deberá actualizar los filtros.

## Vínculos de documentación relevantes {#relevant-documentation-links}

Esta sección incluye el tutorial de API y la documentación de referencia relevantes para la funcionalidad mejorada de exportación de datos a destinos de almacenamiento en la nube.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [Tutorial de API para exportar segmentos a destinos de almacenamiento en la nube](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Documentación de referencia de la API del servicio de flujo Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Resumen de cambios incompatibles con versiones anteriores {#summary-backwards-incompatible-changes}

Con la migración a los nuevos destinos, todos los flujos de datos existentes a [!DNL Amazon S3], [!DNL Azure Blob]Los destinos SFTP y ahora se asignarán a nuevas conexiones de destino y conexiones base. El paso de asignación de perfiles también cambia. Los cambios incompatibles con versiones anteriores se resumen en las secciones siguientes para cada destino. Vea también la [glosario de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) para obtener más información sobre los términos del diagrama siguiente.

![Imagen de información general de guía de migración](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Cambios incompatibles con versiones anteriores del [!DNL Amazon S3] destino {#changes-amazon-s3-destination}

Los cambios incompatibles con versiones anteriores para los usuarios de la API se han actualizado `connection spec ID` y `flow spec ID` como se muestra en la tabla siguiente:

| [!DNL Amazon S3] | Heredado | Nuevo |
|---------|----------|---------|
| Especificación de flujo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| Especificación de conexión | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Vea los ejemplos completos de conexión base y de destino heredados y nuevos para [!DNL Amazon S3] en las pestañas siguientes. Los parámetros necesarios para crear conexiones base para [!DNL Amazon S3] los destinos no cambian.

Del mismo modo, no hay cambios incompatibles con versiones anteriores en los parámetros necesarios para crear conexiones de destino.

>[!BEGINTABS]

>[!TAB Conexión base heredada y conexión de destino]

+++Ver heredado [!DNL base connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Ver heredado [!DNL target connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nueva conexión base y conexión de destino]

+++Ver nuevo [!DNL base connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Ver nuevo [!DNL target connection] para [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Cambios incompatibles con versiones anteriores de [!DNL Azure Blob] destino {#changes-azure-blob-destination}

Los cambios incompatibles con versiones anteriores para los usuarios de la API se han actualizado `connection spec ID` y `flow spec ID` como se muestra en la tabla siguiente:

| [!DNL Azure Blob] | Heredado | Nuevo |
|---------|----------|---------|
| Especificación de flujo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| Especificación de conexión | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Vea los ejemplos completos de conexión base y de destino heredados y nuevos para [!DNL Azure Blob] en las pestañas siguientes. Los parámetros necesarios para crear conexiones base para destinos de Azure Blob no cambian.

Del mismo modo, no hay cambios incompatibles con versiones anteriores en los parámetros necesarios para crear conexiones de destino.

>[!BEGINTABS]

>[!TAB Conexión base heredada y conexión de destino]

+++Ver heredado [!DNL base connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Ver heredado [!DNL target connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nueva conexión base y conexión de destino]

+++Ver nuevo [!DNL base connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Ver nuevo [!DNL target connection] para [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Cambios incompatibles con versiones anteriores en el destino SFTP {#changes-sftp-destination}

Los cambios incompatibles con versiones anteriores para los usuarios de la API se han actualizado `connection spec ID` y `flow spec ID` como se muestra en la tabla siguiente:

| SFTP | Heredado | Nuevo |
|---------|----------|---------|
| Especificación de flujo | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeb799 |
| Especificación de conexión | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Además de las especificaciones de flujo y conexión actualizadas anteriores, hay cambios en los parámetros necesarios al crear conexiones base SFTP.

* Anteriormente, la conexión base para destinos SFTP requería un `host` parámetro. Este parámetro se ha cambiado a `domain`.

Vea los ejemplos completos de conexión base y de destino heredados y nuevos para SFTP en las pestañas siguientes, con las líneas que cambian resaltadas. Los parámetros necesarios para crear conexiones de destino para destinos SFTP no cambian.

>[!BEGINTABS]

>[!TAB Conexión base heredada y conexión de destino]

+++Ver heredado [!DNL base connection] para SFTP: autenticación de contraseña

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Ver heredado [!DNL base connection] para [!DNL SFTP - SSH key] authentication

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Ver heredado [!DNL target connection] para SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Nueva conexión base y conexión de destino]

+++Ver nuevo [!DNL base connection] para [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Ver nuevo [!DNL base connection] para [!DNL SFTP - SSH key] authentication

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Ver nuevo [!DNL target connection] para SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Cambios incompatibles con versiones anteriores comunes a [!DNL Amazon S3], [!DNL Azure Blob]destinos SFTP y {#changes-all-destinations}

El paso del selector de perfil en los tres destinos se reemplaza por un paso de asignación que le permite cambiar el nombre de los encabezados de columna en los archivos exportados, si lo desea. Consulte la siguiente imagen en paralelo con el paso del selector de atributos antiguo a la izquierda y el nuevo paso de asignación a la derecha.

![Imagen de información general de guía de migración](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Observe cómo la variable `profileSelectors` en los ejemplos heredados, el objeto se sustituye por el nuevo `profileMapping` objeto.

Encuentre información completa sobre la configuración de `profileMapping` objeto en el [Tutorial de API para exportar datos a destinos de almacenamiento en la nube](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB Parámetros de transformación antiguos]

+++Ver un ejemplo de parámetros de transformación antiguos

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Nuevos parámetros de transformación]

+++Vea un ejemplo de parámetros de transformación después de la migración

Observe en el ejemplo de configuración siguiente cómo `profileSelectors` Los campos de se han sustituido por un `profileMapping` objeto.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Cronología de la migración y elementos de acción {#timeline-and-action-items}

La migración de flujos de datos heredados a las nuevas tarjetas de destino para [!DNL Amazon S3], [!DNL Azure Blob]Los destinos SFTP y se producirán en cuanto su organización esté lista para la migración y no más tarde de **26 de julio de 2023**.

Recibirá correos electrónicos de recordatorio del Adobe a medida que se aproxime la fecha de migración. Como preparación, lea la sección Elementos de acción a continuación para prepararse para la migración.

### Elementos de acción {#action-items}

A fin de prepararse para la migración de [!DNL Amazon S3], [!DNL Azure Blob], y los destinos de almacenamiento en la nube SFTP para las nuevas tarjetas, prepárese para actualizar los scripts y las llamadas de API automatizadas como se sugiere a continuación.

1. Actualizar cualquier script o llamada de API automatizada para cualquier [!DNL Amazon S3], [!DNL Azure Blob]o destinos de almacenamiento en la nube SFTP antes del 26 de julio de 2023. Cualquier llamada o script de API automatizado que aproveche las especificaciones de conexión o las especificaciones de flujo heredadas debe actualizarse a las nuevas especificaciones de conexión o de flujo.
2. Póngase en contacto con el representante de su cuenta de Adobe cuando las secuencias de comandos se hayan actualizado antes del 26 de julio.
3. Por ejemplo, la variable `targetConnectionSpecId` se puede utilizar como indicador para determinar si el flujo de datos se ha migrado a la nueva tarjeta de destino. Puede actualizar los scripts con un `if` condición para ver las especificaciones de conexión de destino heredadas y actualizadas en `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` y determine si el flujo de datos se ha migrado. Puede ver los ID de especificaciones de conexión nuevos y heredados en las secciones específicas de esta página para cada destino.
4. El equipo de la cuenta de Adobe se pondrá en contacto con usted para proporcionarle más información sobre cuándo se migrarán los flujos de datos.
5. A partir del 26 de julio, se migrarán todos los flujos de datos. Todos los flujos de datos existentes ahora tendrán nuevas entidades de flujo (especificaciones de conexión, especificaciones de flujo, conexiones base y conexiones de destino). Cualquier script o llamada a la API por su parte que utilice las entidades de flujo heredadas dejará de funcionar.

## Otras consideraciones de migración {#other-considerations}

Tenga en cuenta que la programación de exportaciones existente no se ve afectada durante la migración o después de realizarla.

## Pasos siguientes {#next-steps}

Al leer esta página, ahora sabe si necesita tomar alguna acción como preparación para la migración de los destinos de almacenamiento en la nube. También sabe a qué páginas de documentación hacer referencia al configurar flujos de trabajo basados en API para exportar archivos fuera de Experience Platform a sus destinos de almacenamiento en la nube preferidos. A continuación, puede ver el tutorial de API para lo siguiente [exportar datos a destinos de almacenamiento en la nube](/help/destinations/api/activate-segments-file-based-destinations.md).
