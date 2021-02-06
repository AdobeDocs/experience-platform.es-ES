---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Apéndice de la Guía de API de Privacy Service
topic: developer guide
description: Este documento contiene información adicional para trabajar con la API de Privacy Service.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 9%

---


# Apéndice de la guía de la API de Privacy Service

Las secciones siguientes contienen información adicional para trabajar con la API de Adobe Experience Platform Privacy Service.

## Áreas de nombres de identidad estándar {#standard-namespaces}

Todas las identidades que se envían a [!DNL Privacy Service] deben proporcionarse bajo una Área de nombres de identidad específica. Las Áreas de nombres de identidad son un componente de [Adobe Experience Platform Identity Service](../../identity-service/home.md) que indica el contexto al que se relaciona una identidad.

La siguiente tabla describe varios tipos de identidad predefinidos y utilizados comúnmente disponibles mediante [!DNL Experience Platform], junto con sus valores `namespace` asociados:

| Tipo de identidad | `namespace` | `namespaceId` |
| --- | --- | --- |
| Correo electrónico | Correo electrónico | 6 |
| Phone | Teléfono | 7 |
| Adobe Advertising Cloud ID | Adcloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] ID para anunciantes | IDFA | 2015 |
| [!DNL Google] ID de anuncio | GAID | 2014 |
| [!DNL Windows] AYID | WAID | 8 |

>[!NOTE]
>
>Cada tipo de identidad también tiene un valor entero `namespaceId`, que puede utilizarse en lugar de la cadena `namespace` al establecer la propiedad `type` de la identidad en &quot;namespaceId&quot;. Consulte la sección sobre [calificadores de Área de nombres](#namespace-qualifiers) para obtener más información.

Puede recuperar una lista de Áreas de nombres de identidad que esté utilizando su organización haciendo una solicitud de GET al extremo `idnamespace/identities` en la API [!DNL Identity Service]. Consulte la [guía para desarrolladores de Identity Service](../../identity-service/api/getting-started.md) para obtener más información.

## Calificadores de Área de nombres

Al especificar un valor `namespace` en la API [!DNL Privacy Service], debe incluirse un calificador de Área de nombres **** en un parámetro `type` correspondiente. La siguiente tabla describe los diferentes calificadores de Área de nombres aceptados.

| Cualificador | Definición |
| --------- | ---------- |
| standard | Una de las Áreas de nombres estándar definidas globalmente, no vinculada a un conjunto de datos de una organización individual (por ejemplo, correo electrónico, número de teléfono, etc.). Se proporciona el ID de Área de nombres. |
| personalizado | Una Área de nombres única creada en el contexto de una organización, no compartida entre [!DNL Experience Cloud]. El valor representa el nombre descriptivo (campo &quot;nombre&quot;) que se va a buscar. Se proporciona el ID de Área de nombres. |
| integrationCode | Código de integración: similar a &quot;personalizado&quot;, pero definido específicamente como el código de integración de un origen de datos que se va a buscar. Se proporciona el ID de Área de nombres. |
| namespaceId | Indica que el valor es el ID real de la Área de nombres que se creó o asignó a través del servicio de Área de nombres. |
| no registrado | Una cadena improvisada que no está definida en el servicio de Área de nombres y se toma &quot;tal cual&quot;. Cualquier aplicación que gestione este tipo de Áreas de nombres comprueba su existencia y gestiona, si procede, el contexto de compañía y el conjunto de datos. No se proporciona ningún ID de Área de nombres. |
| analytics | Una Área de nombres personalizada que se asigna internamente en [!DNL Analytics], no en el servicio de Área de nombres. Esto se pasa directamente según lo especificado por la solicitud original, sin un ID de Área de nombres |
| Target | Una Área de nombres personalizada entendida internamente por [!DNL Target], no en el servicio de Área de nombres. Esto se pasa directamente según lo especificado por la solicitud original, sin un ID de Área de nombres |

## Valores de producto aceptados

La siguiente tabla describe los valores aceptados para especificar un producto de Adobe en el atributo `include` de una solicitud de creación de trabajos.

| Producto | Valor para usar en el atributo `include` |
--- | ---
| Adobe Advertising Cloud | &quot;Adcloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticación de Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Servicio de registro de clientes | &quot;CRS&quot; |
| Perfil del cliente en tiempo real | &quot;ProfileService&quot; |