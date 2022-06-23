---
title: (Beta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# (Beta) [!DNL Google Ad Manager 360] connection

## Información general {#overview}

La variable [!DNL Google Ad Manager 360] la conexión habilita la carga por lotes para [!DNL publisher provided identifiers] (PPID) en [!DNL Google Ad Manager 360], a través de [!DNL Google Cloud Storage].

Para obtener más información sobre cómo funcionan los identificadores proporcionados por el editor en Google Ad Manager 360, consulte la [documentación oficial de Google](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Este destino está actualmente en versión beta y solo está disponible para un número limitado de clientes. Para solicitar acceso a la [!DNL Google Ad Manager 360] conexión, póngase en contacto con su representante de Adobe y proporcione su [!DNL IMS Organization ID].

La variable [!DNL Google Ad Manager 360] exportaciones de destino [!DNL CSV] los archivos de [!DNL Google Cloud Storage] cubo. Una vez que haya exportado la variable [!DNL CSV] archivos, debe importarlos en su [!DNL Google Ad Manager 360] cuenta.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ad Manager 360] destinos.

* Las audiencias activadas se crean mediante programación en la plataforma Google y se rellenan en el archivo CSV.

## Identidades compatibles {#supported-identities}

[!DNL This integration] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Seleccione esta identidad de destino para enviar audiencias a [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Basado en perfiles]** | Está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla seleccionar atributos de perfil del [flujo de trabajo de activación de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frecuencia de exportación | **[!UICONTROL Lote]** | Los destinos de lote exportan archivos a plataformas descendentes en incrementos de tres, seis, ocho, doce o veinticuatro horas. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

### Permitir inclusión en la lista {#allow-listing}

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager] destino en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado en [!DNL Google] antes de crear un destino.

Antes de crear la variable [!DNL Google Ad Manager 360] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos . Contacto [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **ID de red**: esta es su cuenta con [!DNL Google Ad Manager]
* **ID del vínculo de audiencia**: esta es su cuenta con [!DNL Google Ad Manager]
* El tipo de cuenta. DFP de Google o del comprador de AdX.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Nombre del depósito]**: introduzca el nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

En el paso de asignación de identidad, puede ver las siguientes asignaciones rellenadas previamente:

| Asignación previamente rellenada | Descripción |
|---------|----------|
| `ECID` -> `ppid` | Esta es la única asignación previamente completada editable por el usuario. Puede seleccionar cualquiera de los atributos o áreas de nombres de identidad de Platform y asignarlos a `ppid`. |
| `metadata.segment.alias` -> `list_id` | Asigna nombres de segmento de Experience Platform a ID de segmento en la plataforma Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indica a la plataforma de Google cuándo eliminar de los segmentos a los usuarios no cualificados. |

Estas asignaciones son necesarias para [!DNL Google Ad Manager 360] y son creados automáticamente por Adobe Experience Platform para todos [!DNL Google Ad Manager 360] conexiones.

![Imagen de la interfaz de usuario que muestra el paso de asignación para Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente, consulte [!DNL Google Cloud Storage] y asegúrese de que los archivos exportados contienen las poblaciones de perfiles esperadas.
