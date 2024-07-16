---
title: Utilice el atributo XDM Última hora de calificación en los nuevos destinos de almacenamiento de la nube beta
description: Aprenda a utilizar el atributo XDM tiempo de última calificación en los nuevos destinos de almacenamiento en la nube beta
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Utilice el atributo XDM Última hora de calificación en los nuevos destinos de almacenamiento de la nube beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Esta página describe la funcionalidad que está en versión beta. La funcionalidad y la documentación están sujetas a cambios. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder a este programa beta.

## Requisitos previos {#prerequisites}

Para utilizar el atributo XDM de la última hora de calificación (`lastQualificationTime`), debe exportar datos a uno de los seis destinos de almacenamiento en la nube que se enumeran a continuación:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Cómo utilizar el atributo XDM de la última hora de calificación {#how-to-use}

Si está utilizando uno de los seis conectores de almacenamiento en la nube enumerados arriba, puede utilizar el atributo XDM Last Qualification Time en el [paso de asignación](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) del flujo de trabajo de activación para crear una columna en el archivo exportado con la última marca de tiempo de cuando un perfil cumple los requisitos para un segmento. Esto puede ayudarle con determinados casos de uso de medición o análisis, así como darle una mejor idea de cuándo activar determinadas audiencias.

Tenga en cuenta que para agregar `lastQualificationTime` a las exportaciones de archivos, actualmente necesita insertar manualmente el valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` en el campo de origen, como se muestra a continuación. También puede editar el campo de destino a `lastQualificationTime` o a cualquier otro valor al que desee asignar un nombre a esta columna. Tenga en cuenta que como esta es una funcionalidad beta, la sintaxis del valor `xdm: segmentMembership.ups.seg_id.lastQualificationTime` puede cambiar en el futuro.

![Grabación de pantalla que muestra la última hora de calificación del atributo XDM pegado en el paso de asignación](/help/destinations/ui/last-qualification-time.gif)

## Más información {#more-information}

Para obtener información detallada sobre la activación de datos en destinos basados en archivos, incluidos todos los pasos del flujo de trabajo y los permisos necesarios, lea el [tutorial de activación de destinos basados en archivos](/help/destinations/ui/activate-batch-profile-destinations.md).
