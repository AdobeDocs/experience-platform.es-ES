---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;habilitar perfil;Activar perfil
title: Añadir datos al perfil del cliente en tiempo real
topic-legacy: tutorial
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al perfil del cliente en tiempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Añadir datos a [!DNL Real-time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-time Customer Profile].

## Habilitar un esquema para [!DNL Real-time Customer Profile]

Los datos introducidos en [!DNL Experience Platform] para su uso por [!DNL Real-time Customer Profile] deben cumplir un esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que un esquema esté habilitado para Profile, debe implementar la clase [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

Puede habilitar un esquema para utilizarlo en [!DNL Real-time Customer Profile] mediante la API [!DNL Schema Registry] o la interfaz de usuario [!DNL Schema Editor]. Para empezar, siga los tutoriales para [crear un esquema con API](../../xdm/tutorials/create-schema-api.md) o [crear un esquema con la IU del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adición de datos mediante ingesta por lotes

Todos los datos cargados en [!DNL Platform] mediante ingesta por lotes se cargan en conjuntos de datos individuales. Antes de que [!DNL Real-time Customer Profile] pueda utilizar estos datos, el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre [configuración de un conjunto de datos para Perfil y servicio de identidad](dataset-configuration.md).

Una vez configurado el conjunto de datos, puede empezar a introducir datos en él. Consulte la [guía para desarrolladores sobre ingesta en lotes](../../ingestion/batch-ingestion/api-overview.md) para obtener información detallada sobre cómo cargar archivos en diferentes formatos.

## Adición de datos mediante ingesta de flujo continuo

Cualquier dato ingerido en la emisión que sea compatible con un esquema XDM habilitado para [!DNL Profile] añadirá o sobrescribirá automáticamente el registro apropiado en [!DNL Real-time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidad sin necesidad de ninguna configuración adicional. Consulte la [guía para desarrolladores de ingesta de flujo](../../ingestion/tutorials/streaming-record-data.md) para obtener más información.

## Confirme que la carga se ha realizado correctamente.

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Con la API de acceso [!DNL Real-time Customer Profile], puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplan con sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a entidades mediante la API [!DNL Real-time Customer Profile], consulte la [guía de extremo de entidades](../api/entities.md), también conocida como la &quot;[!DNL Profile Access] API&quot;.
