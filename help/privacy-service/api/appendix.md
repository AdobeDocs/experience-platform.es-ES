---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Apéndice de Guía de API de Privacy Service
description: Este documento contiene información adicional para trabajar con la API de Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 6%

---

# apéndice de la guía de API de Privacy Service

Las secciones siguientes contienen información adicional para trabajar con la API de Adobe Experience Platform Privacy Service.

## Áreas de nombres de identidad estándar {#standard-namespaces}

Todas las identidades enviadas a [!DNL Privacy Service] debe proporcionarse en un área de nombres de identidad específica. Las áreas de nombres de identidad son un componente de [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md) que indican el contexto al que se relaciona una identidad.

En la tabla siguiente se describen varios tipos de identidad predefinidos de uso común que pone a disposición [!DNL Experience Platform], junto con sus asociados `namespace` valores:

| Tipo de identidad | `namespace` | `namespaceId` |
| --- | --- | --- |
| Correo electrónico | `Email` | `6` |
| Teléfono | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| UUID DE ADOBE AUDIENCE MANAGER | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple] ID para anunciantes | `IDFA` | `20915` |
| [!DNL Google] ID de anuncio | `GAID` | `20914` |
| [!DNL Windows] AYUDA | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Cada tipo de identidad también tiene un `namespaceId` valor entero, que puede utilizarse en lugar del valor `namespace` cadena al configurar el de identidad `type` propiedad a &quot;namespaceId&quot;. Consulte la sección sobre [calificadores de área de nombres](#namespace-qualifiers) para obtener más información.

Puede recuperar una lista de áreas de nombres de identidad que utiliza su organización realizando una solicitud de GET a `idnamespace/identities` punto final en la [!DNL Identity Service] API. Consulte la [Guía para desarrolladores de Identity Service](../../identity-service/api/getting-started.md) para obtener más información.

## Calificadores de área de nombres

Al especificar un `namespace` valor en [!DNL Privacy Service] API, a **calificador de área de nombres** debe incluirse en una `type` parámetro. En la tabla siguiente se describen los diferentes calificadores de área de nombres aceptados.

| Calificador | Definición |
| --------- | ---------- |
| `standard` | Una de las áreas de nombres estándar definidas globalmente, no vinculadas a un conjunto de datos de organización individual (por ejemplo, correo electrónico, número de teléfono, etc.). Se ha proporcionado el ID de área de nombres. |
| `custom` | Un área de nombres única creada en el contexto de una organización, no compartida en el [!DNL Experience Cloud]. El valor representa el nombre descriptivo (campo &quot;nombre&quot;) que se va a buscar. Se ha proporcionado el ID de área de nombres. |
| `integrationCode` | Código de integración: similar a &quot;personalizado&quot;, pero definido específicamente como el código de integración de una fuente de datos que se va a buscar. Se ha proporcionado el ID de área de nombres. |
| `namespaceId` | Indica que el valor es el ID real del área de nombres que se creó o asignó mediante el servicio de área de nombres. |
| `unregistered` | Una cadena de forma libre que no está definida en el servicio de área de nombres y que se toma &quot;tal cual&quot;. Cualquier aplicación que administre este tipo de áreas de nombres las compara con ellas y las gestiona si es adecuado para el contexto de la empresa y el conjunto de datos. No se ha proporcionado ningún ID de área de nombres. |
| `analytics` | Un área de nombres personalizada que se asigna internamente en [!DNL Analytics], no en el servicio de área de nombres. Se transfiere directamente como se especifica en la solicitud original, sin un ID de área de nombres |
| `target` | Un área de nombres personalizada entendida internamente por [!DNL Target], no en el servicio de área de nombres. Se transfiere directamente como se especifica en la solicitud original, sin un ID de área de nombres |

{style="table-layout:auto"}

## Valores de producto aceptados

En la tabla siguiente se describen los valores aceptados para especificar un producto de Adobe en `include` atributo de una solicitud de creación de trabajo.

| Producto | Valor para usar en `include` atributo |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (lago de datos) | `aepDataLake` |
| Adobe Experience Platform (Perfil del cliente en tiempo real) | `profileService` |
| Adobe Pass Authentication | `primetimeAuthentication` |
| Adobe Target | `target` |
| Atributos del cliente (CRS) | `CRS` |
| Servicio de identidad | `identity` |
| Marketo Engage | `marketo` |

{style="table-layout:auto"}
