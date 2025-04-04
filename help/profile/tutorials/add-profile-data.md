---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API;habilitar perfil;Habilitar perfil
title: Añadir datos al perfil del cliente en tiempo real
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al Perfil del cliente en tiempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Agregar datos a [!DNL Real-Time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-Time Customer Profile].

## Habilitar un esquema para [!DNL Real-Time Customer Profile]

Los datos que se están ingiriendo en [!DNL Experience Platform] para su uso por [!DNL Real-Time Customer Profile] deben ajustarse a un esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para habilitar un esquema para el perfil, debe implementar la clase [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

Puede habilitar un esquema para utilizarlo en [!DNL Real-Time Customer Profile] mediante la API [!DNL Schema Registry] o la interfaz de usuario [!DNL Schema Editor]. Para empezar, siga los tutoriales de [creación de un esquema con API](../../xdm/tutorials/create-schema-api.md) o [creación de un esquema con la interfaz de usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Añadir datos mediante la ingesta por lotes

Todos los datos cargados a [!DNL Experience Platform] mediante la ingesta por lotes se cargan en conjuntos de datos individuales. Para que [!DNL Real-Time Customer Profile] pueda usar estos datos, el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre [configuración de un conjunto de datos para el perfil y el servicio de identidad](dataset-configuration.md).

Una vez configurado el conjunto de datos, puede empezar a introducir datos en él. Consulte la [guía para desarrolladores de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md) para ver los pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Adición de datos mediante la ingesta por streaming

Cualquier dato ingerido por flujo que sea compatible con un esquema XDM habilitado para [!DNL Profile] agregará o sobrescribirá automáticamente el registro correspondiente en [!DNL Real-Time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidades sin configuración adicional. Consulte la [guía para desarrolladores de ingesta de transmisión](../../ingestion/tutorials/streaming-record-data.md) para obtener más información.

## Confirme que la carga se ha realizado correctamente

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que implica un nuevo ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Con la API de acceso de [!DNL Real-Time Customer Profile], puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplen con sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a entidades que utilizan la API [!DNL Real-Time Customer Profile], consulte la [guía de extremo de entidades](../api/entities.md), también conocida como la API [!DNL Profile Access].

## Actualizar datos del almacén de perfiles

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para el perfil y configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial de [habilitar un conjunto de datos para Perfil y actualizar](../../catalog/datasets/enable-upsert.md).
