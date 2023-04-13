---
keywords: Experience Platform;introducción;ai del cliente;temas populares;entrada de ayuda del cliente;salida de ayuda del cliente; requisitos de datos
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Requisitos de datos en Customer AI
topic-legacy: Getting started
description: Obtenga más información sobre los eventos, entradas y salidas necesarios que utiliza Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# Entrada y salida en Customer AI

El siguiente documento describe los diferentes eventos, entradas y salidas necesarios que se utilizan en Customer AI.

## Primeros pasos {#getting-started}

Estos son los pasos para crear modelos de inclinación e identificar audiencias objetivo para el marketing personalizado en Customer AI:

1. Casos de uso de esquema: ¿Cómo ayudarían los modelos de propensión a identificar las audiencias objetivo para el marketing personalizado? ¿Cuáles son mis objetivos comerciales y las tácticas correspondientes para lograr el objetivo? ¿Dónde se puede ajustar el modelado de tendencia en este proceso?

2. Priorizar los casos de uso: ¿Cuáles son las prioridades más altas para el negocio?

3. Creación de modelos en Customer AI: Observe esto [tutorial rápido](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=es) y consulte nuestra [Guía de la interfaz de usuario](../customer-ai/user-guide/configure.md) para un proceso paso a paso para crear un modelo.

4. [Generar segmentos](../customer-ai/user-guide/create-segment.md) uso de resultados de modelo.

5. Realice acciones comerciales segmentadas en función de estos segmentos. Supervise los resultados e itere las acciones para mejorar.

A continuación, se muestran ejemplos de configuraciones para su primer modelo.  El modelo de ejemplo, integrado en este documento, utiliza un modelo de AI del cliente para predecir quién probablemente realizará una conversión para un negocio minorista en los próximos 30 días. El conjunto de datos de entrada es un conjunto de datos de Adobe Analytics.

| Paso | Definición | Ejemplo |
| ---- | ------ | ------- |
| Configurar | Especifique información básica sobre el modelo. | **Nombre**: Modelo de propensión de compra de lápiz <br> **Tipo de modelo**: Conversión |
| Seleccionar datos | Especifique los conjuntos de datos utilizados para crear el modelo. | **Conjunto de datos**: Conjunto de datos de Adobe Analytics <br> **Identidad**: Asegúrese de que la columna de identidad de cada conjunto de datos esté configurada como una identidad común. |
| Definir objetivo | Defina el objetivo, la población apta, los eventos personalizados y los atributos de perfil. | **Objetivo de predicción**: Select `commerce.purchases.value` es igual a lápiz <br> **Ventana de resultado**: 30 días. |
| Definir opciones | Configuración de la programación para la actualización del modelo y habilitación de puntuaciones para Perfil | **Programación**: Semanal <br> **Habilitar para perfil**: Debe habilitarse para que el resultado del modelo se utilice en la segmentación. |

## Información general de datos {#data-overview}

Las siguientes secciones describen los diferentes eventos, entradas y salidas requeridos que se utilizan en Customer AI.

La AI del cliente funciona analizando los siguientes conjuntos de datos para predecir las puntuaciones de tendencia de pérdida (cuando es probable que un cliente deje de utilizar el producto) o conversión (cuando es probable que un cliente realice una compra):

- Los datos de Adobe Analytics que utilizan la variable [Conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Los datos de Adobe Audience Manager que utilizan la variable [Conector de origen del Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Conjunto de datos de Evento de experiencia](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Conjunto de datos del Evento de experiencia del consumidor](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

Puede agregar varios conjuntos de datos de diferentes fuentes si cada uno de los conjuntos de datos comparte el mismo tipo de identidad (área de nombres), como un ECID. Para obtener más información sobre la adición de varios conjuntos de datos, consulte la [Guía del usuario de Customer AI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Los conectores de origen tardan hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe verificar que el conjunto de datos tenga la longitud mínima de datos requerida para Customer AI. Revise el [datos históricos](#data-requirements) para verificar que tiene datos suficientes para el objetivo de predicción.

La siguiente tabla describe algunos términos comunes utilizados en este documento:

| Término | Definición |
| --- | --- |
| [Modelo de datos de experiencia (XDM)](../../xdm/home.md) | XDM es el marco fundamental que permite a Adobe Experience Cloud, con tecnología de Adobe Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. Platform utiliza el sistema XDM para organizar los datos de una determinada manera que facilita su uso para los servicios de Platform. |
| [Esquema XDM](../../xdm/schema/composition.md) | Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase XDM base y de cero o más grupos de campos de esquema. |
| [Clase XDM](../../xdm/schema/field-constraints.md) | Todos los esquemas XDM describen datos que se pueden categorizar como `Experience Event`. El comportamiento de los datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos determinado. |
| [Grupos de campo](../../xdm/schema/composition.md) | Componente que define uno o más campos de un esquema. Los grupos de campos refuerzan la forma en que sus campos aparecen en la jerarquía del esquema y, por lo tanto, muestran la misma estructura en cada esquema en el que están incluidos. Los grupos de campo solo son compatibles con clases específicas, según se identifiquen por sus `meta:intendedToExtend` atributo. |
| [Tipo de datos](../../xdm/schema/composition.md) | Componente que también puede proporcionar uno o más campos para un esquema. Sin embargo, a diferencia de los grupos de campos, los tipos de datos no están restringidos a una clase en particular. Esto hace que los tipos de datos sean una opción más flexible para describir estructuras de datos comunes que se pueden reutilizar en varios esquemas con clases potencialmente diferentes. Los tipos de datos descritos en este documento son compatibles con los esquemas CEE y Adobe Analytics. |
| [Perfil del cliente en tiempo real](../../profile/home.md) | El perfil del cliente en tiempo real proporciona un perfil de cliente centralizado para la administración de experiencias personalizadas y con un público objetivo. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que involucran al individuo que han tenido lugar en cualquiera de los sistemas que utiliza con el Experience Platform. |

## Datos de entrada de Customer AI {#customer-ai-input-data}

Para conjuntos de datos de entrada, como Adobe Analytics y Adobe Audience Manager, los respectivos conectores de origen asignan directamente los eventos de estos grupos de campos estándar (Comercio, Web, Aplicación y Búsqueda) de forma predeterminada durante el proceso de conexión. La tabla siguiente muestra los campos de evento en los grupos de campos estándar predeterminados para Customer AI.

Para obtener más información sobre la asignación de datos de Adobe Analytics o datos de Audience Manager, visite Asignación de campos o Audience Manager de Analytics [guía de asignaciones de campos](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Puede utilizar esquemas XDM de Evento de experiencia del consumidor o Evento de experiencia del consumidor para conjuntos de datos de entrada que no se rellenan mediante uno de los conectores anteriores. Se pueden agregar grupos de campos XDM adicionales durante el proceso de creación del esquema. Los grupos de campos se pueden proporcionar mediante Adobe, como los grupos de campos estándar o un grupo de campos personalizado, que coincida con la representación de datos en Platform.

>[!IMPORTANT]
>
>Debe asegurarse de que los datos se rellenen en estos conjuntos de datos de entrada. Si no se encuentran eventos de grupos de campos estándar en los conjuntos de datos de entrada, debe agregar eventos personalizados durante el flujo de trabajo de configuración. Consulte los detalles sobre los eventos personalizados.

### Grupos de campos estándar utilizados por Customer AI {#standard-events}

Los eventos de experiencia se utilizan para determinar distintos comportamientos de los clientes. Según la estructura de sus datos, es posible que los tipos de eventos enumerados a continuación no abarquen todos los comportamientos de sus clientes. Depende de usted determinar qué campos tienen los datos necesarios para identificar la actividad del usuario en la web u otro canal específico de forma clara e inequívoca. Según el objetivo de la predicción, los campos necesarios pueden cambiar.

>[!NOTE]
>
>Si utiliza datos de Adobe Analytics o Adobe Audience Manager, el esquema se crea automáticamente con los eventos estándar necesarios para capturar los datos. Si está creando su propio esquema EE personalizado para capturar datos, debe tener en cuenta qué grupos de campos son necesarios para capturar los datos.

Customer AI utiliza los eventos de estos cuatro grupos de campos estándar de forma predeterminada: Comercio, Web, Aplicación y Búsqueda. No es necesario tener datos para cada evento en los grupos de campos estándar enumerados a continuación, pero ciertos eventos son necesarios para ciertos escenarios. Si hay eventos disponibles en los grupos de campos estándar, se recomienda incluirlos en el esquema. Por ejemplo, si desea crear un modelo de AI del cliente para predecir eventos de compra, resulta útil tener datos de los grupos de campos de detalles de página web y comercio .

Para ver un grupo de campos en la interfaz de usuario de Platform, seleccione la opción **[!UICONTROL Esquemas]** en el carril izquierdo seguido de seleccionar la **[!UICONTROL Grupos de campo]** pestaña .

| Grupo de campos | Tipo de evento | Ruta de campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalles del comercio] | pedido | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | cierres de compra | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | compras | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Detalles web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Detalles de la aplicación] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Detalles de búsqueda] | búsqueda | `search.keywords` |

Además, Customer AI puede utilizar los datos de suscripción para crear modelos de mejor reproducción. Se necesitan datos de suscripción para cada perfil que utiliza la variable [[!UICONTROL Suscripción]](../../xdm/data-types/subscription.md) formato de tipo de datos. La mayoría de los campos son opcionales, sin embargo, para un modelo de pérdida óptimo, se recomienda proporcionar datos para tantos campos como sea posible, como, por ejemplo, `startDate`, `endDate`, y cualquier otro detalle relevante. Póngase en contacto con el equipo de su cuenta para obtener soporte adicional sobre esta función.

### Adición de eventos personalizados y atributos de perfil {#add-custom-events}

Si tiene información que desea incluir además del valor predeterminado [campos de evento estándar](#standard-events) utilizado por Customer AI, puede utilizar la variable [configuración de evento personalizada](./user-guide/configure.md#custom-events) para aumentar los datos utilizados por el modelo.

#### Cuándo utilizar eventos personalizados

Los eventos personalizados son necesarios cuando los conjuntos de datos elegidos en el paso de selección del conjunto de datos contienen *ninguno* de los campos de evento predeterminados utilizados por Customer AI. Customer AI necesita información sobre al menos un evento de comportamiento de usuario que no sea el resultado.

Los eventos personalizados son útiles para:

- Incorporación de conocimientos de dominio o experiencia previa en el modelo.

- Mejora de la calidad del modelo predictivo.

- Obtención de perspectivas e interpretaciones adicionales.

Los mejores candidatos para eventos personalizados son los datos que contienen conocimiento del dominio que puede ser predictivo del resultado. Algunos ejemplos generales de eventos personalizados son:

- Registrarse en la cuenta

- Suscribirse a la newsletter

- Realizar una llamada al servicio al cliente

A continuación se muestra una selección de ejemplos de eventos personalizados específicos del sector:

| de la industria | Eventos personalizados |
| --- | --- |
| Comercial | Transacción en el almacén<br>Inscríbase en la tarjeta club<br>Clip de cupón móvil. |
| Entretenimiento | abono de temporada de compra <br> Reproducir vídeo. |
| Hospitalidad | Hacer reserva de restaurante <br> Comprar puntos de lealtad. |
| Viaje | Añada información conocida del viajero Comprar millas. |
| Comunicaciones | Plan de actualización/baja/cancelación. |

Los eventos personalizados deben representar las acciones iniciadas por el usuario para que se puedan seleccionar. Por ejemplo, &quot;Envío de correo electrónico&quot; es una acción iniciada por un especialista en marketing y no por el usuario, por lo que no debe utilizarse como evento personalizado.

### Datos históricos

Customer AI requiere datos históricos para la formación de modelos. La duración requerida para que los datos existan dentro del sistema está determinada por dos elementos clave: la ventana de resultados y la población elegible.

De forma predeterminada, Customer AI busca un usuario que haya tenido actividad en los últimos 45 días si no se proporciona ninguna definición de población apta durante la configuración de la aplicación. Además, Customer AI requiere un mínimo de 500 eventos calificativos y 500 eventos no calificativos (un total de 1000) a partir de datos históricos basados en una definición de objetivo predicha.

Los siguientes ejemplos muestran el uso de una fórmula sencilla que le ayuda a determinar la cantidad mínima de datos necesaria. Si tiene más datos que el requisito mínimo, es probable que el modelo proporcione resultados más precisos. Si tiene menos de la cantidad mínima requerida, el modelo fallará, ya que no hay suficientes datos para la formación del modelo.

**Fórmula**:

Para decidir la duración mínima requerida de los datos existentes en el sistema:

- Los datos mínimos necesarios para crear funciones son de 30 días. Compare la ventana retrospectiva de idoneidad con 30 días:

   - Si la ventana retrospectiva de idoneidad es buena a más de 30 días, el requisito de datos = ventana retrospectiva de idoneidad + ventana de resultado.

   - De lo contrario, el requisito de datos = 30 días + ventana de resultados.

** Si hay más de una condición para definir la población elegible, la ventana de retrospectiva de elegibilidad es la más larga.

>[!NOTE]
>
>30 es el número mínimo de días necesarios para la población elegible. Si no se proporciona, el valor predeterminado es de 45 días.

**Ejemplos**:

- Desea predecir si es probable que un cliente compre un reloj en los próximos 30 días para aquellos que tengan alguna actividad web en los últimos 60 días.

   - Período de retrospectiva de elegibilidad = 60 días

   - Período de respuesta = 30 días

   - Datos necesarios = 60 días + 30 días = 90 días

- Desea predecir si es probable que el usuario compre un reloj en los próximos 7 días **without** proporcionar una población elegible explícita. En este caso, la población elegible toma como valor predeterminado &quot;aquellos que han tenido actividad en los últimos 45 días&quot; y la ventana de resultados es de 7 días.

   - Período de retrospectiva de elegibilidad = 45 días

   - Ventana de resultado = 7 días

   - Datos necesarios = 45 días + 7 días = 52 días

- Desea predecir si es probable que el cliente compre un reloj en los próximos 7 días para aquellos que tengan alguna actividad web en los últimos 7 días.

   - Período de retrospectiva de elegibilidad = 7 días

   - Datos mínimos necesarios para crear funciones = 30 días

   - Ventana de resultado = 7 días

   - Datos necesarios = 30 días + 7 días = 37 días

Aunque la AI del cliente requiere un período de tiempo mínimo para que los datos existan en el sistema, también funciona mejor con los datos recientes. Al utilizar datos de comportamiento más recientes, es probable que la AI del cliente genere una predicción más precisa del comportamiento futuro de un usuario.

## Datos de salida de Customer AI {#customer-ai-output-data}

La AI del cliente genera varios atributos para perfiles individuales que se consideran aptos. Existen dos formas de utilizar la puntuación (salida) en función de lo que haya aprovisionado. Si tiene un conjunto de datos habilitado para Perfil del cliente en tiempo real, puede consumir perspectivas de Perfil del cliente en tiempo real en la variable [Generador de segmentos](../../segmentation/ui/segment-builder.md). Si no tiene un conjunto de datos habilitado para Perfil, puede [descargar la salida Customer AI](./user-guide/download-scores.md) conjunto de datos disponible en el lago de datos.

Puede encontrar el conjunto de datos de salida en la plataforma **Conjuntos de datos** espacio de trabajo. Todos los conjuntos de datos de salida de Customer AI comienzan con el nombre **Puntuaciones de Customer AI: NAME_OF_APP**. Del mismo modo, todos los esquemas de salida de Customer AI comienzan con el nombre **Esquema AI del cliente: Nombre de la aplicación**.

![Nombre de los conjuntos de datos de salida en Customer AI](./images/user-guide/cai-schema-name-of-app.png)

La tabla siguiente describe los distintos atributos que se encuentran en la salida de Customer AI:

| Atributo | Descripción |
| ----- | ----------- |
| [!UICONTROL Puntuación] | La probabilidad relativa de que un cliente logre el objetivo predicho dentro del lapso de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino como la probabilidad de un individuo en comparación con la población total. Esta puntuación va del 0 al 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil de alcanzar el objetivo predicho dentro del lapso de tiempo definido. Al comparar resultados entre objetivos diferentes, se recomienda tener en cuenta la probabilidad sobre el percentil o la puntuación. La probabilidad siempre debe utilizarse al determinar la probabilidad promedio entre la población elegible, ya que la probabilidad tiende a estar en el lado inferior para los eventos que no ocurren con frecuencia. Los valores para el rango de probabilidad entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles de puntuación similar. Por ejemplo, un perfil con una clasificación de percentil de 99 para la pérdida indica que tiene un mayor riesgo de pérdida en comparación con el 99% de todos los demás perfiles que se clasificaron. Los percentiles varían de 1 a 100. |
| Tipo de propensión | El tipo de tendencia seleccionado. |
| Fecha de puntuación | Fecha en la que se produjo la puntuación. |
| Factores influyentes | Estas son razones predichas por las que es probable que un perfil se convierta o produzca. Estos factores se componen de los siguientes atributos:<ul><li>Código: El perfil o atributo de comportamiento que influye positivamente en la puntuación predicha de un perfil. </li><li>Valor: El valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o atributo de comportamiento que tiene en la puntuación predicha (baja, media, alta)</li></ul> |

## Pasos siguientes {#next-steps}

Una vez que prepare los datos y se asegure de que todas las credenciales y esquemas están establecidos, consulte la [Configuración de una instancia de AI del cliente](./user-guide/configure.md) guía, que le guiará por un tutorial paso a paso para crear una instancia de AI del cliente.