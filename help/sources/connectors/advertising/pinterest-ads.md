---
keywords: Experience Platform;inicio;temas populares;Pinterest Ads;
title: Información general sobre la fuente de anuncios de pinterest
description: Obtenga información sobre cómo conectar Pinterest Ads a Adobe Experience Platform mediante API o la interfaz de usuario.
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>La variable [!DNL Pinterest Ads] el origen está en versión beta. Lea el [Resumen de fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform permite la ingesta de datos desde un sistema de publicidad de terceros. La compatibilidad con los proveedores de publicidad incluye [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) es un motor de descubrimiento visual para encontrar recetas, decoración doméstica, inspiración de estilo y otras ideas en la web. Estos se presentan en pequeña escala utilizando imágenes, GIF animados y vídeos en formato de tablero. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) le permite ampliar su negocio y llegar a 400 millones de personas utilizando [!DNL Pinterest].

con [!DNL Pinterest Ads], puede llegar a los usuarios a través de anuncios orientados para descubrir y comprar sus productos. Anclajes desde [!DNL Pinterest Ads] están patrocinados para recibir exposición adicional en los resultados de búsqueda relevantes. Usuarios suscritos a [!DNL Pinterest Business] puede elegir promocionar los pines de mejor rendimiento existentes, crear una nueva imagen o vídeo o incluso promocionar una imagen anclada desde un sitio web. [!DNL Pinterest Ads] ofrece varios formatos de anuncio para ayudarle a alcanzar sus objetivos de campaña específicos.

## [!DNL Pinterest] API {#pinterest-apis}

La variable [!DNL Pinterest Ads] source aprovecha el [!DNL Pinterest] API para recuperar su [!DNL Pinterest Ads] junto con todas las métricas y de rendimiento. Los extremos de API admitidos son:

* [Análisis de campañas](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análisis de grupos de publicidad](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Análisis de anuncios](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilice la variable [!DNL Pinterest Ads] fuente desde la que se extraen los datos [!DNL Pinterest] en Experience Platform, donde puede ejecutar análisis de datos. Los datos se devuelven a partir de la fecha de ingesta durante un intervalo con fecha anterior de 90 días. [!DNL Pinterest Ads] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL Pinterest] API.

## Requisitos previos {#prerequisites}

El primer paso para crear un [!DNL Pinterest Ads] la conexión de origen es para asegurarse de que tiene una cuenta de desarrollador de Pinterest. Si todavía no tiene uno, visite [registrar](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) para registrar y crear su cuenta.

### Configuración [!DNL Pinterest] aplicación y generar token de acceso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Se recomienda usar la variable [!DNL Pinterest] API para generar el token de acceso porque la generación del token de acceso en la interfaz de usuario proporciona un acceso limitado. A través de la interfaz de usuario solo puede acceder a los siguientes ámbitos: `pins:read`, `boards:read` y `user_accounts:read`. Esta limitación no es adecuada para su uso con los extremos de análisis de la variable [!DNL Pinterest] API.

Para generar el token de acceso, lea la [!DNL Pinterest] guías sobre [configuración de la aplicación](https://developers.pinterest.com/docs/getting-started/set-up-app/) y [autenticación mediante OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Recopilar las credenciales necesarias {#gather-required-credentials}

Para conectarse [!DNL Pinterest Ads] en Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Token de acceso | La variable [!DNL Pinterest Ads] token de acceso para su cuenta de usuario. La cuenta de usuario del token debe ser el propietario del [!DNL Pinterest Ad] o que se les otorgue una de las funciones necesarias a través de Acceso empresarial: Administrador, Analista o Administrador de campañas. Para obtener más información sobre el token de acceso, consulte la [[!DNL Pinterest] guía sobre la generación del token de acceso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID de cuenta de anuncio | El [!DNL Pinterest Ads] ID de cuenta de anuncio para su unidad de negocio. Para obtener información sobre cómo recuperar el ID de cuenta de anuncio. Visite la [[!DNL Pinterest] guía para encontrar ID en el Administrador de anuncios](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campaña, grupo de publicidad o ID de publicidad | La variable `campaign`, `ad group`o `ad` ID que se correspondan con el ID de su cuenta publicitaria. Para obtener los ID necesarios, vaya a la [!DNL Pinterest] página para **Pinterest Business Hub** > **Resumen de la cuenta del anuncio** > **Campañas** / **Grupos de publicidad** / **Publicidades** y copie los ID requeridos mencionados justo debajo de cada uno de sus nombres. |

>[!NOTE]
>
>La variable [!DNL Pinterest] La API proporciona API individuales para recuperar datos asociados con cada ID. Por lo tanto, solo debe pasar los ID correspondientes para el tipo de ID que le interese.

## Mecanismos de protección {#guardrails}

Las secciones siguientes proporcionan información sobre las protecciones de datos para [!DNL Pinterest].

### [!DNL Pinterest] intervalo de fechas {#pinterest-date-range}

La variable [!DNL Pinterest] La API admite ambas `start_date` y `end_date` para recuperar datos de análisis entre un intervalo de fechas determinado.

* La variable `start_date` no puede ser superior a 90 días antes de la fecha actual.
* La variable `end_date` no puede ser superior a 90 días después del `start_date`.

Al programar el flujo de datos, debe configurar una de las siguientes opciones de frecuencia e intervalo:

| Frecuencia | Intervalo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por ejemplo, si la ingesta se establece el 15 de marzo de 2023 con una configuración de frecuencia e intervalo configurada en `Day=1` o `Hour=24`, luego la variable [!DNL Pinterest] La API solo recuperaría datos desde el 15 de diciembre de 2022 porque el cálculo lleva 90 días de retraso.

### [!DNL Pinterest] intervalo de tiempo {#pinterest-time-range}

La variable [!DNL Pinterest] La API admite distintos tipos de granularidad temporal para la forma en que se pueden recuperar los datos:

| Granularidad de tiempo | Descripción |
| --- | --- |
| **TOTAL** | Las métricas de datos se acumulan en un intervalo de fechas especificado. |
| **DÍA** | Las métricas de datos se desglosan diariamente. |
| **HORA** | Las métricas de datos se desglosan por hora. |
| **SEMANAL** | Las métricas de datos se desglosan semanalmente. |
| **MENSUAL** | Las métricas de datos se desglosan mensualmente. |

Para Platform, la variable [!DNL Pinterest Ads] el origen se configura internamente para `Day`, lo que significa que los datos se agregarán diariamente. Por ejemplo, al usar `impressions recorded` como métrica, ya que la granularidad está configurada como un `DAY`, obtendrá `xx` impresiones en `day 1`, `yy` impresiones en `day 2` y así sucesivamente.

>[!IMPORTANT]
>
>Pinterest impone un límite de tasa de 1000 llamadas diarias a la API para leer información de anuncios, grupos de anuncios o campañas de publicidad. Para obtener información sobre los límites de velocidad aplicables a las llamadas de API subyacentes, consulte la [[!DNL Pinterest] documentación sobre límites de tasa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connect [!DNL Pinterest Ads] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo conectar [!DNL Pinterest Ads] a Platform mediante API o la interfaz de usuario:

### Connect [!DNL Pinterest Ads] a Platform mediante API {#connect-to-platform-using-api}

* [Creación de una conexión base de Pinterest mediante la API de servicio de flujo](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Exploración de tablas de datos mediante la API de servicio de flujo](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen publicitario mediante la API de servicio de flujo](../../tutorials/api/collect/advertising.md)

### Connect [!DNL Pinterest Ads] a Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen de Pinterest en la interfaz de usuario](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Crear un flujo de datos para una conexión de origen de publicidad en la interfaz de usuario](../../tutorials/ui/dataflow/advertising.md)
