---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Añadir datos al Perfil del cliente en tiempo real
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Añadir datos al Perfil del cliente en tiempo real

Este tutorial describe los pasos necesarios para agregar datos al Perfil del cliente en tiempo real.

## Habilitar un esquema para el Perfil del cliente en tiempo real

Los datos que el Perfil del cliente en tiempo real ingesta en la plataforma de experiencia para su uso deben cumplir con un esquema del modelo de datos de experiencia (XDM) habilitado para el Perfil. Para que un esquema esté habilitado para Perfil, debe implementar la clase XDM Individual Perfil o XDM ExperienceEvent.

Puede activar un esquema para utilizarlo en el Perfil de clientes en tiempo real mediante la API del Registro de Esquemas o la interfaz de usuario del Editor de Esquemas. Para empezar, siga los tutoriales para [crear un esquema con API](../../xdm/tutorials/create-schema-api.md) o [crear un esquema con la interfaz de usuario](../../xdm/tutorials/create-schema-ui.md)del Editor de Esquemas.

## Añadir datos mediante ingestión por lotes

Todos los datos cargados en la plataforma mediante la ingestión por lotes se cargan en conjuntos de datos individuales. Antes de que el Perfil del cliente en tiempo real pueda utilizar estos datos, el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas, consulte el tutorial sobre la [configuración de un conjunto de datos para Perfil y servicio](dataset-configuration.md)de identidad.

Una vez configurado el conjunto de datos, puede realizar el inicio de la ingesta de datos. Consulte la guía [para desarrolladores de](../../ingestion/batch-ingestion/api-overview.md) ingestión por lotes para ver los pasos detallados sobre cómo cargar archivos en diferentes formatos.

## Añadir datos mediante la transmisión de la ingestión

Cualquier dato ingerido por flujo que sea compatible con un esquema XDM habilitado para Perfil automáticamente agregará o sobrescribirá el registro apropiado en el Perfil del cliente en tiempo real. Si se proporciona más de una identidad en el registro o se consumen datos de series temporales, esas identidades se asignarán en el gráfico de identidad sin necesidad de realizar ninguna configuración adicional. Consulte la guía [para desarrolladores de](../../ingestion/tutorials/streaming-record-data.md) transmisiones de flujo continuo para obtener más información.

## Confirme que la carga se ha realizado correctamente

Al cargar datos en un nuevo conjunto de datos por primera vez, o como parte de un proceso que involucra una nueva ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente.

Mediante la API de acceso a Perfil de cliente en tiempo real, puede recuperar datos por lotes a medida que se cargan en un conjunto de datos. Si no puede recuperar ninguna de las entidades que espera, es posible que el conjunto de datos no esté habilitado para el Perfil. Después de confirmar que el conjunto de datos se ha habilitado, asegúrese de que el formato y los identificadores de los datos de origen admiten sus expectativas.

Para obtener instrucciones detalladas sobre cómo acceder a las entidades mediante la API de Perfil del cliente en tiempo real, consulte la [subguía de entidades, también conocida como la &quot;API de acceso a Perfil&quot;](../api/entities.md).