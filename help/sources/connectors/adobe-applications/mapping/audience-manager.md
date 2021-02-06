---
keywords: Experience Platform;inicio;temas populares;asignación de Audience Manager;asignación de administrador de audiencias
solution: Experience Platform
title: Campos de asignación para el conector de origen de Adobe Audience Manager
topic: overview
description: Obtenga información sobre cómo asignar datos de Adobe Audience Manager (en tiempo real, integrados y datos de Perfil) a los campos correspondientes del Modelo de datos de experiencia (XDM) para el conector de origen del Audience Manager.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Asignaciones de campos Audience Manager

Las siguientes tablas contienen las asignaciones entre los campos de los datos de Adobe Audience Manager (Tiempo real, En el tablero y Datos de Perfil) y sus correspondientes campos XDM.

Consulte el [diccionario de campo XDM](../../../../xdm/schema/field-dictionary.md) para obtener más información sobre cada campo XDM.

## Datos en tiempo real

Tipo: Datos en tiempo real

| Campo de datos en tiempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *Solo para Áreas de nombres presentes en endUserIds y solo para el primer valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo para Áreas de nombres presentes en endUserIds y solo el primer valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primarioHardwareType → tipo</li><li>fabricante → fabricante</li><li>marketingName → modelo</li><li>modelNumber → modelo</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvincia</li><li>d_city → ciudad</li><li>d_postal → postalCode</li><li>d_lat → latitud</li><li>d_longitude → longitud</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nombre de SO </li><li>d_os_version → os_version</li></ul> |

## Datos de perfil

Tipo: Perfil XDM

| Campo perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
