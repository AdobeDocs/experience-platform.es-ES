---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API;habilitar perfil;Habilitar perfil
title: Añadir datos al Perfil del cliente en tiempo real
topic: tutorial
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al Perfil del cliente en tiempo real.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Añadir datos a [!DNL Real-time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-time Customer Profile].

## Habilitar un esquema para [!DNL Real-time Customer Profile]

Los datos que se están ingeriendo en [!DNL Experience Platform] para su uso por [!DNL Real-time Customer Profile] deben cumplir un esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que un esquema esté habilitado para Perfil, debe implementar la clase [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

Puede habilitar un esquema para utilizarlo en [!DNL Real-time Customer Profile] mediante la API [!DNL Schema Registry] o la interfaz de usuario [!DNL Schema Editor]. Para empezar, siga los tutoriales para [crear un esquema con API](../../xdm/tutorials/create-schema-api.md) o [crear un esquema con la IU del Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md).

## Añadir datos mediante ingestión por lotes

Todos los datos cargados a [!DNL Platform] mediante ingestión por lotes se cargan en conjuntos de datos individuales. Antes de que [!DNL Real-time Customer Profile] pueda utilizar estos datos, el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre [configuración de un conjunto de datos para Perfil y servicio de identidad](dataset-configuration.md).

Una vez configurado el conjunto de datos, puede realizar el inicio de la ingesta de datos. Consulte la [guía para desarrolladores de ingestión por lotes](../../ingestion/batch-ingestion/api-overview.md) para obtener pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Añadir datos mediante la transmisión de la ingestión

Cualquier dato ingerido por flujo que sea compatible con un esquema XDM habilitado para [!DNL Profile] automáticamente agregará o sobrescribirá el registro apropiado en [!DNL Real-time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidad sin necesidad de realizar ninguna configuración adicional. Consulte la [guía para desarrolladores de sugerencias de flujo continuo](../../ingestion/tutorials/streaming-record-data.md) para obtener más información.

## Confirme que la carga se ha realizado correctamente

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Mediante la API de acceso [!DNL Real-time Customer Profile], puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades que espera, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato y los identificadores de los datos de origen admiten sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a las entidades mediante la API [!DNL Real-time Customer Profile], consulte la [guía de extremo de entidades](../api/entities.md), también conocida como la &quot;[!DNL Profile Access] API&quot;.