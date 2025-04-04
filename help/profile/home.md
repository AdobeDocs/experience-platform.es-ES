---
title: Resumen del perfil del cliente en tiempo real
description: El perfil del cliente en tiempo real combina datos de varias fuentes y proporciona acceso a esos datos en forma de perfiles de clientes individuales y eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 1%

---

# Información general de [!DNL Real-Time Customer Profile]

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de sus clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes. Esta introducción le ayudará a comprender el rol y el uso de [!DNL Real-Time Customer Profile] en [!DNL Experience Platform].

## [!DNL Profile] en Experience Platform

La relación entre el perfil del cliente en tiempo real y otros servicios de Experience Platform aparece resaltada en el siguiente diagrama:

![La relación entre el perfil del cliente en tiempo real y otros servicios en Adobe Experience Platform. Este diagrama muestra que el perfil es uno de los componentes principales de Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Explicación de perfiles

[!DNL Real-Time Customer Profile] combina datos de varios sistemas empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de clientes con eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales. En las secciones siguientes se destacan algunos de los conceptos principales que debe comprender para generar y mantener perfiles dentro de Experience Platform de forma eficaz.

### Composición de entidades de perfil

Un perfil del cliente en tiempo real está compuesto por una entidad principal llamada **entidad principal** y varias entidades auxiliares. En el contexto de Experience Platform, la entidad principal suele ser una **entidad de perfil**, que se compone de características, comportamientos y pertenencias a audiencias de una persona individual. Otras entidades permiten que el motor de segmentación utilice datos fuera de la entidad principal del perfil e incluyen lo siguiente:

- **Entidad dimensional**: La entidad que se usa para simplificar el proceso de modelado de datos para la información compartida entre eventos o registros de perfil. Esto también se conoce como entidad de búsqueda o entidad de clasificación.
- **Entidad B2B**: Entidades que describen la relación del perfil con oportunidades y cuentas de empresa a empresa.

![Diagrama que explica la composición de la entidad de perfil.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Dado que las entidades dimensionales y B2B solo existen fuera de la entidad principal, solo se utilizan para la segmentación por lotes.

Las entidades dimensionales y B2B están vinculadas a la entidad principal mediante **relaciones de esquema**. Consulte la siguiente documentación para obtener más información:

- [Crear una relación de esquema uno a uno para entidades de búsqueda](../xdm/tutorials/relationship-ui.md)
- [Crear una relación de esquema varios a uno para entidades B2B](../xdm/tutorials/relationship-b2b.md)

### Almacén de datos de perfil

Aunque [!DNL Real-Time Customer Profile] procesa los datos ingeridos y usa Adobe Experience Platform [!DNL Identity Service] para combinar datos relacionados mediante la asignación de identidad, mantiene sus propios datos en el almacén de datos [!DNL Profile]. El almacén [!DNL Profile] es independiente de los datos del catálogo en el lago de datos y de los datos [!DNL Identity Service] en el gráfico de identidad.

El almacén de perfiles utiliza una infraestructura de Microsoft Azure Cosmos DB y el lago de datos de Experience Platform utiliza el almacenamiento de Microsoft Azure Data Lake.

### Protecciones de perfil

Experience Platform proporciona una serie de protecciones que le ayudarán a evitar la creación de [esquemas XDM (Experience Data Model)](../xdm/home.md) que el perfil del cliente en tiempo real no admite. Esto incluye límites leves que resultarán en una degradación del rendimiento, así como límites duros que resultarán en errores y roturas del sistema. Para obtener más información, incluida una lista de directrices y ejemplos de casos de uso, lea la documentación de [protecciones de perfil](guardrails.md).

### Tablero de perfil {#profile-dashboard}

La interfaz de usuario de Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los datos del perfil del cliente en tiempo real, tal como se capturan durante una instantánea diaria. Para obtener información sobre cómo acceder al panel [!DNL Profile] y trabajar con él en la interfaz de usuario, así como información detallada sobre las métricas mostradas en el panel, consulte la [Guía de la interfaz de usuario del panel de perfil](ui/profile-dashboard.md).

### Fragmentos de perfil frente a perfiles combinados {#profile-fragments-vs-merged-profiles}

Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Experience Platform, se combinan para crear un único perfil para ese cliente.

En otras palabras, los fragmentos de perfil representan una identidad principal única y los datos correspondientes de [registro](#record-data) o [evento](#time-series-events) para ese ID dentro de un conjunto de datos determinado.

Cuando los datos de varios conjuntos de datos entran en conflicto (por ejemplo, cuando un fragmento enumera al cliente como &quot;único&quot; mientras que el otro indica al cliente como &quot;casado&quot;), la [política de combinación](#merge-policies) determina qué información se debe priorizar e incluir en el perfil para el individuo. Por lo tanto, es probable que el número total de fragmentos de perfil dentro de Experience Platform siempre sea mayor que el número total de perfiles combinados, ya que cada perfil suele estar compuesto por varios fragmentos de varios conjuntos de datos.

### Registrar datos {#record-data}

Un perfil es una representación de un sujeto, una organización o un individuo, compuesta por muchos atributos (también conocidos como datos de registro). Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellidos y dirección de correo electrónico. Con [!DNL Experience Platform], puede personalizar perfiles para que utilicen datos específicos relevantes para su negocio. La clase estándar [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], es la clase preferida sobre la que generar un esquema al describir datos de registros de clientes y proporciona los datos integrales a muchas interacciones entre servicios de Experience Platform. Para obtener más información sobre cómo trabajar con esquemas en [!DNL Experience Platform], comience por leer la [descripción general del sistema XDM](../xdm/home.md).

### Eventos de series temporales {#time-series-events}

Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto realizó una acción, directa o indirectamente, así como datos que detallan el propio evento. Representados por la clase de esquema estándar XDM ExperienceEvent, los datos de series temporales pueden describir eventos como elementos que se añaden a un carro de compras, vínculos en los que se hace clic y vídeos visualizados. Los datos de series temporales se pueden utilizar para basar las reglas de segmentación en y se puede acceder a los eventos de forma individual en el contexto de un perfil.

### Identidades

Cada empresa quiere comunicarse con sus clientes de una manera que se sienta personal. Sin embargo, uno de los desafíos de ofrecer experiencias digitales relevantes a los clientes es comprender cómo unir sus datos desconectados, que a menudo se propaga a través de diferentes canales digitales, como tabletas, teléfonos móviles y portátiles. [!DNL Identity Service] le permite recopilar una imagen completa de su cliente vinculando identidades de varios canales y creando un gráfico de identidades para cada cliente. Visite [Introducción al servicio de identidad](../identity-service/home.md) para obtener más información.

### Combinar políticas

Al unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales, las políticas de combinación son las reglas que [!DNL Experience Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se utilizarán para crear el perfil del cliente.

Cuando hay datos en conflicto de varios conjuntos de datos, la política de combinación determina cómo se deben tratar esos datos y qué valor se debe utilizar. A través de las API de RESTful o de la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una política de combinación predeterminada para su organización.

Para obtener más información acerca de las políticas de combinación y su función en Experience Platform, lea la [descripción general de las políticas de combinación](merge-policies/overview.md).

### Esquemas de unión {#profile-fragments-and-union-schemas}

Una de las características principales de [!DNL Real-Time Customer Profile] es la capacidad de unificar los datos multicanal. Cuando se usa [!DNL Real-Time Customer Profile] para acceder a una entidad, puede proporcionarle una vista combinada de todos los fragmentos de perfil de esa entidad en todos los conjuntos de datos, denominada como la &quot;vista de unión&quot; y que es posible gracias a lo que se conoce como esquema de unión.

Para obtener más información sobre los esquemas de unión, incluido cómo acceder a los esquemas de unión en la interfaz de usuario, visite la [guía de la interfaz de usuario del esquema de unión](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Perfiles y públicos

Adobe Experience Platform [!DNL Segmentation Service] produce las audiencias necesarias para potenciar las experiencias de sus clientes individuales. Cuando se crea una audiencia, su ID se añade a la lista de suscripciones a audiencias de todos los perfiles aptos. Las reglas de segmentos se crean y aplican a los datos de [!DNL Real-Time Customer Profile] mediante las API de RESTful y la interfaz de usuario del Generador de segmentos. Para obtener más información acerca de la segmentación, comience por leer la [descripción general del servicio de segmentación](../segmentation/home.md).

### Ingesta de streaming y segmentación de streaming

La entrada en tiempo real es posible mediante un proceso denominado ingesta de transmisión. A medida que se incorporan los datos del perfil y la serie temporal, [!DNL Real-Time Customer Profile] decide automáticamente incluir o excluir esos datos de las audiencias a través de un proceso continuo denominado segmentación de flujo continuo, antes de combinarlos con los datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos y tomar decisiones de forma instantánea para ofrecer experiencias mejoradas e individualizadas a los clientes mientras interactúan con su marca. Durante la ingesta, los datos también se someten a validación para garantizar que se ingieran correctamente y que se ajusten al esquema en el que se basa el conjunto de datos. Para obtener más información acerca de la validación que se realiza durante la ingesta, comience por leer la [descripción general de la calidad de la ingesta de datos](../ingestion/quality/overview.md).

## Ingesta de datos en [!DNL Profile]

[!DNL Experience Platform] se puede configurar para enviar datos de registros y series temporales a [!DNL Profile], lo cual admite la ingesta de transmisión en tiempo real y la ingesta por lotes. Para obtener más información, consulte el tutorial que describe cómo [agregar datos al Perfil del cliente en tiempo real](tutorials/add-profile-data.md).

>[!NOTE]
>
>Los datos recopilados a través de las soluciones de Adobe, incluyendo [!DNL Analytics Cloud], [!DNL Marketing Cloud] y [!DNL Advertising Cloud], fluyen a [!DNL Experience Platform] y se incorporan en [!DNL Profile].

### Métricas de ingesta de perfil

Observability Insights le permite exponer métricas clave en Adobe Experience Platform. Además de [!DNL Experience Platform] estadísticas de uso e indicadores de rendimiento para varias funcionalidades de [!DNL Experience Platform], hay métricas específicas relacionadas con el perfil que le permiten obtener insight en las tasas de solicitudes entrantes, las tasas de ingesta exitosas, los tamaños de registros ingeridos y más. Para obtener más información, comience por leer la [descripción general de la API de Observability Insights](../observability/api/overview.md) y, para obtener una lista completa de las métricas del perfil del cliente en tiempo real, consulte la documentación sobre [métricas disponibles](../observability/api/metrics.md#available-metrics).

## Actualizar datos del almacén de perfiles

En ocasiones puede ser necesario actualizar los datos en el almacén de perfiles de su organización. Por ejemplo, es posible que tenga que corregir registros o cambiar un valor de atributo. Esto se puede hacer mediante la ingesta por lotes y requiere un conjunto de datos habilitado para el perfil y configurado con una etiqueta de actualización. Para obtener más información sobre cómo configurar un conjunto de datos para actualizaciones de atributos, consulte el tutorial de [habilitar un conjunto de datos para Perfil y actualizar](../catalog/datasets/enable-upsert.md).

## Administración de datos y [!DNL Privacy]

Administración de datos es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos.

En lo que se refiere al acceso a los datos, el control de datos desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles:

- Etiquetado de uso de datos
- Políticas de acceso a datos
- Control de acceso a los datos para acciones de marketing

La gobernanza de datos se administra en varios puntos. Estos incluyen decidir qué datos se incorporan a [!DNL Experience Platform] y a qué datos se puede acceder después de la ingesta para una acción de marketing determinada. Para obtener más información, comience por leer la [descripción general del control de datos](../data-governance/home.md).

### Gestión de solicitudes de exclusión y privacidad de datos

[!DNL Experience Platform] permite que sus clientes envíen solicitudes de exclusión relacionadas con el uso y almacenamiento de sus datos en [!DNL Real-Time Customer Profile]. Para obtener más información sobre cómo se administran las solicitudes de exclusión, consulte la documentación sobre [cumplimiento de las solicitudes de exclusión](../segmentation/tutorials/consents.md).

## Pasos siguientes y recursos adicionales

Para obtener más información sobre cómo trabajar con los datos del perfil del cliente en tiempo real usando la interfaz de usuario de Experience Platform o la API de perfil, comience por leer la [guía de la interfaz de usuario del perfil](ui/user-guide.md) o la [guía para desarrolladores de API](api/overview.md), respectivamente.
