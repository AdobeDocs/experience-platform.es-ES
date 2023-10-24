---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión de octubre de 2023 para Adobe Experience Platform.
source-git-commit: d024596c7d85139721ef370f9e081911a217d9ba
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 43%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de octubre de 2023**

Actualizaciones de las funciones existentes en Experience Platform:

- [Fuentes](#sources)

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Autenticación actualizada para la zona de aterrizaje de datos | Ahora puede ver la fecha de caducidad designada de la zona de aterrizaje de datos al ver sus credenciales. Debe actualizar el token antes de la fecha de caducidad para poder utilizarlo en la aplicación. Si no actualiza manualmente el token antes de la fecha de caducidad indicada, se actualizará automáticamente y proporcionará un nuevo token la próxima vez que recupere las credenciales. Para obtener más información, lea la documentación sobre [uso de la zona de aterrizaje de datos](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Para obtener más información sobre las fuentes, lea la [información general de orígenes](../../sources/home.md).
