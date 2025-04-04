---
title: Exportación de matrices, mapas y objetos desde Real-Time CDP
type: Tutorial
description: Obtenga información sobre cómo exportar matrices, mapas y objetos de Real-Time CDP a destinos de almacenamiento en la nube.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 13%

---

# Exportación de matrices, mapas y objetos desde Real-Time CDP {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>La funcionalidad para exportar matrices y otros objetos complejos a destinos de almacenamiento en la nube suele estar disponible para los siguientes destinos: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md).
>
>Además, puede exportar campos de tipo mapa a los siguientes destinos: [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md).


Aprenda a exportar matrices, asignaciones y objetos de Real-Time CDP a [destinos de almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md). Además, puede exportar campos de tipo mapa a [destinos empresariales](/help/destinations/destination-types.md#advanced-enterprise-destinations) y [destinos de personalización edge](/help/destinations/destination-types.md#edge-personalization-destinations) limitados. Lea este documento para comprender el flujo de trabajo de exportación, los casos de uso habilitados por esta funcionalidad y las limitaciones conocidas. Consulte la tabla siguiente para comprender las funcionalidades disponibles por tipo de destino.

| Tipo de destino | Capacidad para exportar matrices, mapas y otros objetos personalizados |
|---|---|
| Destinos de almacenamiento en la nube creados por Adobe (Amazon S3, Azure Blob, Azure Data Lake Storage Gen2, Data Landing Zone, Google Cloud Storage, SFTP) | Sí, con la opción Habilitar exportación de matrices, mapas y objetos activada al configurar una conexión de destino. |
| Destinos de marketing por correo electrónico basados en archivos (Adobe Campaign, Oracle Eloqua, Oracle Responsys, Salesforce Marketing Cloud) | No |
| Destinos de almacenamiento en la nube creados por socios personalizados existentes (destinos personalizados basados en archivos creados mediante Destination SDK) | No |
| Destinos empresariales (Amazon Kinesis, Azure Event Hubs, API HTTP) | Parcialmente. Puede seleccionar y exportar objetos de tipo mapa en el paso de asignación del flujo de trabajo de activación. |
| Destinos de streaming (por ejemplo: Facebook, Braze, Google Customer Match y más) | No |
| Destinos de personalización de Edge (Adobe Target) | Parcialmente. Puede seleccionar y exportar objetos de tipo mapa en el paso de asignación del flujo de trabajo de activación. |

{style="table-layout:auto"}

Considere esta página como su lugar de referencia para todo lo que desee saber acerca de la exportación de matrices, mapas y otros tipos de objetos de Experience Platform.

## Línea inferior delante

Obtenga la información más importante acerca de la funcionalidad de esta sección y continúe a las demás secciones del documento para obtener información detallada.

* En el caso de los destinos de almacenamiento en la nube, la capacidad de exportar matrices, asignaciones y objetos depende de que haya seleccionado la opción **Exportar matrices, asignaciones, objetos**. Obtenga más información [más abajo en la página](#export-arrays-maps-objects-toggle).
* Puede exportar matrices, asignaciones y objetos a destinos de almacenamiento en la nube en `JSON` y `Parquet` archivos. Para los destinos de personalización de empresa y Edge, el tipo de datos exportado es `JSON`. Se admiten las audiencias de personas y clientes potenciales, pero no las de cuenta.
* Para los destinos de almacenamiento en la nube basados en archivos, *puede* exportar matrices, asignaciones y objetos a archivos CSV, pero solo mediante la funcionalidad de campos calculados y concatenándolos en una cadena mediante la función `array_to_string`.

## Matrices y otros tipos de objetos en Experience Platform {#arrays-strings-other-objects}

En Experience Platform, puede usar [esquemas XDM](/help/xdm/home.md) para administrar diferentes tipos de campos. Antes de añadir compatibilidad con las exportaciones de matrices, podía exportar campos de tipo de par clave-valor simples, como cadenas, desde Experience Platform a los destinos deseados. Un ejemplo de un campo de este tipo que se admitía para la exportación anteriormente es `personalEmail.address`:`johndoe@acme.org`.

Otros tipos de campo en Experience Platform incluyen campos de matriz. Obtenga más información acerca de [administrar campos de matriz en la interfaz de usuario de Experience Platform](/help/xdm/ui/fields/array.md). Ahora puede exportar objetos de matriz, como en el ejemplo siguiente.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Además de las matrices, también puede exportar mapas y objetos de Experience Platform al destino de almacenamiento en la nube deseado. Obtenga más información sobre [mapas](/help/xdm/ui/fields/map.md) y [objetos](/help/xdm/ui/fields/object.md) en Experience Platform.

## Requisitos previos {#prerequisites}

[Conéctese](/help/destinations/ui/connect-destination.md) a un destino de almacenamiento en la nube deseado, avance en los [pasos de activación para los destinos de almacenamiento en la nube](/help/destinations/ui/activate-batch-profile-destinations.md) y vaya al paso [asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). Al conectarse al destino de nube deseado, debe seleccionar la opción **[!UICONTROL Exportar matrices, mapas, objetos]**. Obtenga más información en la sección siguiente.

>[!NOTE]
>
>Para destinos de personalización de empresa y Edge, la compatibilidad de exportación para campos de tipo map está disponible sin necesidad de seleccionar una opción **[!UICONTROL Exportar matrices, mapas, objetos]**. Esta opción no está disponible o no es necesaria al conectarse a estos tipos de destinos.

## Exportar matrices, mapas, objetos o alternar {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Exportación de matrices, mapas y objetos"
>abstract="<p> Establezca esta configuración en <b>on</b> (activada) para habilitar la exportación de matrices, mapas y objetos a archivos JSON o Parquet. Puede seleccionar estos tipos de objeto en la vista del campo de origen del paso de asignación. Con la opción activada, no se puede utilizar la opción de campos calculados en el paso de asignación.</p><p>Si esta opción está <b>desactivada</b>, puede usar la opción de campos calculados y aplicar varias funciones de transformación de datos al activar públicos. Sin embargo, <i>no</i> puede exportar matrices, asignaciones y objetos a archivos JSON o Parquet y debe configurar un destino independiente para ese fin.</p>"

Al conectarse a un destino de almacenamiento en la nube basado en archivos, puede activar o desactivar **[!UICONTROL Exportar matrices, mapas, objetos]**.

![Exporte matrices, mapas, objetos que se muestran con una configuración de activación o desactivación, así como resaltando la ventana emergente.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

Establezca esta configuración en **on** (activada) para habilitar la exportación de matrices, mapas y objetos a archivos JSON o Parquet. Puede seleccionar estos tipos de objeto en la vista del campo de origen del [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) al activar audiencias en destinos de almacenamiento en la nube. Sin embargo, con esta configuración activada, no se puede utilizar la opción de campos calculados para transformar los datos al activarlos.

Si esta opción está **desactivada**, puede usar la opción de campos calculados y aplicar varias funciones de transformación de datos al activar públicos. Sin embargo, no puede exportar matrices, mapas y objetos a archivos JSON o Parquet y debe configurar un destino independiente para ese fin.

## Exportar matrices, mapas, objetos, alternar *en* {#export-arrays-maps-objects-toggle-on}

Con esta configuración activada, puede exportar objetos completos (por ejemplo `person.name`) y matrices seleccionándolos a través del selector del campo de origen en el paso de asignación del flujo de trabajo de activación.

![Seleccione objetos mediante el selector de campo de origen en el paso de asignación del flujo de trabajo de activación.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Con esta opción seleccionada, la interfaz de usuario impide que los usuarios usen campos calculados y el control **[!UICONTROL Agregar campos calculados]** está deshabilitado, como se muestra a continuación. Para utilizar campos calculados para transformaciones de datos, configure una conexión de destino con la opción desactivada.

![Se deshabilitó el control de campos calculados.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Exportar matrices, mapas, objetos desactivar *off* {#export-arrays-maps-objects-toggle-off}

Con esta opción establecida en *off*, puede utilizar la opción de campos calculados y aplicar varias funciones de transformación de datos al activar audiencias. Sin embargo, no puede exportar matrices, mapas y objetos a archivos JSON o Parquet y debe configurar un destino independiente para ese fin.

*puede* exportar matrices, asignaciones y objetos a archivos CSV mediante la funcionalidad de campos calculados y concatenarlos en una cadena mediante la función `array_to_string`. [Más información](#array-to-string-function-export-arrays) sobre cómo usar esa función.

Obtenga más información sobre cómo trabajar con campos calculados para [realizar transformaciones en los datos exportados a destinos de almacenamiento en la nube](/help/destinations/ui/data-transformations-calculated-fields.md).

## Archivos exportados de muestra {#sample-exported-files}

Con esta funcionalidad, puede exportar archivos Parquet y JSON donde los datos conservan la estructura de Experience Platform. Vea a continuación un ejemplo de un archivo JSON exportado.

+++ Seleccione para ver el archivo JSON exportado.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++