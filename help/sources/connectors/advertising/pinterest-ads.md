---
keywords: Experience Platform;inicio;temas populares;Pinterest Ads;
title: Información general sobre Pinterest Ads Source
description: Obtenga información sobre cómo conectar Pinterest Ads a Adobe Experience Platform mediante API o la interfaz de usuario.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>El origen [!DNL Pinterest Ads] está en la versión beta. Lea [Resumen de fuentes](../../home.md#terms-and-conditions) para obtener más información sobre cómo usar conectores con etiqueta beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde un sistema de publicidad de terceros. Los proveedores de publicidad admiten [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) es un motor de descubrimiento visual que permite encontrar recetas, decoración del hogar, inspiración de estilos y otras ideas en la web. Se presentan a pequeña escala con imágenes, GIF animados y vídeos en formato de tablón. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) le permite hacer crecer su negocio y llegar a los 400 millones de personas con [!DNL Pinterest].

Con [!DNL Pinterest Ads], puede llegar a los usuarios a través de anuncios segmentados para descubrir y comprar sus productos. Los pines de [!DNL Pinterest Ads] se patrocinan para recibir una exposición adicional en los resultados de búsqueda relevantes. Los usuarios suscritos a [!DNL Pinterest Business] pueden elegir promocionar los anclajes con mejor rendimiento existentes, crear una nueva imagen o vídeo, o incluso promocionar una imagen anclada desde un sitio web. [!DNL Pinterest Ads] ofrece varios formatos de anuncios para ayudarle a alcanzar sus objetivos específicos de campaña.

## API de [!DNL Pinterest] {#pinterest-apis}

El origen de [!DNL Pinterest Ads] aprovecha las API de [!DNL Pinterest] para recuperar los datos de [!DNL Pinterest Ads], junto con todas las métricas y el rendimiento. Los extremos de API admitidos son:

* [Análisis de campaña](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Análisis de grupos de anuncios](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Análisis de anuncios](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilice el origen [!DNL Pinterest Ads] para llevar los datos de [!DNL Pinterest] a Experience Platform, donde podrá ejecutar el análisis de datos. Se devuelven datos a partir de la fecha de ingesta para un intervalo antedatado de 90 días. [!DNL Pinterest Ads] usa tokens de portador como mecanismo de autenticación para comunicarse con las API [!DNL Pinterest].

## Requisitos previos {#prerequisites}

El primer paso para crear una conexión de origen de [!DNL Pinterest Ads] es asegurarse de que tiene una cuenta de desarrollador de Pinterest. Si todavía no tiene una, visite la página [regístrese](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) para registrarse y crear su cuenta.

### Configurar la aplicación [!DNL Pinterest] y generar el token de acceso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Se recomienda usar las API [!DNL Pinterest] para generar el token de acceso, ya que la generación del token de acceso en la interfaz de usuario proporciona un acceso limitado. A través de la interfaz de usuario, solamente podrá obtener acceso a los ámbitos siguientes: `pins:read`, `boards:read` y `user_accounts:read`. Esta limitación no es adecuada para su uso con los extremos de análisis de la API [!DNL Pinterest].

Para generar tu token de acceso, lee las guías de [!DNL Pinterest] sobre [configuración de tu aplicación](https://developers.pinterest.com/docs/getting-started/set-up-app/) y [autenticación mediante OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Recopilar credenciales necesarias {#gather-required-credentials}

Para conectar [!DNL Pinterest Ads] a Experience Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| Token de acceso | El token de acceso [!DNL Pinterest Ads] de su cuenta de usuario. La cuenta de usuario del token debe ser el propietario de la cuenta de [!DNL Pinterest Ad] especificada o tener una de las funciones necesarias otorgadas a través del acceso empresarial: administrador, analista o administrador de campaña. Para obtener más información sobre el token de acceso, consulte la [[!DNL Pinterest] guía sobre cómo generar el token de acceso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID de cuenta de anuncio | El ID de cuenta de anuncio [!DNL Pinterest Ads] relacionado para su unidad comercial. Para obtener información sobre cómo recuperar el ID de cuenta de Ad. Visite la [[!DNL Pinterest] guía sobre cómo encontrar ID en el Administrador de anuncios](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campaña, grupo de anuncios o ID de anuncio | Los identificadores de `campaign`, `ad group` o `ad` que se corresponden con su ID de cuenta de publicidad. Para obtener los identificadores necesarios, vaya a la página [!DNL Pinterest] de **Pinterest Business Hub** > **Resumen de cuenta de publicidad** > **Campañas** / **Grupos de publicidad** / **Anuncios** y copie los identificadores necesarios que se mencionan justo debajo de cada uno de sus nombres. |

>[!NOTE]
>
>La API [!DNL Pinterest] proporciona API individuales para recuperar datos asociados con cada ID. Por lo tanto, solo debe pasar los ID correspondientes para el tipo de ID que le interesa.

## Mecanismos de protección {#guardrails}

Las secciones siguientes proporcionan información sobre los protecciones de datos de [!DNL Pinterest].

### [!DNL Pinterest] intervalo de fecha {#pinterest-date-range}

La API [!DNL Pinterest] admite un parámetro `start_date` y un parámetro `end_date` para recuperar datos de análisis entre un intervalo de fechas determinado.

* El `start_date` no puede ser anterior en más de 90 días a la fecha actual.
* `end_date` no puede ser posterior en más de 90 días a `start_date`.

Al programar el flujo de datos, debe configurar una de las siguientes opciones de frecuencia e intervalo:

| Frecuencia | Intervalo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Por ejemplo, si la ingesta se establece el 15 de marzo de 2023 con una configuración de frecuencia e intervalo configurada en `Day=1` o `Hour=24`, la API [!DNL Pinterest] solo recuperaría datos desde el 15 de diciembre de 2022, porque el cálculo tiene una fecha anterior de 90 días.

### [!DNL Pinterest] intervalo de tiempo {#pinterest-time-range}

La API [!DNL Pinterest] admite diferentes tipos de granularidad de tiempo para la recuperación de datos:

| Granularidad de tiempo | Descripción |
| --- | --- |
| **TOTAL** | Las métricas de datos se agregan en un intervalo de fechas especificado. |
| **DÍA** | Las métricas de datos se desglosan diariamente. |
| **HORA** | Las métricas de datos se desglosan por hora. |
| **SEMANALMENTE** | Las métricas de datos se desglosan semanalmente. |
| **MENSUALMENTE** | Las métricas de datos se desglosan mensualmente. |

Para Experience Platform, el origen [!DNL Pinterest Ads] está configurado internamente en `Day`, lo que significa que los datos se agregarán diariamente. Por ejemplo, si usa `impressions recorded` como métrica, dado que la granularidad está configurada como `DAY`, obtendrá `xx` impresiones en `day 1`, `yy` impresiones en `day 2`, etc.

>[!IMPORTANT]
>
>Pinterest impone a su API un límite de 1000 llamadas a la API diarias para leer información de anuncios, grupos de anuncios o campañas de publicidad. Para obtener información sobre los límites de tasa aplicables a las llamadas a API subyacentes, consulte la [[!DNL Pinterest] documentación sobre límites de tasa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Conectar [!DNL Pinterest Ads] a Experience Platform {#connect-to-platform}

La siguiente documentación proporciona información sobre cómo conectar [!DNL Pinterest Ads] a Experience Platform mediante API o la interfaz de usuario:

### Conectar [!DNL Pinterest Ads] a Experience Platform mediante API {#connect-to-platform-using-api}

* [Crear una conexión base de Pinterest mediante la API de Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Creación de un flujo de datos para una fuente de publicidad mediante la API de Flow Service](../../tutorials/api/collect/advertising.md)

### Conectar [!DNL Pinterest Ads] a Experience Platform mediante la interfaz de usuario {#connect-to-platform-using-ui}

* [Crear una conexión de origen de Pinterest en la interfaz de usuario](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Crear un flujo de datos para una conexión de origen de publicidad en la interfaz de usuario](../../tutorials/ui/dataflow/advertising.md)
