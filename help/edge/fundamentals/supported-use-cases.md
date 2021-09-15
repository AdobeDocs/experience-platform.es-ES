---
title: Casos de uso compatibles con el SDK web de Adobe Experience Platform
description: Descubra qué casos de uso son compatibles con el SDK web de Adobe Experience Platform.
keywords: sdk web;casos de uso
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 18%

---

# Casos de uso admitidos

Esta página enumera los casos de uso admitidos para el SDK web, con vínculos a información adicional.

## General

| Caso de uso | Más información |
| --- | --- |
| SDK simplificado único |  |
| Red de recopilación de datos globales |  |
| Consentimiento basado en el curso |  |
| Recopilar el consentimiento del cliente según diversos estándares | <ul><li>[Compatibilidad con el consentimiento de Adobe 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[Compatibilidad con IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Integración del SDK para enviar señales de consentimiento a la red perimetral](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| Compatibilidad con ECID | Para obtener información sobre la recuperación del ECID, consulte nuestra documentación [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) y [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Recopilar varias entidades |  |
| Compatibilidad con Device Graph (público/privado) | [Documentación](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Enviar datos a varias organizaciones de la página | [Documentación](./interacting-with-multiple-properties.md) |
| Registros e informes de errores detallados |  |
| Rastrear solicitudes del lado del cliente y del servidor |  |
| extensión de etiqueta | [Documentos de extensión del SDK web](../../tags/extensions/web/sdk/overview.md) |
| Herramientas de depuración disponibles | [Extensión de Debugger ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) y  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Caso de uso | Más información |
| --- | --- |
| Enviar eventos de experiencia |  |
| Offer Decisioning | [Documentación](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Si el conjunto de datos está habilitado para el perfil, la capacidad de enviar datos al perfil de datos del cliente en tiempo real en tiempo real |  |
| Enviar datos al Customer Journey Analytics en tiempo real |  |
| Escribir consentimiento en perfil | [Documentación](../../landing/governance-privacy-security/consent/sdk.md) |
| Reenviar datos del lado del servidor en tiempo real a terceros | [Documentación](../../tags/ui/event-forwarding/overview.md) |
| Compatibilidad con el área de nombres de identidad |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Caso de uso | Más información |
| --- | --- |
| Analytics para Target (A4T) |  |
| Sin latencia de Analytics for Target (A4T) |  |
| Etiquetado de grupos múltiples |  |
| Filtrado de bots |  |
| Props, eVars y eventos |  |
| Compatibilidad de ListVar con Adobe Analytics |  |
| SO y versión del explorador |  |
| Variables integradas | [Variables asignadas automáticamente](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| Reglas de VISTA/reglas de procesamiento |  |
| Compatibilidad con atributos del visitante |  |
| Compatibilidad con vínculos de salida |  |
| Vínculos personalizados/Vínculos de descarga |  |
| Seguimiento de estados y acciones |  |
| Serialización de eventos para eventos estándar |  |
| Variable products | [Documentación](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Caso de uso | Más información |
| --- | --- |
| Todos los tipos de actividades |  |
| Compatibilidad con Compositor de experiencias visuales nativas y SPA | [Documentación](../personalization/adobe-target/spa-implementation.md) |
| Compositor basado en formularios |  |
| Compatibilidad con mbox global | [Documentación](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Mboxes personalizados | [Documentación](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics para Target (A4T) |  |
| Compatibilidad con el entorno |  |
| Compatibilidad con Workspace |  |
| Vínculos de control de calidad en Adobe Target |  |
| Objetivo basado en la ubicación geográfica o el dispositivo en Adobe Target |  |
| Compatibilidad con atributos del visitante |  |
| Scripts de perfil |  |
| XDM se convierte en parámetros de mbox |  |
| Ofertas de redireccionamiento compatibles con los informes de A4T | [Documentación](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Actualización del perfil de Target | [Documentación](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Recomendaciones |  |
| mBox ID de terceros |  |
| Tokens de respuesta | [Documentación](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Caso de uso | Más información |
| --- | --- |
| Audience Analytics |  |
| Uso compartido de segmentos con Adobe Analytics |  |
| Compatibilidad con atributos del visitante |  |
| Sincronizaciones de socios |  |
| Destinos de URL |  |
| Destinos de cookies |  |
| Compatibilidad con el entorno |  |
| Sincronización de áreas de nombres de Adobe Experience Platform con fuentes de datos de Audience Manager |  |
| ID autenticados o conocidos |  |

{style=&quot;table-layout:auto&quot;}
