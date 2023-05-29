---
keywords: Experience Platform;inicio;temas populares;Pinterest Ads;
title: Información general sobre orígenes de pinterest Ads
description: Obtenga información sobre cómo conectar Pinterest Ads a Adobe Experience Platform mediante API o la interfaz de usuario.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>El [!DNL Pinterest Ads] el origen está en versión beta. Lea el [Resumen de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema de publicidad de terceros. El soporte para proveedores de publicidad incluye [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) es un motor de descubrimiento visual para encontrar recetas, decoración del hogar, inspiración de estilo y otras ideas en la web. Se presentan a pequeña escala con imágenes, GIF animados y vídeos en formato de tablón. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) le permite hacer crecer su negocio y llegar a 400 millones de personas utilizando [!DNL Pinterest].

Con [!DNL Pinterest Ads], puede llegar a los usuarios a través de anuncios dirigidos para descubrir y comprar sus productos. Pines de [!DNL Pinterest Ads] son patrocinados para recibir una exposición adicional en los resultados de búsqueda relevantes. Usuarios suscritos a [!DNL Pinterest Business] Puede elegir promocionar los anclajes con mejor rendimiento existentes, crear una nueva imagen o vídeo, o incluso promocionar una imagen que se ha anclado desde un sitio web. [!DNL Pinterest Ads] ofrece varios formatos de anuncio para ayudarle a alcanzar sus objetivos específicos de campaña.

## [!DNL Pinterest] API {#pinterest-apis}

El [!DNL Pinterest Ads] fuente aprovecha el [!DNL Pinterest] API para recuperar su [!DNL Pinterest Ads] datos, junto con todo el rendimiento y las métricas. Los extremos de API admitidos son:

* [Análisis de Campaign](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análisis de grupos de anuncios](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Análisis de anuncios](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilice el [!DNL Pinterest Ads] origen desde el que se obtienen los datos [!DNL Pinterest] a Experience Platform, donde podrá ejecutar el análisis de datos. Se devuelven datos a partir de la fecha de ingesta para un intervalo antedatado de 90 días. [!DNL Pinterest Ads] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL Pinterest] API.

## Requisitos previos {#prerequisites}

El primer paso para crear un [!DNL Pinterest Ads] la conexión de origen es para asegurarse de que tiene una cuenta de desarrollador de Pinterest. Si todavía no tiene uno, visite la [apuntarse](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) página para registrarse y crear su cuenta.

### Configurar [!DNL Pinterest] aplicación y generar token de acceso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Se recomienda utilizar la variable [!DNL Pinterest] API para generar su token de acceso, ya que la generación de su token de acceso en la interfaz de usuario proporciona un acceso limitado. A través de la interfaz de usuario, solo podrá acceder a los siguientes ámbitos: `pins:read`, `boards:read` y `user_accounts:read`. Esta limitación no es adecuada para su uso con los extremos de análisis del [!DNL Pinterest] API.

Para generar el token de acceso, lea la [!DNL Pinterest] guías sobre [configuración de la aplicación](https://developers.pinterest.com/docs/getting-started/set-up-app/) y [autenticación mediante OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Recopilar credenciales necesarias {#gather-required-credentials}

Para poder conectarse [!DNL Pinterest Ads] En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Token de acceso | El [!DNL Pinterest Ads] token de acceso para su cuenta de usuario. La cuenta de usuario del token debe ser el propietario del especificado [!DNL Pinterest Ad] cuenta o tiene una de las funciones necesarias otorgadas a través de Acceso empresarial: Administrador, Analista o Administrador de campañas. Para obtener más información sobre el token de acceso, consulte la [[!DNL Pinterest] guía para generar el token de acceso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID de cuenta de anuncio | Los relacionados [!DNL Pinterest Ads] agregue el ID de cuenta de su unidad empresarial. Para obtener información sobre cómo recuperar el ID de cuenta de Ad. Visite la [[!DNL Pinterest] Guía de búsqueda de ID en el Administrador de anuncios](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campaña, grupo de anuncios o ID de anuncio | El `campaign`, `ad group`, o `ad` ID que se corresponden con su ID de cuenta de publicidad. Para obtener los ID necesarios, vaya a [!DNL Pinterest] página para **Pinterest Business Hub** > **Resumen de cuenta de publicidad** > **Campañas** / **Grupos de publicidad** / **Anuncios** y copie los ID necesarios mencionados justo debajo de cada uno de sus nombres. |

>[!NOTE]
>
>El [!DNL Pinterest] API proporciona API individuales para recuperar datos asociados a cada ID. Por lo tanto, solo debe pasar los ID correspondientes para el tipo de ID que le interesa.

## Mecanismos de protección {#guardrails}

En las secciones siguientes se proporciona información sobre las protecciones de datos para [!DNL Pinterest].

### [!DNL Pinterest] intervalo de fecha {#pinterest-date-range}

El [!DNL Pinterest] La API admite un `start_date` y un `end_date` para recuperar datos de analytics entre un intervalo de fechas determinado.

* El `start_date` no puede ser más de 90 días antes de la fecha actual.
* El `end_date` no puede ser superior a 90 días después de la `start_date`.

Al programar el flujo de datos, debe configurar una de las siguientes opciones de frecuencia e intervalo:

| Frecuencia | Intervalo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por ejemplo, si la ingesta se establece el 15 de marzo de 2023 con una configuración de frecuencia e intervalo configurada en `Day=1` o `Hour=24`y, a continuación, el [!DNL Pinterest] La API solo recuperaría datos desde el 15 de diciembre de 2022, porque el cálculo está retrasado durante 90 días.

### [!DNL Pinterest] intervalo de tiempo {#pinterest-time-range}

El [!DNL Pinterest] API admite diferentes tipos de granularidad de tiempo para la forma en que se pueden recuperar los datos:

| Granularidad de tiempo | Descripción |
| --- | --- |
| **TOTAL** | Las métricas de datos se agregan en un intervalo de fechas especificado. |
| **DÍA** | Las métricas de datos se desglosan diariamente. |
| **HOUR** | Las métricas de datos se desglosan por hora. |
| **SEMANAL** | Las métricas de datos se desglosan semanalmente. |
| **MENSUAL** | Las métricas de datos se desglosan mensualmente. |

Para Platform, la variable [!DNL Pinterest Ads] el origen está configurado internamente para `Day`, lo que significa que los datos se agregarán diariamente. Por ejemplo, con `impressions recorded` como métrica, ya que la granularidad está configurada como `DAY`, obtendría lo siguiente `xx` impresiones sobre `day 1`, `yy` impresiones sobre `day 2` y demás.

>[!IMPORTANT]
>
>Pinterest impone a su API un límite de 1000 llamadas a la API diarias para leer información de anuncios, grupos de anuncios o campañas de publicidad. Para obtener información sobre los límites de tasa aplicables a las llamadas a la API subyacentes, consulte la [[!DNL Pinterest] documentación sobre los límites de velocidad](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connect [!DNL Pinterest Ads] a Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Pinterest Ads] Vaya a Platform mediante las API o la interfaz de usuario de:

### Connect [!DNL Pinterest Ads] a Platform mediante API {#connect-to-platform-using-api}

* [Crear una conexión base de Pinterest mediante la API de Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Creación de un flujo de datos para una fuente de publicidad mediante la API de Flow Service](../../tutorials/api/collect/advertising.md)

### Connect [!DNL Pinterest Ads] a Platform mediante la IU {#connect-to-platform-using-ui}

* [Crear una conexión de origen de Pinterest en la interfaz de usuario](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Crear un flujo de datos para una conexión de origen de publicidad en la interfaz de usuario](../../tutorials/ui/dataflow/advertising.md)
