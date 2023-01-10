---
keywords: Experience Platform;inicio;temas populares;asignación de Audience Manager;asignación de audience manager
solution: Experience Platform
title: Asignación de campos para el conector de origen de Adobe Audience Manager
description: Obtenga información sobre cómo asignar datos de Adobe Audience Manager (datos en tiempo real, integrados y de perfil) a los campos correspondientes del Modelo de datos de experiencia (XDM) para el conector de origen del Audience Manager.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---

# asignaciones de campos de Audience Manager

Las tablas siguientes contienen las asignaciones entre los campos de los datos de Adobe Audience Manager (en tiempo real, integrados y datos de perfil) y sus campos XDM correspondientes.

Consulte la [Diccionario de campo XDM](../../../../xdm/schema/field-dictionary.md) para obtener más información sobre cada campo XDM.

## Datos en tiempo real

Tipo: Datos en tiempo real

| Campo de datos en tiempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo para áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo para áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → tipo</li><li>fabricante → fabricante</li><li>marketingName → modelo</li><li>modelNumber → modelo</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvincia</li><li>d_city → ciudad</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitud</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nombre de os </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Datos de perfil

Tipo: XDM de perfil

| Campo de perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
