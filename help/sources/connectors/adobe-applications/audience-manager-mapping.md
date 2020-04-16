---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Campo de asignación del Administrador de Audiencias
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Campo de asignación del Administrador de Audiencias

Las siguientes tablas contienen las asignaciones entre los campos de los datos de Adobe Audiencia Manager (datos en tiempo real, integrados y de Perfil) y sus correspondientes campos XDM.

Consulte el diccionario [de campo](../../../xdm/schema/field-dictionary.md) XDM para obtener más información sobre cada campo XDM.

## Datos en tiempo real

Tipo: Datos en tiempo real

| Campo de datos en tiempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo para Áreas de nombres presentes en endUserIds y solo para el primer valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds: *solo para Áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primarioHardwareType → tipo</li><li>fabricante → fabricante</li><li>marketingName → modelo</li><li>modelNumber → modelo</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvincia</li><li>d_city → ciudad</li><li>d_postal → postalCode</li><li>d_lat → latitud</li><li>d_longitude → longitud</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nombre de SO </li><li>d_os_version → os_version</li></ul> |
| `Signals` | ExperienceEvent.signals |

## Datos de entrada **(obsoleto)**

Tipo: ExperienceEvent

| Campo de entrada | Campo XDM |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Los campos entrantes están programados para quedar obsoletos en una versión futura.

## Datos de Perfil

Tipo: Perfil XDM

| Campo Perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
