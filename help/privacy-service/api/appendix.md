---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Áreas de nombres y calificadores de identidad aceptados
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Apéndice

## Áreas de nombres de identidad estándar

Todas las identidades que se envían a Privacy Service deben proporcionarse con una Área de nombres de identidad específica. Las Áreas de nombres de identidad son un componente de [Adobe Experience Platform Identity Service](../../identity-service/home.md) que indica el contexto al que se relaciona una identidad.

La siguiente tabla describe varios tipos de identidad predefinidos y utilizados comúnmente disponibles en la plataforma de experiencias, junto con sus `namespace` valores asociados:

| Tipo de identidad | `namespace` | `namespaceId` |
| --- | --- | --- |
| Correo electrónico | Correo electrónico | 6 |
| Phone | Phone | 7 |
| Adobe Advertising Cloud ID | Adcloud | 411 |
| UUID de Adobe Audiencia Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| ID de Adobe Destinatario | TNTID | 9 |
| ID de Apple para anunciantes | IDFA | 20915 |
| ID de publicidad de Google | GAID | 20914 |
| AID de Windows | WAID | 8 |

>[!NOTE] Cada tipo de identidad también tiene un valor `namespaceId` entero, que se puede utilizar en lugar de la `namespace` cadena al establecer la propiedad `type` de la identidad en &quot;namespaceId&quot;. Consulte la sección sobre calificadores [de](#namespace-qualifiers) Área de nombres para obtener más información.

Puede recuperar una lista de Áreas de nombres de identidad que esté utilizando su organización haciendo una solicitud GET al extremo en la API de servicio de identidad `idnamespace/identities` . Consulte la guía [para desarrolladores de](../../identity-service/api/getting-started.md) Identity Service para obtener más información.

## Calificadores de Área de nombres

Al especificar un `namespace` valor en la API de Privacy Service, se debe incluir un calificador **de** Área de nombres en un `type` parámetro correspondiente. La siguiente tabla describe los diferentes calificadores de Área de nombres aceptados.

| Cualificador | Definición |
| --------- | ---------- |
| standard | Una de las Áreas de nombres estándar definidas globalmente, no vinculada a un conjunto de datos de una organización individual (por ejemplo, correo electrónico, número de teléfono, etc.). Se proporciona el ID de Área de nombres. |
| personalizado | Una Área de nombres única creada en el contexto de una organización, no compartida en Experience Cloud. El valor representa el nombre descriptivo (campo &quot;nombre&quot;) que se va a buscar. Se proporciona el ID de Área de nombres. |
| integrationCode | Código de integración: similar a &quot;personalizado&quot;, pero definido específicamente como el código de integración de un origen de datos que se va a buscar. Se proporciona el ID de Área de nombres. |
| namespaceId | Indica que el valor es el ID real de la Área de nombres que se creó o asignó a través del servicio de Área de nombres. |
| no registrado | Una cadena improvisada que no está definida en el servicio de Área de nombres y se toma &quot;tal cual&quot;. Cualquier aplicación que gestione este tipo de Áreas de nombres comprueba su existencia y gestiona, si procede, el contexto de compañía y el conjunto de datos. No se proporciona ningún ID de Área de nombres. |
| analytics | Área de nombres personalizada que se asigna internamente en Analytics, no en el servicio de Área de nombres. Esto se pasa directamente según lo especificado por la solicitud original, sin un ID de Área de nombres |
| Target | Una Área de nombres personalizada entendida internamente por Destinatario, no en el servicio de Área de nombres. Esto se pasa directamente según lo especificado por la solicitud original, sin un ID de Área de nombres |

## Valores de producto aceptados

La siguiente tabla describe los valores aceptados para especificar un producto de Adobe en el `include` atributo de una solicitud de creación de trabajos.

| Producto | Valor que se usará en el `include` atributo |
--- | ---
| Adobe Advertizing Cloud | &quot;Adcloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticación de Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Servicio de registro de clientes | &quot;CRS&quot; |
| Perfil del cliente en tiempo real | &quot;ProfileService&quot; |