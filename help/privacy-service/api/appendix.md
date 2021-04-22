---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Apéndice de la guía de API del Privacy Service
topic-legacy: developer guide
description: Este documento contiene información adicional para trabajar con la API de Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 5%

---

# apéndice de la guía de API del Privacy Service

Las secciones siguientes contienen información adicional para trabajar con la API de Adobe Experience Platform Privacy Service.

## Espacios de nombres de identidad estándar {#standard-namespaces}

Todas las identidades que se envían a [!DNL Privacy Service] deben proporcionarse en un área de nombres de identidad específica. Las áreas de nombres de identidad son un componente de [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md) que indica el contexto al que se relaciona una identidad.

La siguiente tabla describe varios tipos de identidad predefinidos utilizados comúnmente que están disponibles en [!DNL Experience Platform], junto con sus valores `namespace` asociados:

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
>Cada tipo de identidad también tiene un valor entero `namespaceId`, que puede utilizarse en lugar de la cadena `namespace` al establecer la propiedad `type` de la identidad en &quot;namespaceId&quot;. Consulte la sección sobre [calificadores de espacio de nombres](#namespace-qualifiers) para obtener más información.

Puede recuperar una lista de áreas de nombres de identidad en uso por su organización realizando una solicitud de GET al extremo `idnamespace/identities` en la API [!DNL Identity Service]. Consulte la [Guía para desarrolladores del servicio de identidad](../../identity-service/api/getting-started.md) para obtener más información.

## Calificadores de área de nombres

Al especificar un valor `namespace` en la API [!DNL Privacy Service], se debe incluir un calificador de **área de nombres** en un parámetro `type` correspondiente. La siguiente tabla describe los diferentes calificadores de área de nombres aceptados.

| Cualificador | Definición |
| --------- | ---------- |
| `standard` | Una de las áreas de nombres estándar definidas globalmente, no está vinculada a un conjunto de datos de organización individual (por ejemplo, correo electrónico, número de teléfono, etc.). Se proporciona el ID de área de nombres. |
| `custom` | Un espacio de nombres único creado en el contexto de una organización, no compartido entre [!DNL Experience Cloud]. El valor representa el nombre descriptivo (campo &quot;nombre&quot;) que se va a buscar. Se proporciona el ID de área de nombres. |
| `integrationCode` | Código de integración : similar a &quot;personalizado&quot;, pero definido específicamente como el código de integración de una fuente de datos que se va a buscar. Se proporciona el ID de área de nombres. |
| `namespaceId` | Indica que el valor es el ID real del área de nombres que se creó o asignó a través del servicio de área de nombres. |
| `unregistered` | Cadena de forma libre que no está definida en el servicio de área de nombres y se toma &quot;tal cual&quot;. Cualquier aplicación que gestione este tipo de áreas de nombres comprueba su existencia y gestiona, si corresponde, el contexto de la empresa y el conjunto de datos. No se proporciona ningún ID de área de nombres. |
| `analytics` | Un área de nombres personalizada que se asigna internamente en [!DNL Analytics], no en el servicio de área de nombres. Esto se transfiere directamente según lo especificado por la solicitud original, sin un ID de área de nombres |
| `target` | Un espacio de nombres personalizado comprendido internamente por [!DNL Target], no en el servicio de espacio de nombres. Esto se transfiere directamente según lo especificado por la solicitud original, sin un ID de área de nombres |

{style=&quot;table-layout:auto&quot;}

## Valores de producto aceptados

La siguiente tabla describe los valores aceptados para especificar un producto de Adobe en el atributo `include` de una solicitud de creación de trabajo.

| Producto | Valor que se utiliza en el atributo `include` |
| --- | --- |
| Adobe Advertising Cloud | `AdCloud` |
| Adobe Analytics | `Analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `Campaign` |
| Adobe Experience Platform | `aepDataLake` |
| Autenticación de Adobe Primetime | `primetimeAuthentication` |
| Adobe Target | `Target` |
| Servicio de registro de cliente | `CRS` |
| Perfil del cliente en tiempo real | `ProfileService` |

{style=&quot;table-layout:auto&quot;}