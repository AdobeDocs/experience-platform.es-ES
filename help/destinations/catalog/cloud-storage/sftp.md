---
keywords: SFTP;sftp
title: Conexión SFTP
description: Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 55f72e4f229e18648e0e745a2a60e9add50455b0
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 7%

---

# Conexión SFTP

## Registro de cambios de destino {#changelog}

>[!IMPORTANT]
>
>Con la versión beta de la funcionalidad exportar conjuntos de datos y la funcionalidad mejorada de exportación de archivos, es posible que ahora vea dos [!DNL SFTP] tarjetas en el catálogo de destinos.
>* Si ya está exportando archivos a **[!UICONTROL SFTP]** destino: cree nuevos flujos de datos para el nuevo **[!UICONTROL SFTP beta]** destino.
>* Si todavía no ha creado ningún flujo de datos en **[!UICONTROL SFTP]** destino, utilice el nuevo **[!UICONTROL SFTP beta]** para exportar archivos a **[!UICONTROL SFTP]**.


![Imagen de las dos tarjetas de destino SFTP en una vista en paralelo.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Mejoras en el nuevo [!DNL SFTP] la tarjeta de destino incluye:

* [Compatibilidad con exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).
* Adicional [opciones de nomenclatura de archivos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Posibilidad de establecer encabezados de archivo personalizados en los archivos exportados a través de [paso de asignación mejorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidad para personalizar el formato de archivos de datos CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Información general {#overview}

Cree una conexión saliente activa a su servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque Experience Platform admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL SFTP].

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Va a exportar todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos por lotes exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Información de autenticación {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para añadir cifrado a los archivos exportados. Vea un ejemplo de una clave con formato correcto en el vínculo de documentación siguiente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Clave SSH privada"
>abstract="La clave SSH privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña."

Si selecciona la opción **[!UICONTROL Autenticación básica]** escriba para conectarse a su ubicación SFTP:

![Autenticación básica de destino SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: la dirección de la ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Contraseña]**: contraseña para iniciar sesión en la ubicación de almacenamiento SFTP.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Si selecciona la opción **[!UICONTROL SFTP con clave SSH]** tipo de autenticación para conectarse a su ubicación SFTP:

![Autenticación de clave SSH de destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: complete la dirección IP o el nombre de dominio de su cuenta SFTP
* **[!UICONTROL Puerto]**: el puerto utilizado por la ubicación de almacenamiento SFTP;
* **[!UICONTROL Nombre de usuario]**: el nombre de usuario para iniciar sesión en la ubicación de almacenamiento SFTP;
* **[!UICONTROL Clave SSH]**: clave SSH privada que se utiliza para iniciar sesión en la ubicación de almacenamiento SFTP. La clave privada debe tener el formato de cadena codificada Base64 y no debe estar protegida por contraseña.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Detalles del destino {#destination-details}

Después de establecer la conexión de autenticación con la ubicación SFTP, proporcione la siguiente información para el destino:

![Detalles de destino disponibles para el destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nombre]**: introduzca un nombre que le ayude a identificar este destino en la interfaz de usuario del Experience Platform;
* **[!UICONTROL Descripción]**: introduzca una descripción para este destino;
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta en la ubicación SFTP donde se exportarán los archivos.
* **[!UICONTROL Tipo de archivo]**: seleccione el Experience Platform de formato que debe utilizar para los archivos exportados. Esta opción solo está disponible para **[!UICONTROL SFTP beta]** destino. Al seleccionar la variable [!UICONTROL CSV] , también puede hacer lo siguiente [configurar las opciones de formato de archivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados. Esta opción solo está disponible para **[!UICONTROL SFTP beta]** destino.
* 
   * **[!UICONTROL Incluir archivo de manifiesto]**: active esta opción si desea que las exportaciones incluyan un archivo JSON de manifiesto que contenga información sobre la ubicación de exportación, el tamaño de exportación, etc. Esta opción solo está disponible para **[!UICONTROL SFTP beta]** destino.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar exportaciones de conjuntos de datos, lea la [tutorial de exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Datos exportados {#exported-data}

Para [!DNL SFTP] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.

## LISTA DE PERMITIDOS de direcciones IP

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.
