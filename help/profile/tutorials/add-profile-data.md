---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;habilitar perfil;Activar perfil
title: Añadir datos al perfil del cliente en tiempo real
topic-legacy: tutorial
type: Tutorial
description: Este tutorial describe los pasos necesarios para agregar datos al perfil del cliente en tiempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Añadir datos a [!DNL Real-Time Customer Profile]

Este tutorial describe los pasos necesarios para agregar datos a [!DNL Real-Time Customer Profile].

## Habilitar un esquema para [!DNL Real-Time Customer Profile]

Datos introducidos en [!DNL Experience Platform] para su uso por [!DNL Real-Time Customer Profile] debe ajustarse a un [!DNL Experience Data Model] esquema (XDM) habilitado para [!DNL Profile]. Para que un esquema esté habilitado para Profile, debe implementar la variable [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent] Clase .

Puede activar un esquema para utilizarlo en [!DNL Real-Time Customer Profile] usando la variable [!DNL Schema Registry] API o [!DNL Schema Editor] interfaz de usuario. Para empezar, siga los tutoriales de [creación de un esquema con API](../../xdm/tutorials/create-schema-api.md) o [creación de un esquema mediante la interfaz de usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adición de datos mediante ingesta por lotes

Todos los datos cargados a [!DNL Platform] el uso de la ingesta por lotes se carga en conjuntos de datos individuales. Antes de que estos datos puedan ser utilizados por [!DNL Real-Time Customer Profile], el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial en [configuración de un conjunto de datos para Perfil y servicio de identidad](dataset-configuration.md).

Una vez configurado el conjunto de datos, puede empezar a introducir datos en él. Consulte la [guía para desarrolladores sobre ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md) para ver los pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Adición de datos mediante ingesta de flujo continuo

Cualquier dato ingerido por flujo que sea compatible con un [!DNL Profile]El esquema XDM habilitado para - añadirá o sobrescribirá automáticamente el registro apropiado en [!DNL Real-Time Customer Profile]. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidad sin necesidad de ninguna configuración adicional. Consulte la [guía para desarrolladores de ingesta de transmisión](../../ingestion/tutorials/streaming-record-data.md) para obtener más información.

## Confirme que la carga se ha realizado correctamente.

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Al usar la variable [!DNL Real-Time Customer Profile] Acceso a la API de , puede recuperar datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades esperadas, es posible que el conjunto de datos no esté habilitado para [!DNL Profile]. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato de datos de origen y los identificadores cumplan con sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a las entidades mediante la variable [!DNL Real-Time Customer Profile] API, consulte la [guía de extremo de entidades](../api/entities.md), también conocido como &quot;[!DNL Profile Access] API&quot;.

## Actualizar datos del Almacenamiento de perfiles

En ocasiones puede ser necesario actualizar los datos en el Almacenamiento de perfiles de su organización. Por ejemplo, es posible que necesite corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para Perfil configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial para [activación de un conjunto de datos para Perfil y actualizar](../../catalog/datasets/enable-upsert.md).
