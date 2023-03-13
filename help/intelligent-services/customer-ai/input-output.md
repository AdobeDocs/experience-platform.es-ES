---
keywords: Experience Platform;introducción;inteligencia artificial aplicada al cliente;temas populares;entrada de inteligencia artificial aplicada al cliente;salida de inteligencia artificial aplicada al cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Entrada y salida en Customer AI
description: Obtenga más información acerca de los eventos, las entradas y los resultados necesarios que utiliza la inteligencia artificial aplicada al cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 2%

---

# Entrada y salida en Customer AI

En el siguiente documento se describen los diferentes eventos, entradas y resultados necesarios que se utilizan en la inteligencia artificial aplicada al cliente.

## Primeros pasos

La inteligencia artificial aplicada al cliente funciona analizando uno de los siguientes conjuntos de datos para predecir puntuaciones de pérdida o tendencia a la conversión:

- Los datos de Adobe Analytics que utilizan [Conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Los datos de Adobe Audience Manager que utilizan [Conector de origen del Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- Conjunto de datos de evento de experiencia (EE)
- Conjunto de datos de Evento de experiencia del consumidor (CEE)

Puede agregar varios conjuntos de datos de diferentes fuentes si cada uno de los conjuntos de datos comparte el mismo tipo de identidad (área de nombres), como un ECID. Para obtener más información sobre cómo agregar varios conjuntos de datos, visite la [Guía del usuario de Customer AI](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>Los conectores de origen tardan hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe verificar que el conjunto de datos tenga la longitud mínima de datos necesaria para la inteligencia artificial aplicada al cliente. Consulte la [datos históricos](#data-requirements) para verificar que tiene datos suficientes para el objetivo de predicción.

Este documento requiere una comprensión básica del esquema CEE. Consulte la [Preparación de datos de servicios inteligentes](../data-preparation.md) documentación antes de continuar.

En la tabla siguiente se describen algunos términos comunes utilizados en este documento:

| Término | Definición |
| --- | --- |
| [Modelo de datos de experiencia (XDM)](../../xdm/home.md) | XDM es el marco de trabajo básico que permite a Adobe Experience Cloud, con tecnología Adobe Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. La metodología en la que se crea el Experience Platform, el sistema XDM, pone en funcionamiento los esquemas del modelo de datos de experiencia para que los utilicen los servicios de Platform. |
| Esquema XDM | Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. Antes de poder introducir datos en Platform, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase XDM base y cero o más grupos de campos de esquema. |
| clase XDM | Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el número más pequeño de propiedades que debe contener un esquema para representar un comportamiento de datos determinado. |
| [Grupos de campo](../../xdm/schema/composition.md) | Componente que define uno o varios campos de un esquema. Los grupos de campos aplican la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en todos los esquemas en los que se incluyen. Los grupos de campos solo son compatibles con clases específicas, identificadas por sus `meta:intendedToExtend` atributo. |
| [Tipo de datos](../../xdm/schema/composition.md) | Componente que también puede proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes. Los tipos de datos descritos en este documento son compatibles con los esquemas CEE y Adobe Analytics. |
| Pérdida | Una medición del porcentaje de cuentas que cancelan o deciden no renovar sus suscripciones. Una tasa de pérdida alta puede afectar negativamente a los ingresos mensuales recurrentes (MRR) y también puede indicar insatisfacción con un producto o servicio. |
| [Perfil del cliente en tiempo real](../../profile/home.md) | El Perfil del cliente en tiempo real proporciona un perfil de consumidor centralizado para la administración de experiencias personalizada y dirigida. Cada perfil contiene datos agregados de todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que implican a la persona que ha tenido lugar en cualquiera de los sistemas que utiliza con Experience Platform. |

## Datos de entrada de Customer AI

>[!TIP]
>
> La inteligencia artificial aplicada al cliente determina automáticamente qué eventos son útiles para las predicciones y genera una advertencia si los datos disponibles no son suficientes para generar predicciones de calidad.

La inteligencia artificial aplicada al cliente es compatible con los conjuntos de datos de Adobe Analytics, Adobe Audience Manager, Evento de experiencia (EE) y Evento de experiencia del consumidor (CEE). El esquema CEE requiere que agregue grupos de campos durante el proceso de creación del esquema. Si utiliza conjuntos de datos de Adobe Analytics o Adobe Audience Manager, el conector de origen asigna directamente los eventos estándar (comercio, detalles de página web, aplicación y búsqueda) que se enumeran a continuación durante el proceso de conexión. Puede agregar varios conjuntos de datos de diferentes fuentes si cada uno de los conjuntos de datos comparte el mismo tipo de identidad (área de nombres), como un ECID.

Para obtener más información sobre la asignación de datos de Adobe Analytics o datos de Audience Manager, visite la [Asignaciones de campos de Analytics](../../sources/connectors/adobe-applications/analytics.md) o [Asignaciones de campos de Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md) guía.

### Eventos estándar utilizados por Customer AI {#standard-events}

Los eventos de experiencia XDM se utilizan para determinar varios comportamientos de cliente. Según la estructura de los datos, es posible que los tipos de evento enumerados a continuación no abarquen todos los comportamientos del cliente. Depende de usted determinar qué campos tienen los datos necesarios para identificar de forma clara e inequívoca la actividad de los usuarios web. Según el objetivo de predicción, los campos obligatorios que se necesitan pueden cambiar.

La inteligencia artificial aplicada al cliente se basa en diferentes tipos de eventos para crear funciones de modelo. Estos tipos de eventos se añaden automáticamente al esquema mediante varios grupos de campos XDM.

>[!NOTE]
>
>Si utiliza datos de Adobe Analytics o Adobe Audience Manager, el esquema se crea automáticamente con los eventos estándar necesarios para capturar los datos. Si está creando su propio esquema CEE personalizado para capturar datos, debe tener en cuenta qué grupos de campos son necesarios para capturar los datos.

No es necesario tener datos para cada uno de los eventos estándar enumerados a continuación, pero ciertos eventos son necesarios para ciertos escenarios. Si tiene disponibles algunos de los datos de eventos estándar, se recomienda incluirlos en el esquema. Por ejemplo, si desea crear una aplicación de inteligencia artificial aplicada al cliente para predecir eventos de compra, sería útil tener datos de la variable `Commerce` y `Web page details` tipos de datos.

Para ver un grupo de campos en la IU de Platform, seleccione **[!UICONTROL Esquemas]** en el carril izquierdo, seguido de la selección de la **[!UICONTROL Grupos de campos]** pestaña.

| Grupo de campos | Tipo de evento | Ruta de campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalles de comercio] | pedido | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | cierres | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | compras | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Detalles web] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Detalles de aplicación] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpupgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Detalles de búsqueda] | búsqueda | search.keywords |

Además, la inteligencia artificial aplicada al cliente puede utilizar los datos de suscripción para crear mejores modelos de pérdida. Se necesitan datos de suscripción para cada perfil que use [[!UICONTROL Suscripción]](../../xdm/data-types/subscription.md) formato de tipo de datos. La mayoría de los campos son opcionales, sin embargo, para un modelo de pérdida óptimo, se recomienda proporcionar datos para tantos campos como sea posible, como, `startDate`, `endDate`y cualquier otra información pertinente.

### Añadir eventos personalizados y atributos de perfil

Si tiene información que desea incluir además de la [campos de eventos estándar](#standard-events) Cuando la inteligencia artificial aplicada al cliente la utiliza, se proporciona un evento personalizado y una opción de atributo de perfil personalizada durante su [configuración de instancia](./user-guide/configure.md#custom-events).

Si el conjunto de datos seleccionado incluye eventos personalizados o atributos de perfil como una &quot;reserva de hotel&quot; o un &quot;empleado de X company&quot; definidos en el esquema, puede agregarlos a la instancia. La inteligencia artificial aplicada al cliente utiliza estos eventos personalizados y atributos de perfil adicionales para mejorar la calidad del modelo y proporcionar resultados más precisos.

### Datos históricos {#data-requirements}

La inteligencia artificial aplicada al cliente requiere datos históricos para la formación sobre modelos, pero la cantidad de datos necesarios se basa en dos elementos clave: la ventana de resultados y la población elegible.

De forma predeterminada, la inteligencia artificial aplicada al cliente busca un usuario que haya tenido actividad en los últimos 120 días si no se proporciona ninguna definición de población apta durante la configuración de la aplicación. Además, la inteligencia artificial aplicada al cliente requiere un mínimo de 500 eventos calificadores y 500 no calificadores (1000 en total) de datos históricos basados en una definición de objetivo predicha.

Los siguientes ejemplos proporcionan una fórmula sencilla para ayudarle a determinar la cantidad mínima de datos necesarios. Si tiene más del requisito mínimo, es probable que el modelo proporcione resultados más precisos. Si tiene menos de la cantidad mínima requerida, el modelo fallará porque no hay una cantidad de datos suficiente para la formación del modelo.

**Fórmula**:

Longitud mínima de datos requerida = población elegible + ventana de resultados

>[!NOTE]
>
> 30 es el número mínimo de días requeridos para la población elegible. Si no se proporciona, el valor predeterminado es de 120 días.

Ejemplos:

- Desea predecir si es probable que un cliente compre un reloj en los próximos 30 días. También desea puntuar a los usuarios que hayan realizado alguna actividad web en los últimos 60 días. En este caso, la longitud mínima de datos requerida = 60 días + 30 días. La población elegible es de 60 días y la ventana de resultado es de 30 días, con un total de 90 días.

- Desea predecir si es probable que el usuario compre un reloj en los próximos 7 días. En este caso, la longitud mínima de datos requerida = 120 días + 7 días. La población elegible toma como valor predeterminado 120 días y la ventana de resultado es de 7 días, con un total de 127 días.

- Desea predecir si es probable que el cliente compre un reloj en los próximos 7 días. También desea puntuar a los usuarios que hayan realizado alguna actividad web en los últimos 7 días. En este caso, la longitud mínima de datos requerida = 30 días + 7 días. La población elegible requiere un mínimo de 30 días y la ventana de resultados es de 7 días, con un total de 37 días.

Además de los datos mínimos requeridos, la inteligencia artificial aplicada al cliente también funciona mejor con datos recientes. En este caso de uso, la inteligencia artificial aplicada al cliente está haciendo una predicción para el futuro en función de los datos de comportamiento recientes de un usuario. En otras palabras, es probable que los datos más recientes arrojen una predicción más precisa.

### Casos de ejemplo

En esta sección, se describen diferentes escenarios para instancias de inteligencia artificial aplicada al cliente, así como los tipos de eventos requeridos y recomendados. Consulte la [tabla de eventos estándar](#standard-events) arriba para obtener más información sobre el grupo de campos y su ruta de campo.

>[!NOTE]
>
> Los tipos de evento requeridos se utilizan para identificar de forma clara e inequívoca la actividad del usuario web. El número de tipos de eventos requeridos cambiará según el objetivo de predicción y la estructura del esquema. Si no está seguro de que se necesita un tipo de evento determinado, se recomienda incluir ese tipo de evento al crear su esquema CEE. Si utiliza datos de Adobe Analytics o Adobe Audience Manager, los eventos estándar requeridos deben estar disponibles según los datos que esté transmitiendo.

### Escenario 1: conversión de compra en un sitio web de comercio electrónico minorista

**Objetivo de predicción:** Predecir la tendencia de conversión para que los perfiles aptos compren un determinado artículo de ropa en un sitio web.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- pedido
- cierres
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 2: conversión de suscripción en un sitio web de servicio de streaming de medios

**Objetivo de predicción:** Prediga la tendencia de conversión de la suscripción para que los perfiles aptos se comprometan a un determinado nivel de suscripción, como un plan estándar o premium.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- pedido
- cierres
- compras
- webVisit
- búsqueda

En este ejemplo, `order`, `checkouts`, y `purchases` se utilizan para indicar que se compró una suscripción y su tipo.

Además, para un modelo preciso, se recomienda utilizar algunas de las propiedades disponibles en la variable [tipo de datos de suscripción](../../xdm/data-types/subscription.md).

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 3: pérdida en un sitio web de venta minorista de comercio electrónico

**Objetivo de predicción:** Predecir la probabilidad de que no se produzca un evento de compra.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- pedido
- cierres
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 4: ampliar la conversión de ventas en un sitio web de comercio electrónico minorista

**Objetivo de predicción:** Predecir la tendencia a la compra de la población que ha comprado un producto específico para comprar un nuevo producto relacionado.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- pedido
- cierres
- compras
- webVisit
- búsqueda

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 5: cancelar la suscripción (pérdida) a un medio de comunicación en línea

**Objetivo de predicción:** Predecir la tendencia de la población elegible a cancelar la suscripción a un servicio el mes próximo.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- webVisit
- búsqueda

Además, para un modelo preciso, se recomienda utilizar algunas de las propiedades disponibles en la variable [tipo de datos de suscripción](../../xdm/data-types/subscription.md).

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 6: Iniciar la aplicación móvil

**Objetivo de predicción:** Prediga la tendencia de los perfiles elegibles a iniciar una aplicación móvil de pago en los próximos X días. Esto es similar a predecir el indicador de rendimiento clave (KPI) de &quot;Usuarios activos mensualmente&quot;.

**Tipos de eventos estándar requeridos:**

Los tipos de eventos que se enumeran a continuación son necesarios para una salida óptima de la inteligencia artificial aplicada al cliente con este objetivo de predicción concreto. Es posible excluir un evento requerido según el objetivo de predicción, sin embargo, excluir varios eventos puede llevar a resultados deficientes.

- pedido
- cierres
- compras
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpupgrades

En este ejemplo, `order`, `checkouts`, y `purchases` se utilizan cuando es necesario adquirir una aplicación móvil.

**Tipos de eventos estándar recomendados adicionales:**

Cualquiera de los restantes [tipos de eventos](#standard-events) puede ser necesario en función de la complejidad de su objetivo y de la población apta al configurar su instancia de inteligencia artificial aplicada al cliente. Se recomienda que, si los datos están disponibles para un tipo de datos concreto, estos datos se incluyan en el esquema.

### Escenario 7: características realizadas (Adobe Audience Manager)

**Objetivo de predicción:** Predecir la tendencia a realizar algunos rasgos.

**Tipos de eventos estándar requeridos:**

Para utilizar características de Adobe Audience Manager, debe crear una conexión de origen utilizando [Conector de origen del Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). El conector de origen crea automáticamente el esquema con los grupos de campos adecuados. No es necesario agregar manualmente tipos de eventos adicionales para que el esquema funcione con la inteligencia artificial aplicada al cliente.

Al configurar una nueva instancia de inteligencia artificial aplicada al cliente, `audienceName` y `audienceID` se puede usar para seleccionar un rasgo particular para la puntuación al definir el objetivo.

## Datos de salida de Customer AI

La inteligencia artificial aplicada al cliente genera varios atributos para perfiles individuales que se consideran aptos. Existen dos maneras de consumir la puntuación (salida) en función de lo que haya aprovisionado. Si tiene un conjunto de datos habilitado para el Perfil del cliente en tiempo real, puede consumir datos del Perfil del cliente en tiempo real en el [Generador de segmentos](../../segmentation/ui/segment-builder.md). Si no tiene un conjunto de datos con perfil habilitado, puede hacer lo siguiente [descargar la salida de Customer AI](./user-guide/download-scores.md) conjunto de datos disponible en el lago de datos.

Puede encontrar el conjunto de datos de salida en **Conjuntos de datos** en Platform. Todos los conjuntos de datos de salida de inteligencia artificial aplicada al cliente comienzan con el nombre **Puntuaciones de inteligencia artificial aplicada al cliente - Name_of_app**. Del mismo modo, todos los esquemas de salida de Customer AI comienzan con el nombre **Esquema de inteligencia artificial aplicada al cliente: Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> Los valores de salida los consume el perfil del cliente en tiempo real, que se puede utilizar para crear y definir segmentos.

La siguiente tabla describe los distintos atributos que se encuentran en la salida de la inteligencia artificial aplicada al cliente:

| Atributo | Descripción |
| ----- | ----------- |
| Puntuación | La probabilidad relativa de que un cliente alcance el objetivo predicho dentro del lapso de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino más bien como la probabilidad de un individuo en comparación con la población general. Esta puntuación va del 0 al 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil para lograr el objetivo predicho dentro del lapso de tiempo definido. Al comparar resultados en diferentes objetivos, se recomienda considerar la probabilidad por encima del percentil o la puntuación. La probabilidad siempre se debe utilizar al determinar la probabilidad promedio en toda la población elegible, ya que la probabilidad tiende a estar en el lado inferior para los eventos que no ocurren con frecuencia. Los valores de probabilidad varían entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles con puntuaciones similares. Por ejemplo, un perfil con una clasificación de percentil de 99 para la pérdida indica que tiene un mayor riesgo de pérdida en comparación con el 99 % de todos los demás perfiles marcados. Los percentiles van del 1 al 100. |
| Tipo de tendencia | El tipo de tendencia seleccionado. |
| Fecha de puntuación | La fecha en la que se produjo la puntuación. |
| Factores influyentes | Razones previstas sobre por qué es probable que un perfil se convierta o se renueve. Los factores se componen de los siguientes atributos:<ul><li>Código: el perfil o atributo de comportamiento que influye positivamente en la puntuación prevista de un perfil. </li><li>Valor: Valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o atributo de comportamiento en la puntuación predicha (baja, media, alta)</li></ul> |

>[!NOTE]
>
> - La inteligencia artificial aplicada al cliente solo utiliza datos actualizados para una formación y puntuación adicionales. Del mismo modo, cuando solicita eliminar datos, la inteligencia artificial aplicada al cliente se abstiene de utilizar los datos eliminados.
> - Customer AI aprovecha los conjuntos de datos de Platform. Para admitir solicitudes de derechos de consumidor que una marca pueda recibir, las marcas deben utilizar Platform Privacy Service para enviar solicitudes de acceso y eliminación de consumidores con el fin de eliminar sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real.
> - Todos los conjuntos de datos que utilizamos para la entrada/salida de modelos seguirán las directrices de Platform. El cifrado de datos de Platform se aplica a los datos en reposo y en tránsito. Consulte la documentación para obtener más información sobre [cifrado de datos](../../../help/landing/governance-privacy-security/encryption.md)


## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya establecido todas sus credenciales y esquemas, comience por seguir el [Configuración de una instancia de Customer AI](./user-guide/configure.md) guía. Esta guía le explica cómo crear una instancia para la inteligencia artificial aplicada al cliente.




