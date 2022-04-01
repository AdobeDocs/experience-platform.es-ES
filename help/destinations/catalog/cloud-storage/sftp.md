---
keywords: SFTP;sftp
title: Conexión SFTP
description: Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 99bb5d1b76b926622ca21fa1df7c3cb9fabc4856
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# Conexión SFTP

## Información general {#overview}

Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque el Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar los datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada Base64."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clave SSH"
>abstract="La clave SSH requiere una cadena Base64."

When [conexión](../../ui/connect-destination.md) para este destino, debe proporcionar la siguiente información:

#### Información de autenticación {#authentication-information}

Si selecciona la opción **[!UICONTROL Autenticación básica]** escriba para conectarse a su ubicación SFTP:

![Autenticación básica de destino SFTP](../..//assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: La dirección de la ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para iniciar sesión en su ubicación de almacenamiento SFTP;
* **[!UICONTROL Contraseña]**: La contraseña para iniciar sesión en la ubicación de almacenamiento SFTP.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
   * Ejemplo: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![Clave PGP](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


Si selecciona la opción **[!UICONTROL SFTP con clave SSH]** tipo de autenticación para conectarse a su ubicación SFTP:

![Autenticación de clave SSH de destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: Rellene la dirección IP o el nombre de dominio de su cuenta SFTP.
* **[!UICONTROL Puerto]**: El puerto que utiliza su ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario para iniciar sesión en su ubicación de almacenamiento SFTP;
* **[!UICONTROL Clave SSH]**: La clave SSH para iniciar sesión en la ubicación de almacenamiento SFTP.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.
   * Ejemplo: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`

      ![Clave PGP](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Detalles de destino {#destination-details}

Después de establecer la conexión de autenticación en la ubicación SFTP, proporcione la siguiente información para el destino:

![Detalles de destino disponibles para el destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino en la interfaz de usuario del Experience Platform;
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino;
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta en la ubicación SFTP desde la que se exportan los archivos.

## Datos exportados {#exported-data}

Para [!DNL SFTP] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.

## LISTA DE PERMITIDOS de direcciones IP

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.
