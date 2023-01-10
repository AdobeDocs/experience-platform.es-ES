---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Apéndice de la guía de API del Privacy Service
description: Este documento contiene información adicional para trabajar con la API de Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# apéndice de la guía de API del Privacy Service

Las secciones siguientes contienen información adicional para trabajar con la API de Adobe Experience Platform Privacy Service.

## Espacios de nombres de identidad estándar {#standard-namespaces}

Todas las identidades que se envían a [!DNL Privacy Service] debe proporcionarse en un área de nombres de identidad específica. Las áreas de nombres de identidad son un componente de [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md) que indican el contexto al que se relaciona una identidad.

La siguiente tabla describe varios tipos de identidad predefinidos utilizados que se utilizan con más frecuencia y que están disponibles en [!DNL Experience Platform], junto con sus `namespace` valores:

| Tipo de identidad | `namespace` | `namespaceId` |
| --- | --- | --- |
| Correo electrónico | `Email` | `6` |
| Phone | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| UUID de Adobe Audience Manager | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] ID para anunciantes | `IDFA` | `20915` |
| [!DNL Google] ID de anuncio | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Cada tipo de identidad también tiene un `namespaceId` valor entero, que puede utilizarse en lugar de la variable `namespace` cadena al configurar la variable `type` a &quot;namespaceId&quot;. Consulte la sección sobre [calificadores de área de nombres](#namespace-qualifiers) para obtener más información.

Puede recuperar una lista de áreas de nombres de identidad en uso por su organización realizando una solicitud de GET al `idnamespace/identities` en la variable [!DNL Identity Service] API. Consulte la [Guía para desarrolladores del servicio de identidad](../../identity-service/api/getting-started.md) para obtener más información.

## Calificadores de área de nombres

Al especificar un `namespace` en la variable [!DNL Privacy Service] API, un **calificador de área de nombres** debe incluirse en un `type` parámetro. La siguiente tabla describe los diferentes calificadores de área de nombres aceptados.

| Cualificador | Definición |
| --------- | ---------- |
| `standard` | Una de las áreas de nombres estándar definidas globalmente, no está vinculada a un conjunto de datos de organización individual (por ejemplo, correo electrónico, número de teléfono, etc.). Se proporciona el ID de área de nombres. |
| `custom` | Un área de nombres única creada en el contexto de una organización, no compartida entre [!DNL Experience Cloud]. El valor representa el nombre descriptivo (campo &quot;nombre&quot;) que se va a buscar. Se proporciona el ID de área de nombres. |
| `integrationCode` | Código de integración : similar a &quot;personalizado&quot;, pero definido específicamente como el código de integración de una fuente de datos que se va a buscar. Se proporciona el ID de área de nombres. |
| `namespaceId` | Indica que el valor es el ID real del área de nombres que se creó o asignó a través del servicio de área de nombres. |
| `unregistered` | Cadena de forma libre que no está definida en el servicio de área de nombres y se toma &quot;tal cual&quot;. Cualquier aplicación que gestione este tipo de áreas de nombres comprueba su existencia y gestiona, si corresponde, el contexto de la empresa y el conjunto de datos. No se proporciona ningún ID de área de nombres. |
| `analytics` | Un espacio de nombres personalizado que se asigna internamente en [!DNL Analytics], no en el servicio de área de nombres. Esto se transfiere directamente según lo especificado por la solicitud original, sin un ID de área de nombres |
| `target` | Un espacio de nombres personalizado que entienda internamente [!DNL Target], no en el servicio de área de nombres. Esto se transfiere directamente según lo especificado por la solicitud original, sin un ID de área de nombres |

{style=&quot;table-layout:auto&quot;}

## Valores de producto aceptados

La siguiente tabla describe los valores aceptados para especificar un producto de Adobe en la variable `include` de una solicitud de creación de trabajo.

| Producto | Valor que se utilizará en la variable `include` attribute |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (lago de datos) | `aepDataLake` |
| Adobe Experience Platform (Perfil del cliente en tiempo real) | `profileService` |
| Autenticación de Adobe Primetime | `primetimeAuthentication` |
| Adobe Target | `target` |
| Atributos del cliente (CRS) | `CRS` |
| Servicio de identidad | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
