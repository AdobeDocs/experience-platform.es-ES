---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
title: Añadir datos al Perfil del cliente en tiempo real
topic: tutorial
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al Perfil del cliente en tiempo real.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Añadir datos a [!DNL Real-time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-time Customer Profile].

## Habilitar un esquema para [!DNL Real-time Customer Profile]

Los datos que se están ingeriendo [!DNL Experience Platform] para su uso [!DNL Real-time Customer Profile] deben cumplir un esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que un esquema esté habilitado para Perfil, debe implementar la [!DNL XDM Individual Profile] clase o [!DNL XDM ExperienceEvent] .

Puede habilitar un esquema para utilizarlo [!DNL Real-time Customer Profile] mediante la [!DNL Schema Registry] API o la interfaz de [!DNL Schema Editor] usuario. Para empezar, siga los tutoriales para [crear un esquema con API](../../xdm/tutorials/create-schema-api.md) o [crear un esquema con la interfaz de usuario](../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas.

## Añadir datos mediante ingestión por lotes

Todos los datos cargados a [!DNL Platform] mediante la ingestión por lotes se cargan en conjuntos de datos individuales. Antes de que [!DNL Real-time Customer Profile]los datos puedan utilizarse, el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre la [configuración de un conjunto de datos para Perfil y servicio](dataset-configuration.md)de identidad.

Una vez configurado el conjunto de datos, puede realizar el inicio de la ingesta de datos. Consulte la guía [para desarrolladores de](../../ingestion/batch-ingestion/api-overview.md) ingestión por lotes para ver los pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Añadir datos mediante la transmisión de la ingestión

Cualquier dato ingerido por flujo que sea compatible con un esquema XDM [!DNL Profile]habilitado agregará o sobrescribirá automáticamente el registro apropiado en [!DNL Real-time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidad sin necesidad de realizar ninguna configuración adicional. Consulte la guía [para desarrolladores de](../../ingestion/tutorials/streaming-record-data.md) transmisiones de flujo continuo para obtener más información.

## Confirme que la carga se ha realizado correctamente

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Mediante la API de [!DNL Real-time Customer Profile] Access, puede recuperar datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades que espera, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato y los identificadores de los datos de origen admiten sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a las entidades mediante la [!DNL Real-time Customer Profile] API, consulte la guía [de extremo de](../api/entities.md)entidades, también conocida como &quot;[!DNL Profile Access] API&quot;.