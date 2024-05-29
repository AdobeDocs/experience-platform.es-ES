---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;habilitar perfil;habilitar perfil
title: Añadir datos al perfil del cliente en tiempo real
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al Perfil del cliente en tiempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Añadir datos a [!DNL Real-Time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-Time Customer Profile].

## Habilitar un esquema para [!DNL Real-Time Customer Profile]

Datos que se están ingiriendo en [!DNL Experience Platform] para su uso por [!DNL Real-Time Customer Profile] debe ajustarse a un [!DNL Experience Data Model] Esquema (XDM) habilitado para [!DNL Profile]. Para que un esquema esté habilitado para el perfil, debe implementar el [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent] clase.

Puede habilitar un esquema para utilizarlo en [!DNL Real-Time Customer Profile] uso del [!DNL Schema Registry] API para [!DNL Schema Editor] interfaz de usuario. Para empezar, siga los tutoriales de [creación de un esquema mediante API](../../xdm/tutorials/create-schema-api.md) o [creación de un esquema mediante la interfaz de usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Añadir datos mediante la ingesta por lotes

Todos los datos cargados en [!DNL Platform] el uso de la ingesta por lotes se carga en conjuntos de datos individuales. Antes de que estos datos puedan ser utilizados por [!DNL Real-Time Customer Profile], el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre [Configuración de un conjunto de datos para el perfil y el servicio de identidad](dataset-configuration.md).

Una vez configurado el conjunto de datos, puede empezar a introducir datos en él. Consulte la [guía para desarrolladores de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md) para ver los pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Adición de datos mediante la ingesta por streaming

Cualquier dato ingerido por flujo que sea compatible con un [!DNL Profile]El esquema XDM habilitado para agregará o sobrescribirá automáticamente el registro correspondiente en [!DNL Real-Time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidades sin configuración adicional. Consulte la [guía para desarrolladores de ingesta de streaming](../../ingestion/tutorials/streaming-record-data.md) para obtener más información.

## Confirme que la carga se ha realizado correctamente

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que implica un nuevo ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Uso del [!DNL Real-Time Customer Profile] Acceso a la API, puede recuperar los datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplen con sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a entidades utilizando [!DNL Real-Time Customer Profile] API, consulte la [guía de extremo de entidades](../api/entities.md), también conocido como &quot;[!DNL Profile Access] API&quot;.

## Actualizar datos del almacén de perfiles

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para el perfil y configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial de [habilitar un conjunto de datos para perfiles y actualizaciones](../../catalog/datasets/enable-upsert.md).
