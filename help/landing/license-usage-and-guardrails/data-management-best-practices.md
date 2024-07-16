---
title: Prácticas recomendadas de licencia de administración de datos
description: Obtenga información acerca de las prácticas recomendadas y herramientas que puede utilizar para administrar mejor sus derechos de licencia con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 2%

---

# Prácticas recomendadas de asignación de licencias de administración de datos

Adobe Experience Platform es un sistema abierto que transforma sus datos en perfiles de clientes sólidos que se actualizan en tiempo real y utiliza perspectivas impulsadas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales. Puede introducir datos de distintos tipos, volúmenes e historiales en Experience Platform mediante fuentes y, a continuación, atender esos datos en casos de uso que van desde la segmentación y personalización hasta el análisis y el aprendizaje automático.

Platform ofrece licencias que establecen la cantidad de perfiles que puede crear y la cantidad de datos que puede introducir. Dada la capacidad de incorporar cualquier fuente, volumen o historial de datos, es posible superar los derechos de licencia a medida que crezcan los volúmenes de datos.

Este documento describe las prácticas recomendadas a seguir y las herramientas que puede utilizar para administrar mejor las autorizaciones de Adobe Experience Platform.

## Explicación del almacenamiento de datos de Adobe Experience Platform

El Experience Platform está compuesto principalmente por dos repositorios de datos: el [!DNL data lake] y el almacén de perfiles.

**[!DNL data lake]** sirve principalmente para los siguientes propósitos:

* Actúa como zona de ensayo para la incorporación de datos en Experience Platform;
* Actúa como almacenamiento de datos a largo plazo para todos los datos del Experience Platform;
* Habilita casos de uso, como análisis de datos y ciencia de datos.

El almacén de perfiles **Profile Store** es donde se crean los perfiles de cliente y sirve principalmente para los siguientes propósitos:

* Actúa como almacenamiento de datos para perfiles que se utilizan para admitir experiencias en tiempo real;
* Habilita casos de uso como segmentación, activación y personalización.

>[!NOTE]
>
>Su acceso a [!DNL data lake] puede depender del SKU del producto que adquirió. Para obtener más información sobre los SKU de los productos, póngase en contacto con el representante del Adobe.

## Uso de licencias {#license-usage}

Al otorgar la licencia al Experience Platform, se le otorgan derechos de uso de licencia que varían según el SKU:

**[!DNL Addressable Audience]**: el número total de perfiles de clientes que están permitidos contractualmente en Experience Platform, incluidos los perfiles conocidos y seudónimos.

**[!DNL Profile Richness]**: el tamaño promedio de los datos de perfil en Experience Platform. Puede aumentar sus derechos de [!DNL Profile Richness] comprando un paquete richness.

La métrica [!DNL Profile Richness] varía según la licencia que haya adquirido. Hay dos cálculos disponibles para [!DNL Profile Richness]:

* La suma de todos los datos de producción almacenados en Adobe Real-time Customer Data Platform (es decir, el perfil del cliente en tiempo real y el servicio de identidad) en cualquier momento, dividida por [!DNL Addressable Audience];
* La suma de todos los datos almacenados en Platform (incluidos, entre otros, [!DNL data lake], el perfil del cliente en tiempo real y el servicio de identidad) en cualquier momento y cualquier dato que haya retransmitido a través de Platform (en lugar de almacenarlo) en los últimos 12 meses, dividida por [!DNL Addressable Audience].

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían según la licencia que haya adquirido su organización.

## Panel de uso de licencias

La interfaz de usuario de Adobe Experience Platform proporciona un panel a través del cual puede ver una instantánea de los datos relacionados con las licencias de su organización para Platform. Los datos del tablero se muestran exactamente como aparecen en el momento específico en el que se tomó la instantánea. La instantánea no es una aproximación ni una muestra de datos y el panel no se actualiza en tiempo real.

Para obtener más información, consulte la guía de [uso del panel de uso de licencias en la interfaz de usuario de Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Prácticas recomendadas de administración de datos

Las siguientes secciones describen las prácticas recomendadas que deben seguirse para administrar mejor los datos.

### Explicación de los datos

No todos los datos son iguales en Adobe Experience Platform. Algunos datos pueden ser densos, pero de bajo valor, mientras que otros pueden ser dispersos, pero de alto valor. Algunos datos pueden perder valor en cuanto se generan, mientras que otros pueden ser valiosos durante meses o incluso años.

Hay tres dimensiones que se deben tener en cuenta para comprender el valor de los datos:

| Dimensión | Descripción | Ejemplo |
| --- | --- | --- |
| Volumen | Representa la cantidad y la totalidad de los datos ingeridos. | Clics web: alto volumen y fidelidad moderada. El valor puede disminuir rápidamente. |
| Intervalo de tiempo | Representa el tiempo que los datos ingeridos siguen siendo valiosos. | Compras fuera de línea: moderado en volumen y fidelidad, pero puede ser útil durante largos períodos de tiempo. |
| Fidelidad | Representa la riqueza de los datos con información. | Cuentas de cliente: bajo volumen, pero alta fidelidad. Puede ser útil más allá de la vida útil de un cliente. |

### Herramientas de administración de datos {#data-management-tools}

Hay dos escenarios centrales que se deben tener en cuenta al garantizar que el uso de los datos se mantenga dentro de los límites de los derechos de licencia:

### ¿Qué datos introducir en Platform?

Los datos se pueden ingerir en uno o varios sistemas de Platform, a saber, [!DNL data lake] y/o el almacén de perfiles. Esto significa que pueden existir diferentes datos en ambos sistemas para una variedad de casos de uso diferentes. Por ejemplo, es posible que desee guardar los datos históricos en [!DNL data lake], pero no en el almacén de perfiles. Puede seleccionar qué datos enviar al almacén de perfiles habilitando un conjunto de datos para la ingesta de perfiles.

>[!NOTE]
>
>Su acceso a [!DNL data lake] puede depender del SKU del producto que adquirió. Para obtener más información sobre los SKU de los productos, póngase en contacto con el representante del Adobe.

### ¿Qué datos se deben conservar?

Puede aplicar filtros de ingesta de datos y reglas de caducidad para eliminar datos que hayan quedado obsoletos para sus casos de uso. Normalmente, los datos de comportamiento (como los datos de Analytics) consumen mucho más almacenamiento que los datos de registro (como los datos CRM). Por ejemplo, muchos usuarios de Platform tienen hasta el 90 % de perfiles que se rellenan con datos de comportamiento solos, en comparación con los datos de registro. Por lo tanto, la administración de los datos de comportamiento es crítica para garantizar el cumplimiento de los derechos de licencia.

Hay varias herramientas que puede aprovechar para no salirse de sus derechos de uso de licencias:

* [Filtros de ingesta](#ingestion-filters)
* [Almacén de perfiles](#profile-service)

### Servicio de identidad y audiencia accesible {#identity-service}

Los gráficos de identidad no se contabilizan en el derecho total de audiencia a la que se puede dirigir porque audiencia a la que se puede dirigir hace referencia al recuento total de perfiles de clientes.

Sin embargo, los límites del gráfico de identidades pueden afectar a su audiencia direccionable debido a la división de identidades. Por ejemplo, si se elimina el ECID más antiguo del gráfico, ECID seguirá existiendo en el Perfil del cliente en tiempo real como un perfil seudónimo. Puede establecer [caducidades de datos de perfil seudónimos](../../profile/pseudonymous-profiles.md) para evitar este comportamiento. Para obtener más información, lea las [protecciones para los datos del servicio de identidad](../../identity-service/guardrails.md).

### Filtros de ingesta {#ingestion-filters}

Los filtros de ingesta le permiten introducir únicamente los datos necesarios para sus casos de uso y filtrar todos los eventos que no son necesarios.

| Filtro de ingesta | Descripción |
| --- | --- |
| Filtrado de origen de Adobe Audience Manager | Al crear una conexión de origen de Adobe Audience Manager, puede elegir qué segmentos y características incorporar al [!DNL data lake] y al Perfil del cliente en tiempo real, en lugar de ingerir los datos del Audience Manager en su totalidad. Consulte la guía de [creación de una conexión de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| Preparación de datos de Adobe Analytics | Puede utilizar las funcionalidades [!DNL Data Prep] al crear una conexión de origen de Analytics para filtrar los datos que no son necesarios para sus casos de uso. A través de [!DNL Data Prep], puede definir qué atributos/columnas se deben publicar en el perfil. También puede proporcionar afirmaciones condicionales para informar a Platform de si se espera que los datos se publiquen en el perfil o solo en [!DNL data lake]. Consulte la guía de [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad con habilitar/deshabilitar conjuntos de datos para el perfil | Para introducir datos en el Perfil del cliente en tiempo real, debe habilitar un conjunto de datos para su uso en el almacén de perfiles. Al hacerlo, agrega a sus derechos de [!DNL Addressable Audience] y [!DNL Profile Richness]. Una vez que un conjunto de datos ya no es necesario para casos de uso de perfiles de clientes, puede deshabilitar la integración de ese conjunto de datos a Perfil para garantizar que los datos sigan siendo compatibles con la licencia. Consulte la guía sobre [habilitar y deshabilitar conjuntos de datos para el perfil](../../catalog/datasets/enable-for-profile.md) para obtener más información. |
| Exclusión de datos de SDK web y SDK móvil | El SDK web y móvil recopilan dos tipos de datos: datos que se recopilan automáticamente y datos que el desarrollador recopila explícitamente. Para administrar mejor el cumplimiento de la licencia, puede deshabilitar la recopilación automática de datos en la configuración del SDK a través de la configuración de contexto. El desarrollador también puede eliminar o no definir datos personalizados. |
| Exclusión de datos del reenvío del lado del servidor | Si está enviando datos a Platform mediante el reenvío del lado del servidor, puede excluir qué datos se envían eliminando la asignación en una acción de regla para excluirlos en todos los eventos o añadiendo condiciones a la regla para que los datos solo se activen para determinados eventos. Consulte la documentación sobre [eventos y condiciones](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if) para obtener más información. |
| Filtrado de datos en el nivel de origen | Puede utilizar operadores lógicos y de comparación para filtrar los datos de nivel de fila a partir de los orígenes antes de crear una conexión e introducir datos en Experience Platform. Para obtener más información, lea la guía sobre [filtrado de datos de nivel de fila para un origen mediante la [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Almacén de perfiles {#profile-service}

El almacén de perfiles está compuesto por los siguientes componentes:

| Componente de almacén de perfiles | Descripción |
| --- | --- |
| Fragmentos de perfil | Cada perfil de cliente está compuesto por varios **fragmentos de perfil** que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios **fragmentos de perfil** relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Platform, se vinculan mediante el gráfico de identidad para crear un único perfil para ese cliente. **Los fragmentos de perfil** constan de un área de nombres de identidad como identificador, con datos de registro o datos de series temporales asociados. |
| Registro de datos (Atributos) | Un perfil es una representación de un sujeto, una organización o un individuo, compuesta por muchos **Atributos** (también conocidos como **datos de registro**). Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellidos y dirección de correo electrónico. **Registrar datos** suele tener un volumen bajo o moderado, pero es útil durante largos períodos de tiempo. |
| Datos de series temporales (comportamiento) | **Los datos de series temporales** proporcionan información sobre el comportamiento de un usuario. Representados por la clase de esquema estándar Experience Data Model (XDM) [!DNL ExperienceEvent], los datos de series temporales pueden describir eventos como elementos que se agregan al carro de compras, vínculos en los que se hace clic y vídeos visualizados. El valor del comportamiento puede disminuir con el tiempo. |
| Área de nombres de identidad (identidades) | A medida que los datos de los clientes se reúnen, se combinan en un único perfil mediante el uso de **áreas de nombres de identidad**, y la capacidad de unir estas identidades a medida que se conoce más información sobre el usuario. Vea la [descripción general de áreas de nombres de identidad](../../identity-service/features/namespaces.md) para obtener más información. |

{style="table-layout:auto"}

#### Informes de composición del almacén de perfiles

Hay varios informes disponibles para ayudarle a comprender la composición del almacén de perfiles. Estos informes le ayudan a tomar decisiones informadas sobre cómo y dónde establecer las caducidades de los eventos de experiencia para optimizar el uso de la licencia:

* **API de informe de superposición de conjuntos de datos**: expone los conjuntos de datos que más contribuyen a su audiencia direccionable. Puede utilizar este informe para identificar para qué [!DNL ExperienceEvent] conjuntos de datos establecer una caducidad. Consulte el tutorial sobre [generación del informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md) para obtener más información.
* **API de informe de superposición de identidad**: expone las áreas de nombres de identidad que más contribuyen a su audiencia direccionable. Consulte el tutorial sobre [generación del informe de superposición de identidades](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) para obtener más información.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Caducidad de datos de perfil seudónimo {#pseudonymous-profile-expirations}

Esta capacidad le permite eliminar automáticamente perfiles seudónimos antiguos del almacén de perfiles. Para obtener más información sobre esta característica, lea [Información general sobre la caducidad de los datos del perfil seudónimo](../../profile/pseudonymous-profiles.md).

#### Caducidad de Experience Event {#event-expirations}

Esta capacidad le permite eliminar automáticamente datos de comportamiento de un conjunto de datos con perfil habilitado que ya no es útil para sus casos de uso. Consulte la descripción general de [Caducidad de eventos de experiencia](../../profile/event-expirations.md) para obtener detalles sobre cómo funciona este proceso una vez que está habilitado para un conjunto de datos.

## Resumen de las prácticas recomendadas para el cumplimiento de licencias {#best-practices}

A continuación se muestra una lista de algunas prácticas recomendadas que puede seguir para garantizar un mejor cumplimiento de los derechos de uso de licencias:

* Use el [tablero de uso de licencias](../../dashboards/guides/license-usage.md) para rastrear y supervisar las tendencias de uso de los clientes. Esto le permite adelantarse a cualquier posible uso adicional en el que pueda incurrir.
* Configure [filtros de ingesta](#ingestion-filters) identificando los eventos necesarios para los casos de uso de segmentación y personalización. Esto le permite enviar solo los eventos importantes necesarios para sus casos de uso.
* Asegúrese de que solo tiene [conjuntos de datos habilitados para el perfil](#ingestion-filters) que son necesarios para los casos de uso de segmentación y personalización.
* Configure [caducidades de eventos de experiencia](#event-expirations) y [caducidades de datos de perfiles seudónimos](#pseudonymous-profile-expirations) para datos de alta frecuencia como datos web.
* Compruebe periódicamente [informes de composición de perfiles](#profile-store-composition-reports) para comprender su composición de almacén de perfiles. Esto le permite comprender las fuentes de datos que más contribuyen al consumo de licencias.

## Resumen de funciones y disponibilidad {#feature-summary}

Las prácticas recomendadas y las herramientas descritas en este documento le ayudarán a administrar mejor el uso de las autorizaciones en Adobe Experience Platform. Este documento se actualizará a medida que se publiquen funciones adicionales para ayudar a proporcionar visibilidad y control a todos los clientes de Experience Platform.

La siguiente tabla describe la lista de funciones disponibles actualmente para administrar mejor el derecho de uso de licencias.

| Función | Descripción |
| --- | --- |
| [Habilitar/deshabilitar conjuntos de datos para el perfil](../../catalog/datasets/user-guide.md) | Habilite o deshabilite la ingesta de conjuntos de datos en el Perfil del cliente en tiempo real. |
| [Caducidad de evento de experiencia](../../profile/event-expirations.md) | Aplique una hora de caducidad para todos los eventos introducidos en un conjunto de datos con perfil habilitado. Póngase en contacto con el equipo de su cuenta de Adobe o con el Servicio de atención al cliente para habilitar esta función. |
| [Filtros de preparación de datos de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Aplicar filtros [!DNL Kafka] para excluir la ingesta de datos innecesarios |
| [Filtros del conector de origen de Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Aplicar filtros de conexión de origen del Audience Manager para excluir los datos innecesarios de la ingesta |
| [Filtros de datos de reenvío de eventos](../../tags/ui/event-forwarding/overview.md) | Aplique filtros [!DNL Kafka] del lado del servidor para excluir la ingesta de datos innecesarios.  Consulte la documentación sobre [reglas de etiquetas](../../tags/ui/managing-resources/rules.md) para obtener más información. |
| [IU del panel de uso de licencias](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Vea una instantánea de los datos de licencia de su organización para Experience Platform |
| [API de informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md) | Genera los conjuntos de datos que más contribuyen a su audiencia direccionable |
| [API de informe de superposición de identidad](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Genera las áreas de nombres de identidad que más contribuyen a su audiencia direccionable |

{style="table-layout:auto"}
