---
title: Utilice el último atributo XDM de tiempo de calificación en los nuevos destinos de almacenamiento de la nube beta
description: Aprenda a utilizar el último atributo XDM de tiempo de calificación en los nuevos destinos de almacenamiento de la nube beta
hidefromtoc: y
hide: y
source-git-commit: 03031dcaad82932f92e76177adf3b55447c3c153
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Utilice el último atributo XDM de tiempo de calificación en los nuevos destinos de almacenamiento de la nube beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Esta página describe la funcionalidad que está en versión beta. La funcionalidad y la documentación están sujetas a cambios. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder a este programa beta.

## Requisitos previos {#prerequisites}

Para usar la última hora de calificación (`lastQualificationTime`) Atributo XDM, debe estar inscrito en el [programa beta](/help/release-notes/2022/october-2022.md#destinations) para utilizar la funcionalidad mejorada de exportación de archivos y exportar datos a uno de los seis [destinos de almacenamiento en la nube beta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Está inscrito si puede ver las nuevas tarjetas beta para los destinos de almacenamiento en la nube en el catálogo, como se muestra a continuación para [!DNL Amazon S3].

![Imagen que muestra la nueva tarjeta beta Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Uso del último atributo XDM de tiempo de calificación {#how-to-use}

Si utiliza uno de los seis nuevos conectores beta de almacenamiento en la nube, puede utilizar el último atributo XDM de tiempo de calificación en la variable [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo de activación para crear una columna en el archivo exportado con la última marca de tiempo de cuando un perfil cumple los requisitos para un segmento. Esto puede ayudarle con determinados casos de uso de medición o análisis, así como con una mejor idea de cuándo activar determinadas audiencias.

Tenga en cuenta que para agregar `lastQualificationTime` a las exportaciones de archivos, actualmente debe insertar manualmente el valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` en el campo de origen, como se muestra a continuación. También puede editar el campo de destino a `lastQualificationTime` o cualquier otro valor al que desee asignar un nombre a esta columna. Tenga en cuenta que, como se trata de una funcionalidad beta, la sintaxis de la variable `xdm: segmentMembership.ups.seg_id.lastQualificationTime` puede cambiar en el futuro.

![Grabación de pantalla que muestra el último tiempo de calificación, el atributo XDM se pega en el paso de asignación](/help/destinations/ui/last-qualification-time.gif)

## Más información {#more-information}

Para obtener información detallada sobre la activación de datos en destinos basados en archivos, incluidos todos los pasos del flujo de trabajo y los permisos necesarios, lea la [tutorial activar destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md).