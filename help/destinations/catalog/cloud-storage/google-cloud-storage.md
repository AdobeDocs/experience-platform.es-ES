---
title: (Beta) Conexión de almacenamiento en la nube de Google
description: Obtenga información sobre cómo conectar con Google Cloud Storage y activar segmentos o exportar conjuntos de datos.
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: f841b27a2d2700b0b68a386b89d1a5c62d3910ff
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# (Beta) [!DNL Google Cloud Storage] connection

>[!IMPORTANT]
>
>Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la [!DNL Google Cloud Storage] conexión, póngase en contacto con su representante de Adobe y proporcione su [!DNL Organization ID].

## Información general {#overview}

Cree una conexión de salida activa a [!DNL Google Cloud Storage] para exportar periódicamente archivos de datos de Adobe Experience Platform a sus propios bloques.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Se están exportando todos los miembros de un segmento, junto con los campos de esquema aplicables, tal y como se han elegido en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Configuración de requisitos previos para conectar su [!DNL Google Cloud Storage] account {#prerequisites}

Para conectar Platform a [!DNL Google Cloud Storage], primero debe habilitar la interoperabilidad para su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, abra [!DNL Google Cloud Platform] y seleccione **[!UICONTROL Configuración]** de la variable **[!UICONTROL Almacenamiento en la nube]** en el panel de navegación.

![Panel de Google Cloud Platform con almacenamiento en la nube y configuración resaltados.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

La variable **[!UICONTROL Configuración]** se abre. Desde aquí puede ver información sobre su [!DNL Google] ID del proyecto y detalles sobre su [!DNL Google Cloud Storage] cuenta. Para acceder a la configuración de interoperabilidad, seleccione **[!UICONTROL Interoperabilidad]** en el encabezado superior.

![La pestaña Interoperability resaltada en el panel de control de Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

La variable **[!UICONTROL Interoperabilidad]** contiene información sobre la autenticación, las claves de acceso y el proyecto predeterminado asociado a su cuenta de servicio. Para generar un nuevo ID de clave de acceso y una clave de acceso secreta para su cuenta de servicio, seleccione **[!UICONTROL Crear una clave para una cuenta de servicio]**.

![La opción Crear una clave para un control de cuenta de servicio resaltada en el panel de control de Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puede utilizar el ID de clave de acceso y la clave de acceso secreta que acaba de generar para conectar su [!DNL Google Cloud Storage] a Platform.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](/help/destinations/ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

* **[!UICONTROL Acceso a ID de clave]**: Una cadena alfanumérica de 61 caracteres que se usa para autenticar su [!DNL Google Cloud Storage] a Platform. Para obtener información sobre cómo obtener este valor, lea la [requisitos previos](#prerequisites) sección anterior.
* **[!UICONTROL Clave de acceso secreta]**: Una cadena con codificación base64 de 40 caracteres que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform. Para obtener información sobre cómo obtener este valor, lea la [requisitos previos](#prerequisites) sección anterior.
* **[!UICONTROL Clave de cifrado]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la imagen siguiente.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la interfaz de usuario](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obtener más información sobre estos valores, lea la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para ver los pasos sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] información general de la fuente](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Nombre del depósito]**: Introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: Introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Programación

En el **[!UICONTROL Programación]** paso, puede [configuración de la programación de exportación](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para su [!DNL Google Cloud Storage] destino y también puede [configurar el nombre de los archivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Asignación de atributos e identidades {#map}

En el **[!UICONTROL Asignación]** , puede seleccionar qué campos de atributo e identidad desea exportar para sus perfiles. También puede seleccionar cambiar los encabezados del archivo exportado por cualquier nombre descriptivo que desee. Para obtener más información, consulte [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) en el tutorial activar la interfaz de usuario de los destinos de lote .

## (Beta) Exportar conjuntos de datos {#export-datasets}

Este destino admite exportaciones de conjuntos de datos. Para obtener información completa sobre cómo configurar las exportaciones de conjuntos de datos, lea la [tutorial de exportación de conjuntos de datos](/help/destinations/ui/export-datasets.md).

## Validar la exportación de datos correcta {#exported-data}

Para comprobar si los datos se han exportado correctamente, consulte [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
