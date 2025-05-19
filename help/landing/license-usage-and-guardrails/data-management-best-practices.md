---
title: Prácticas recomendadas de licencia de administración de datos
description: Obtenga información acerca de las prácticas recomendadas y herramientas que puede utilizar para administrar mejor sus derechos de licencia con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: a14d94a87eb433dd0bb38e5bf3c9c3a04be9a5c6
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 1%

---

# Prácticas recomendadas de asignación de licencias de administración de datos

Adobe Experience Platform es un sistema abierto que transforma sus datos en perfiles de clientes sólidos que se actualizan en tiempo real y utiliza perspectivas impulsadas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales. Puede introducir datos de distintos tipos, volúmenes e historiales en Experience Platform mediante fuentes y, a continuación, atender esos datos en casos de uso que van desde la segmentación y personalización hasta el análisis y el aprendizaje automático.

Experience Platform ofrece licencias que establecen la cantidad de perfiles que puede crear y la cantidad de datos que puede introducir. Dada la capacidad de incorporar cualquier fuente, volumen o historial de datos, es posible superar los derechos de licencia a medida que crezcan los volúmenes de datos.

Lea esta guía para conocer las prácticas recomendadas a seguir y las herramientas que puede utilizar para administrar mejor las autorizaciones de Experience Platform.

## Resumen de funciones {#summary-of-features}

Utilice las prácticas recomendadas y las herramientas descritas en este documento para administrar mejor el uso de las autorizaciones en Experience Platform. Este documento se actualiza a medida que se lanzan funciones adicionales para ayudar a proporcionar visibilidad y control a todos los clientes de Experience Platform.

La siguiente tabla describe la lista de funciones disponibles actualmente para administrar mejor el derecho de uso de licencias.

| Función | Descripción |
| --- | --- |
| [IU de conjunto de datos - Retención de datos de evento de experiencia](../../catalog/datasets/user-guide.md#data-retention-policy) | Configure un período de retención de datos fijo en el lago de datos y el almacén de perfiles. Los registros se eliminan al finalizar el período de retención configurado. |
| [Habilitar/deshabilitar conjuntos de datos para el perfil del cliente en tiempo real](../../catalog/datasets/user-guide.md) | Habilite o deshabilite la ingesta de conjuntos de datos en el Perfil del cliente en tiempo real. |
| [Caducidad de evento de experiencia en el almacén de perfiles](../../profile/event-expirations.md) | Aplique una hora de caducidad para todos los eventos introducidos en un conjunto de datos con perfil habilitado. Póngase en contacto con el equipo de su cuenta de Adobe o con el Servicio de atención al cliente para habilitar esta función. |
| [Filtros de preparación de datos de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | Aplique [!DNL Kafka] filtros para excluir la ingesta de datos innecesarios. |
| [Filtros del conector de origen de Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Aplique filtros de conexión de origen de Audience Manager para excluir los datos innecesarios de la ingesta. |
| [Filtros de datos de reenvío de eventos](../../tags/ui/event-forwarding/overview.md) | Aplique filtros [!DNL Kafka] del lado del servidor para excluir la ingesta de datos innecesarios.  Consulte la documentación sobre [reglas de etiquetas](../../tags/ui/managing-resources/rules.md) para obtener más información. |
| [IU del panel de uso de licencias](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Monitorice el consumo de productos de Experience Platform por parte de su organización en relación con los derechos con licencia. Acceda a instantáneas de uso diario, tendencias predictivas y datos detallados a nivel de zona protegida para admitir la administración proactiva de licencias. |
| [API de informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md) | Genera los conjuntos de datos que más contribuyen a su audiencia direccionable. |
| [API de informe de superposición de identidad](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Genera las áreas de nombres de identidad que más contribuyen a su audiencia direccionable. |
| [Caducidad de datos de perfil seudónimo](../../profile/pseudonymous-profiles.md) | Configure los tiempos de caducidad de los datos para perfiles seudónimos y elimine automáticamente los datos del almacén de perfiles. |

{style="table-layout:auto"}

## Explicación del almacenamiento de datos de Experience Platform

Experience Platform se compone principalmente de dos repositorios de datos: el lago de datos y el almacén de perfiles.

El lago de datos sirve principalmente para los siguientes propósitos:

* Actúa como área de ensayo para la incorporación de datos en Experience Platform;
* Actúa como almacenamiento de datos a largo plazo para todos los datos de Experience Platform;
* Habilita casos de uso, como análisis de datos y ciencia de datos.

El almacén de perfiles **Profile Store** es donde se crean los perfiles de cliente y sirve principalmente para los siguientes propósitos:

* Actúa como almacenamiento de datos para perfiles que se utilizan para admitir experiencias en tiempo real;
* Habilita casos de uso como segmentación, activación y personalización.

>[!NOTE]
>
>Su acceso a [!DNL data lake] puede depender del SKU del producto que adquirió. Para obtener más información sobre los SKU de productos, póngase en contacto con su representante de Adobe.

## Uso de licencias {#license-usage}

Al obtener la licencia de Experience Platform, se le otorgan derechos de uso de licencia que varían según el SKU:

**[!DNL Addressable Audience]**: el número total de perfiles de clientes que están permitidos por contrato en Experience Platform, incluidos los perfiles conocidos y seudónimos.

**[!DNL Total Data Volume]**: cantidad total de datos disponibles para el perfil del cliente en tiempo real que se utilizará en los flujos de trabajo de participación.

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían según la licencia que haya adquirido su organización.

## Panel de uso de licencias

La interfaz de usuario de Adobe Experience Platform proporciona un panel a través del cual puede ver una instantánea de los datos relacionados con las licencias de su organización para Experience Platform. Los datos del tablero se muestran exactamente como aparecen en el momento específico en el que se tomó la instantánea. La instantánea no es una aproximación ni una muestra de datos y el panel no se actualiza en tiempo real.

Para obtener más información, consulte la guía de [uso del panel de uso de licencias en la interfaz de usuario de Experience Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### ¿Qué datos introducir en Experience Platform?

Los datos se pueden ingerir en uno o varios sistemas de Experience Platform, a saber, [!DNL data lake] y/o el almacén de perfiles. Esto significa que pueden existir diferentes datos en ambos sistemas para una variedad de casos de uso diferentes. Por ejemplo, es posible que desee guardar los datos históricos en [!DNL data lake], pero no en el almacén de perfiles. Puede seleccionar qué datos enviar al almacén de perfiles habilitando un conjunto de datos para la ingesta de perfiles.

>[!NOTE]
>
>Su acceso a [!DNL data lake] puede depender del SKU del producto que adquirió. Para obtener más información sobre los SKU de productos, póngase en contacto con su representante de Adobe.

### ¿Qué datos se deben conservar?

Puede aplicar filtros de ingesta de datos y reglas de caducidad para eliminar datos que hayan quedado obsoletos para sus casos de uso. Normalmente, los datos de comportamiento (como los datos de Analytics) consumen mucho más almacenamiento que los datos de registro (como los datos CRM). Por ejemplo, muchos usuarios de Experience Platform tienen hasta un 90 % de perfiles que se rellenan solo con datos de comportamiento, en comparación con los datos de registro. Por lo tanto, la administración de los datos de comportamiento es crítica para garantizar el cumplimiento de los derechos de licencia.

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
| Filtrado de origen de Adobe Audience Manager | Al crear una conexión de origen de Adobe Audience Manager, puede elegir qué segmentos y características incorporar al [!DNL data lake] y al Perfil del cliente en tiempo real, en lugar de ingerir los datos de Audience Manager en su totalidad. Consulte la guía de [creación de una conexión de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| Preparación de datos de Adobe Analytics | Puede utilizar las funcionalidades [!DNL Data Prep] al crear una conexión de origen de Analytics para filtrar los datos que no son necesarios para sus casos de uso. A través de [!DNL Data Prep], puede definir qué atributos/columnas se deben publicar en el perfil. También puede proporcionar instrucciones condicionales para informar a Experience Platform de si se espera que los datos se publiquen en el perfil o solo en [!DNL data lake]. Consulte la guía de [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad con habilitar/deshabilitar conjuntos de datos para el perfil | Para introducir datos en el Perfil del cliente en tiempo real, debe habilitar un conjunto de datos para su uso en el almacén de perfiles. Al hacerlo, agrega a sus derechos de [!DNL Addressable Audience] y [!DNL Total Data Volume]. Una vez que un conjunto de datos ya no es necesario para casos de uso de perfiles de clientes, puede deshabilitar la integración de ese conjunto de datos a Perfil para garantizar que los datos sigan siendo compatibles con la licencia. Consulte la guía sobre [habilitar y deshabilitar conjuntos de datos para el perfil](../../catalog/datasets/enable-for-profile.md) para obtener más información. |
| Exclusión de datos de Web SDK y Mobile SDK | Web y Mobile SDK recopilan dos tipos de datos: datos que se recopilan automáticamente y datos que recopila explícitamente su desarrollador. Para administrar mejor el cumplimiento de la licencia, puede deshabilitar la recopilación automática de datos en la configuración de SDK a través de la configuración de contexto. El desarrollador también puede eliminar o no definir datos personalizados. |
| Exclusión de datos del reenvío del lado del servidor | Si está enviando datos a Experience Platform mediante el reenvío del lado del servidor, puede excluir qué datos se envían eliminando la asignación en una acción de regla para excluirlos en todos los eventos o añadiendo condiciones a la regla para que los datos solo se activen para determinados eventos. Consulte la documentación sobre [eventos y condiciones](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if) para obtener más información. |
| Filtrado de datos en el nivel de origen | Puede utilizar operadores lógicos y de comparación para filtrar los datos de nivel de fila a partir de los orígenes antes de crear una conexión e introducir datos en Experience Platform. Para obtener más información, lea la guía sobre [filtrado de datos de nivel de fila para un origen mediante la [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Almacén de perfiles {#profile-service}

El almacén de perfiles está compuesto por los siguientes componentes:

| Componente de almacén de perfiles | Descripción |
| --- | --- |
| Fragmentos de perfil | Cada perfil de cliente está compuesto por varios **fragmentos de perfil** que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con su marca en varios canales, su organización tendrá varios **fragmentos de perfil** relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan en Experience Platform, se unen mediante el gráfico de identidades para crear un único perfil para ese cliente. **Los fragmentos de perfil** constan de un área de nombres de identidad como identificador, con datos de registro o datos de series temporales asociados. |
| Registro de datos (Atributos) | Un perfil es una representación de un sujeto, una organización o un individuo, compuesta por muchos **Atributos** (también conocidos como **datos de registro**). Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellidos y dirección de correo electrónico. **Registrar datos** suele tener un volumen bajo o moderado, pero es útil durante largos períodos de tiempo. |
| Datos de series temporales (comportamiento) | **Los datos de series temporales** proporcionan información sobre el comportamiento de un usuario. Representados por la clase de esquema estándar Experience Data Model (XDM) [!DNL ExperienceEvent], los datos de series temporales pueden describir eventos como elementos que se agregan al carro de compras, vínculos en los que se hace clic y vídeos visualizados. El valor del comportamiento puede disminuir con el tiempo. |
| Área de nombres de identidad (identidades) | A medida que los datos de los clientes se reúnen, se combinan en un único perfil mediante el uso de **áreas de nombres de identidad**, y la capacidad de unir estas identidades a medida que se conoce más información sobre el usuario. Vea la [descripción general de áreas de nombres de identidad](../../identity-service/features/namespaces.md) para obtener más información. |

{style="table-layout:auto"}

### Informes de composición del almacén de perfiles

Hay varios informes disponibles para ayudarle a comprender la composición del almacén de perfiles. Estos informes le ayudan a tomar decisiones informadas sobre cómo y dónde establecer las caducidades de los eventos de experiencia para optimizar el uso de la licencia:

* **API de informe de superposición de conjuntos de datos**: expone los conjuntos de datos que más contribuyen a su audiencia direccionable. Puede utilizar este informe para identificar para qué [!DNL ExperienceEvent] conjuntos de datos establecer una caducidad. Consulte el tutorial sobre [generación del informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md) para obtener más información.
* **API de informe de superposición de identidad**: expone las áreas de nombres de identidad que más contribuyen a su audiencia direccionable. Consulte el tutorial sobre [generación del informe de superposición de identidades](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) para obtener más información.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### Caducidad de datos de perfil seudónimo {#pseudonymous-profile-expirations}

Utilice la capacidad Caducidad de datos de perfiles seudónimos para quitar automáticamente datos de que ya no son válidos o útiles para sus casos de uso del almacén de perfiles. La caducidad de datos de perfil seudónimo elimina los registros de evento y de perfil. Como resultado, esta configuración reducirá los volúmenes de Audiencia direccionable. Para obtener más información sobre esta característica, lea [Información general sobre la caducidad de los datos del perfil seudónimo](../../profile/pseudonymous-profiles.md).

### IU de conjunto de datos: retención de conjuntos de datos de Experience Event {#data-retention}

Configure la caducidad y la retención del conjunto de datos para aplicar un período de retención fijo a los datos en el lago de datos y el almacén de perfiles. Una vez finalizado el período de retención, se eliminan los datos. La caducidad de datos de Experience Event solo elimina eventos y no elimina datos de clase de perfil, lo que reducirá el [volumen total de datos](total-data-volume.md) en las métricas de uso de licencias. Para obtener más información, lea la guía sobre [configuración de la directiva de retención de datos](../../catalog/datasets/user-guide.md#data-retention-policy).

### Caducidad de eventos de experiencia de perfil {#event-expirations}

Configure los tiempos de caducidad para eliminar automáticamente los datos de comportamiento del conjunto de datos con perfil habilitado una vez que ya no sean útiles para sus casos de uso. Lea la descripción general de [Vencimientos de eventos de experiencia](../../profile/event-expirations.md) para obtener más información.

## Resumen de las prácticas recomendadas para el cumplimiento de licencias {#best-practices}

A continuación se muestra una lista de algunas prácticas recomendadas que puede seguir para garantizar un mejor cumplimiento de los derechos de uso de licencias:

* Use el [tablero de uso de licencias](../../dashboards/guides/license-usage.md) para rastrear y supervisar las tendencias de uso de los clientes. Esto le permite adelantarse a cualquier posible uso adicional en el que pueda incurrir.
* Configure [filtros de ingesta](#ingestion-filters) identificando los eventos necesarios para los casos de uso de segmentación y personalización. Esto le permite enviar solo los eventos importantes necesarios para sus casos de uso.
* Asegúrese de que solo tiene [conjuntos de datos habilitados para el perfil](#ingestion-filters) que son necesarios para los casos de uso de segmentación y personalización.
* Configure [caducidades de eventos de experiencia](../../catalog/datasets/user-guide.md#data-retention-policy) y [caducidades de datos de perfiles seudónimos](../../profile/pseudonymous-profiles.md) para datos de alta frecuencia como datos web.
* Configure las políticas de retención de [tiempo de vida (TTL) para los conjuntos de datos de evento de experiencia](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) en el lago de datos a fin de eliminar automáticamente los registros obsoletos y optimizar el uso del almacenamiento en línea con las autorizaciones.
* Compruebe periódicamente [informes de composición de perfiles](#profile-store-composition-reports) para comprender su composición de almacén de perfiles. Esto le permite comprender las fuentes de datos que más contribuyen al consumo de licencias.
