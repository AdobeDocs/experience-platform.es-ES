---
title: Amazon Ads
description: Amazon Ads ofrece una serie de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, proveedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias. La integración de Amazon Ads con Adobe Experience Platform proporciona una integración llave en mano con los productos de Amazon Ads, incluido el Amazon DSP (ADSP). Con el destino de Amazon Ads en Adobe Experience Platform Amazon DSP, los usuarios pueden definir audiencias de anunciante para la segmentación y activación en la interfaz de usuario de.
last-substantial-update: 2024-09-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 2%

---

# (Beta) Conexión de Amazon Ads {#amazon-ads}

## Información general {#overview}

[!DNL Amazon Ads] ofrece una serie de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, proveedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias.

La integración de [!DNL Amazon Ads] con Adobe Experience Platform proporciona una integración llave en mano con [!DNL Amazon Ads] productos, incluidos el Amazon DSP (ADSP) y el Amazon Marketing Cloud (AMC).

Si usan el destino [!DNL Amazon Ads] en Adobe Experience Platform, los usuarios podrán definir audiencias de anunciante para el direccionamiento y la activación en la interfaz de usuario de AmazonDSP  Además, los usuarios pueden cargar sus datos en [!DNL Amazon Marketing Cloud] para comprender el rendimiento por audiencia, las dimensiones proporcionadas por el anunciante, la pertenencia a segmentos de Amazon u otras señales disponibles en AMC. Después de cargar audiencias de anunciante en AMC, los usuarios pueden usar [!DNL Amazon Marketing Cloud] para modificar, mejorar o anexar a los miembros de la audiencia señales de Amazon desde [!DNL Amazon Marketing Cloud].

AMC reúne señales únicas de todas las propiedades de Amazon y operadas, abarcando todos los medios, incluyendo pantalla, vídeo, streaming de TV, audio y anuncios patrocinados. Los usuarios pueden enviar fácilmente segmentos depurados de Adobe Experience Platform a AMC para mejorar el aprendizaje, como grupos de mercado de audiencias, cohortes de estilo de vida y patrones de participación de la marca. Los segmentos aumentados se pueden utilizar para optimizar las activaciones de medios en Amazon DSP.

>[!IMPORTANT]
>
>El equipo *[!DNL Amazon Ads]* crea y mantiene este conector de destino y esta página de documentación. Actualmente, este es un producto beta y la funcionalidad está sujeta a cambios. Para cualquier consulta o solicitud de actualización, comuníquese directamente con ellos en *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino *[!DNL Amazon Ads]*, aquí hay casos de uso de ejemplo que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Activación y direccionamiento {#activation-and-targeting}

Esta integración con Amazon DSP permite a los anunciantes de [!DNL Amazon Ads] pasar audiencias de CDP del anunciante de Adobe Experience Platform a Amazon DSP, con el fin de crear audiencias de anunciante para la segmentación de anuncios. Las audiencias pueden seleccionarse dentro de la Amazon DSP para la segmentación positiva, así como para la segmentación negativa (supresión).

### Analytics y medición {#analytics-and-measurement}

Esta integración con [!DNL Amazon Marketing Cloud] (AMC) permite que los anunciantes de [!DNL Amazon Ads] pasen segmentos CDP del formulario de Adobe Experience Platform a AMC. Los anunciantes pueden unirse a las entradas de CDP con señales de [!DNL Amazon Ads] y realizar análisis personalizados sobre temas como el impacto de los medios, los segmentos de audiencia y los recorridos de los clientes en un formato compatible con la privacidad. Por ejemplo: un anunciante puede cargar una lista de sus clientes existentes para comprender el rendimiento agregado de la campaña de publicidad, o estadísticas agregadas de eventos de conversión sin conexión a Amazon, como ver una página de detalles del producto, agregar un producto a un carro de compras o comprar un producto.

### Optimización de Advertising

Esta integración con [!DNL Amazon Marketing Cloud] (AMC) permite a los anunciantes cargar sus propias listas de clientes y, mediante [!DNL Amazon Marketing Cloud] SQL, realizar análisis de superposición, supresiones, adiciones u optimizaciones a las audiencias de forma recurrente antes de crear una audiencia lista para la activación en Amazon DSP para la segmentación.

## Requisitos previos {#prerequisites}

Para usar la conexión [!DNL Amazon Ads] con Adobe Experience Platform, los usuarios deben tener acceso primero a una cuenta de anunciante de Amazon DSP o a una instancia de [!DNL Amazon Marketing Cloud]. Para aprovisionar estas instancias, visite la siguiente página en el sitio web [!DNL Amazon Ads]:

* [Introducción a AmazonDSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Introducción al Marketing Cloud de Amazon](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identidades admitidas {#supported-identities}

La conexión *[!DNL Amazon Ads]* admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service//features/namespaces.md). Para obtener más información sobre las identidades admitidas por [!DNL Amazon Ads], visite el [Centro de soporte técnico de AmazonDSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] aplique automáticamente el hash a los datos durante la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] aplique automáticamente el hash a los datos durante la activación. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino *[!DNL Amazon Ads]*. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

Se le redirigirá a la interfaz de conexión de [!DNL Amazon Ads], donde seleccionará por primera vez las cuentas de anunciante a las que desea conectarse. Tras la conexión, se le redirigirá de nuevo a Adobe Experience Platform con una nueva conexión, siempre que tenga el ID de la cuenta del anunciante que haya seleccionado. Seleccione la cuenta del anunciante adecuada en la pantalla de configuración de destino para continuar.

* **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Conexión de Amazon Ads]**: seleccione el identificador de la cuenta de destino [!DNL Amazon Ads] usada para el destino.

>[!NOTE]
>
>Después de guardar la configuración de destino, no podrá cambiar el identificador del anunciante [!DNL Amazon Ads] aunque vuelva a autenticarse con su cuenta de Amazon. Para usar un identificador de anunciante [!DNL Amazon Ads] diferente, debe crear una nueva conexión de destino. Los anunciantes que ya estén configurados en una integración con ADSP para deben crear un nuevo flujo de destino si desean que sus audiencias se envíen a AMC o a una cuenta ADSP diferente.

* **[!UICONTROL Región del anunciante]**: selecciona la región apropiada en la que está alojado tu anunciante. Para obtener más información sobre los mercados admitidos en cada región, visite la [documentación de Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configurar nuevo destino](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y audiencias en destinos de exportación de audiencias de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

La conexión [!DNL Amazon Ads] admite direcciones de correo electrónico con hash y números de teléfono con hash para fines de coincidencia de identidad. La captura de pantalla siguiente proporciona un ejemplo de coincidencia compatible con la conexión [!DNL Amazon Ads]:

![Asignación de Adobe a Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para asignar direcciones de correo electrónico con hash, seleccione el área de nombres de identidad `Email_LC_SHA256` como campo de origen.
* Para asignar números de teléfono con hash, seleccione el área de nombres de identidad `Phone_SHA256` como campo de origen.
* Para asignar direcciones de correo electrónico o números de teléfono sin hash, seleccione las áreas de nombres de identidad correspondientes como campos de origen y marque la opción `Apply Transformation` para que Platform hash las identidades en la activación.
* *NUEVO a partir de la versión de septiembre de 2024*: Amazon Ads requiere que asigne un campo que contenga un valor `countryCode` en el formato ISO de 2 caracteres para facilitar el proceso de resolución de identidades (por ejemplo: EE. UU., GB, MX, CA, etc.). Las conexiones sin asignaciones de `countryCode` tendrán un impacto negativo en las tasas de coincidencia de identidad.

Solo se selecciona un campo de destino determinado una vez en una configuración de destino del conector [!DNL Amazon Ads].  Por ejemplo, si envía un correo electrónico empresarial, no puede asignar también un correo electrónico personal en la misma configuración de destino.

Se recomienda encarecidamente que asigne tantos campos como tenga disponibles. Si solo hay un atributo de origen disponible, puede asignar un único campo. El destino [!DNL Amazon Ads] utiliza todos los campos asignados con fines de asignación, lo que da como resultado tasas de coincidencia más altas si se proporcionan más campos. Para obtener más información sobre los identificadores aceptados, visite la [página de ayuda de audiencia con hash para Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez que la audiencia se ha cargado, puede validar que se ha creado y cargado correctamente siguiendo los pasos siguientes:

**Para AmazonDSP**

Vaya a **[!UICONTROL ID del anunciante]** > **[!UICONTROL Audiencias]** > **[!UICONTROL Audiencias del anunciante]**. Si la audiencia se creó correctamente y cumple la cantidad mínima de miembros, verá un estado de `Active`. Encontrará más detalles sobre el tamaño y el alcance de su audiencia en el panel Alcance previsto a la derecha de la interfaz de usuario de Amazon DSP.

![Validación de creación de audiencia de AmazonDSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Para[!DNL Amazon Marketing Cloud]**

En el explorador de esquemas de la izquierda, busque su audiencia en **[!UICONTROL Anunciante cargado]** > **[!UICONTROL aep_audiences]**. A continuación, puede consultar la audiencia en el editor AMC SQL con la siguiente cláusula:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![Validación de creación de audiencia de Marketing Cloud de Amazon](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener documentación de ayuda adicional, visite los siguientes [!DNL Amazon Ads] recursos de ayuda:

* [Centro de ayuda de Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Mayo de 2024 | Actualización de funcionalidad y documentación | Se agregó la opción de asignación para exportar el parámetro `countryCode` en Amazon Ads. Use `countryCode` en el [paso de asignación](#map) para mejorar las tasas de coincidencia de identidad con Amazon. |
| Marzo de 2024 | Actualización de funcionalidad y documentación | Se agregó la opción de exportar audiencias para usarlas en [!DNL Amazon Marketing Cloud] (AMC). |
| Mayo de 2023 | Actualización de funcionalidad y documentación | <ul><li>Se agregó compatibilidad con la selección Región del anunciante en [flujo de trabajo de conexión de destino](#destination-details).</li><li>Se ha actualizado la documentación para reflejar la adición de la selección Región del anunciante. Para obtener más información sobre cómo seleccionar la región del anunciante correcta, consulte la [documentación de Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Marzo de 2023 | Versión inicial | Versión de destino inicial y documentación publicada. |

{style="table-layout:auto"}

+++
