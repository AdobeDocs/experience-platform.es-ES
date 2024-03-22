---
title: Amazon Ads
description: Amazon Ads ofrece una serie de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, proveedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias. La integración de Amazon Ads con Adobe Experience Platform proporciona una integración llave en mano con los productos de Amazon Ads, incluido el Amazon DSP (ADSP). Con el destino de Amazon Ads en Adobe Experience Platform Amazon DSP, los usuarios pueden definir audiencias de anunciante para la segmentación y activación en la interfaz de usuario de.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 8e34e5488ab80cd1f3c8086bf7c16d3f22527540
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# (Beta) Conexión de Amazon Ads {#amazon-ads}

## Información general {#overview}

[!DNL Amazon Ads] ofrece una amplia gama de opciones para ayudarle a lograr sus objetivos publicitarios para vendedores registrados, proveedores, proveedores de libros, autores de Kindle Direct Publishing (KDP), desarrolladores de aplicaciones y/o agencias.

El [!DNL Amazon Ads] La integración de con Adobe Experience Platform proporciona una integración llave en mano de [!DNL Amazon Ads] productos de, incluidos el Amazon DSP (ADSP) y el Amazon Marketing Cloud (AMC).

Uso del [!DNL Amazon Ads] destino en Adobe Experience Platform, los usuarios pueden definir audiencias de anunciante para la segmentación y activación en la interfaz de usuario de AmazonDSP  Además, los usuarios pueden cargar sus datos en [!DNL Amazon Marketing Cloud] para comprender el rendimiento por audiencia, las dimensiones proporcionadas por el anunciante, la pertenencia a segmentos de Amazon u otras señales disponibles en AMC. Después de cargar las audiencias del anunciante en AMC, los usuarios pueden utilizar [!DNL Amazon Marketing Cloud] para modificar, mejorar o anexar a miembros de la audiencia utilizando señales de Amazon desde [!DNL Amazon Marketing Cloud].

AMC reúne señales únicas de todas las propiedades de Amazon y operadas, abarcando todos los medios, incluyendo pantalla, vídeo, streaming de TV, audio y anuncios patrocinados. Los usuarios pueden enviar fácilmente segmentos depurados de Adobe Experience Platform a AMC para mejorar el aprendizaje, como grupos de mercado de audiencias, cohortes de estilo de vida y patrones de participación de la marca. Los segmentos aumentados se pueden utilizar para optimizar las activaciones de medios en Amazon DSP.

>[!IMPORTANT]
>
>Este conector de destino y la página de documentación los crea y mantiene el *[!DNL Amazon Ads]* equipo. Actualmente, este es un producto beta y la funcionalidad está sujeta a cambios. Para cualquier consulta o solicitud de actualización, póngase en contacto directamente con ellos en *`amc-support@amazon.com`.*

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el *[!DNL Amazon Ads]* Destino. Estos son ejemplos de casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Activación y direccionamiento {#activation-and-targeting}

Esta integración con Amazon DSP permite lo siguiente [!DNL Amazon Ads] que pasen audiencias de CDP del anunciante de Adobe Experience Platform al servicio de publicidad de Amazon DSP para crear audiencias de anunciante para la segmentación de publicidad. Las audiencias pueden seleccionarse dentro de la Amazon DSP para la segmentación positiva, así como para la segmentación negativa (supresión).

### Analytics y medición {#analytics-and-measurement}

Esta integración con [!DNL Amazon Marketing Cloud] (AMC) permite [!DNL Amazon Ads] que pasen segmentos CDP del formulario de Adobe Experience Platform a AMC. Los anunciantes pueden unirse a las entradas de CDP con [!DNL Amazon Ads] envía señales y realiza análisis personalizados sobre temas como el impacto de los medios, los segmentos de audiencia y los recorridos del cliente en un formato compatible con la privacidad. Por ejemplo: un anunciante puede cargar una lista de sus clientes existentes para comprender el rendimiento agregado de la campaña de publicidad, o estadísticas agregadas de eventos de conversión sin conexión a Amazon, como ver una página de detalles del producto, agregar un producto a un carro de compras o comprar un producto.

### Optimización de publicidad

Esta integración con [!DNL Amazon Marketing Cloud] (AMC) permite a los anunciantes cargar sus propias listas de clientes y utilizar [!DNL Amazon Marketing Cloud] Ejecute SQL, realice análisis de superposición, supresiones, adiciones u optimizaciones a las audiencias de forma recurrente antes de crear una audiencia lista para la activación en Amazon DSP para la segmentación de audiencias

## Requisitos previos {#prerequisites}

Para usar la variable [!DNL Amazon Ads] con Adobe Experience Platform, los usuarios deben tener acceso primero a una cuenta del anunciante de Amazon DSP o a un [!DNL Amazon Marketing Cloud] ejemplo. Para aprovisionar estas instancias, visite la siguiente página en la [!DNL Amazon Ads] sitio web:

* [Introducción a Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Introducción al Marketing Cloud de Amazon](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identidades admitidas {#supported-identities}

El *[!DNL Amazon Ads]* La conexión de admite la activación de las identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service//features/namespaces.md). Para obtener más información sobre las identidades admitidas por [!DNL Amazon Ads], visite la [Centro de soporte de Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identidad de destino | Descripción | Consideraciones |
|---|---|---|
| phone_sha256 | Números de teléfono con hash con el algoritmo SHA256 | Los números de teléfono con hash SHA256 y texto sin formato son compatibles con Adobe Experience Platform. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |
| email_lc_sha256 | Direcciones de correo electrónico con el algoritmo SHA256 | Adobe Experience Platform admite direcciones de correo electrónico con hash SHA256 y de texto sin formato. Si el campo de origen contiene atributos sin hash, marque la **[!UICONTROL Aplicar transformación]** opción, para tener [!DNL Platform] hash automático de los datos en la activación. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en *[!DNL Amazon Ads]* destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

Se le redirige a la [!DNL Amazon Ads] interfaz de conexión en la que selecciona por primera vez las cuentas de anunciante a las que desea conectarse. Tras la conexión, se le redirigirá de nuevo a Adobe Experience Platform con una nueva conexión, siempre que tenga el ID de la cuenta del anunciante que haya seleccionado. Seleccione la cuenta del anunciante adecuada en la pantalla de configuración de destino para continuar.

* **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Conexión de Amazon Ads]**: seleccione el ID para el destino [!DNL Amazon Ads] cuenta utilizada para el destino.

>[!NOTE]
>
>Después de guardar la configuración de destino, no podrá cambiar el [!DNL Amazon Ads] ID del anunciante, incluso si vuelve a autenticarse con su cuenta de Amazon. Para usar un diferente [!DNL Amazon Ads] ID del anunciante, debe crear una nueva conexión de destino.

* **[!UICONTROL Región del anunciante]**: seleccione la región adecuada en la que está alojado el anunciante. Para obtener más información sobre los mercados admitidos en cada región, visite la [Documentación de Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configurar nuevo destino](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Leer [Activación de perfiles y audiencias en destinos de exportación de audiencia de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Asignar atributos e identidades {#map}

El [!DNL Amazon Ads] La conexión de admite direcciones de correo electrónico con hash y números de teléfono con hash para fines de coincidencia de identidad. La captura de pantalla siguiente proporciona una coincidencia de ejemplo compatible con el [!DNL Amazon Ads] conexión:

![Asignación de Adobe a Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Para asignar direcciones de correo electrónico con hash, seleccione la `Email_LC_SHA256` área de nombres de identidad como campo de origen.
* Para asignar números de teléfono con hash, seleccione la `Phone_SHA256` área de nombres de identidad como campo de origen.
* Para asignar direcciones de correo electrónico o números de teléfono sin hash, seleccione las áreas de nombres de identidad correspondientes como campos de origen y marque `Apply Transformation` Opción para que Platform hash las identidades en la activación.

Solo se selecciona un campo de destino determinado una vez en una configuración de destino de [!DNL Amazon Ads] conector.  Por ejemplo, si envía un correo electrónico empresarial, no puede asignar también un correo electrónico personal en la misma configuración de destino.

Se recomienda encarecidamente que asigne tantos campos como tenga disponibles. Si solo hay un atributo de origen disponible, puede asignar un único campo. El [!DNL Amazon Ads] destination utiliza todos los campos asignados con fines de asignación, lo que produce tasas de coincidencia más altas si se proporcionan más campos. Para obtener más información sobre los identificadores aceptados, visite la [Página de ayuda de audiencia con hash de Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Datos exportados / Validar exportación de datos {#exported-data}

Una vez que la audiencia se ha cargado, puede validar que se ha creado y cargado correctamente siguiendo los pasos siguientes:

**Para AmazonDSP**

Navegue hasta su **[!UICONTROL ID del anunciante]** > **[!UICONTROL Audiencias]** > **[!UICONTROL Audiencias del anunciante]**. Si la audiencia se ha creado correctamente y cumple la cantidad mínima de miembros, verá un estado de `Active`. Encontrará más detalles sobre el tamaño y el alcance de su audiencia en el panel Alcance previsto a la derecha de la interfaz de usuario de Amazon DSP.

![Validación de creación de audiencia de Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Para[!DNL Amazon Marketing Cloud]**

En el explorador de esquemas de la izquierda, busque la audiencia en **[!UICONTROL Anunciante cargado]** > **[!UICONTROL aep_audiences]**. A continuación, puede consultar la audiencia en el editor AMC SQL con la siguiente cláusula:

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Validación de creación de audiencia del Marketing Cloud Amazon](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener documentación de ayuda adicional, visite lo siguiente [!DNL Amazon Ads] recursos de ayuda:

* [Centro de ayuda de Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Marzo de 2024 | Actualización de funcionalidad y documentación | Se ha añadido la opción de exportar audiencias para usarlas en [!DNL Amazon Marketing Cloud] (AMC). |
| Mayo de 2023 | Actualización de funcionalidad y documentación | <ul><li>Se ha agregado compatibilidad para la selección de Región del anunciante en [flujo de trabajo de conexión de destino](#destination-details).</li><li>Se ha actualizado la documentación para reflejar la adición de la selección Región del anunciante. Para obtener más información sobre la selección de la región del anunciante correcta, consulte la [Documentación de Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Marzo de 2023 | Versión inicial | Versión de destino inicial y documentación publicada. |

{style="table-layout:auto"}

+++
