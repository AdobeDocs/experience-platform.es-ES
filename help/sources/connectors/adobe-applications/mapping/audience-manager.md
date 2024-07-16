---
keywords: Experience Platform;inicio;temas populares;asignación de Audience Manager;asignación de audience manager
solution: Experience Platform
title: Asignación de campos para el conector de Adobe Audience Manager Source
description: Obtenga información sobre cómo asignar datos de Adobe Audience Manager (datos de tiempo real, integrados y de perfil) a los campos correspondientes del modelo de datos de experiencia (XDM) para el conector de origen del Audience Manager.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Asignaciones de campos de Audience Manager

Las siguientes tablas contienen las asignaciones entre los campos de datos de Adobe Audience Manager (datos en tiempo real, integrados y de perfil) y sus campos XDM correspondientes.

Consulte el [diccionario de campo XDM](../../../../xdm/schema/field-dictionary.md) para obtener más información sobre cada campo XDM.

## Datos en tiempo real

Tipo: datos en tiempo real

| Campo de datos en tiempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo para áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds: *Solo para áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>tipo de → primaryHardwareType</li><li>fabricante → fabricante</li><li>modelo de → marketingName</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → city</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nombre del sistema operativo </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## Datos de perfil

Tipo: XDM de perfil

| Campo de perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
