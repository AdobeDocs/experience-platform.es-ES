---
keywords: Experience Platform;inicio;temas populares;administración de datos;derechos de licencia;licencia;prácticas recomendadas
title: Prácticas recomendadas del derecho de licencia de gestión de datos
description: Obtenga información acerca de las mejores prácticas y herramientas que puede utilizar para administrar mejor sus derechos de licencia con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 2%

---

# Prácticas recomendadas para las licencias de gestión de datos

Adobe Experience Platform es un sistema abierto que transforma los datos en perfiles de clientes sólidos que se actualizan en tiempo real y que utiliza perspectivas basadas en IA para ayudarle a ofrecer las experiencias correctas en todos los canales. Puede incorporar datos de diversos tipos, volúmenes e historias a un Experience Platform mediante fuentes y, a continuación, ocuparlos para casos de uso que abarquen desde la segmentación y personalización hasta el análisis y el aprendizaje automático.

Platform ofrece licencias que establecen el número de perfiles que puede crear y la cantidad de datos que puede introducir. Dada la capacidad de incorporar cualquier fuente, volumen o historial de datos, es posible superar sus derechos de licencia a medida que crecen sus volúmenes de datos.

Este documento describe las prácticas recomendadas a seguir y las herramientas que puede utilizar para administrar mejor las autorizaciones de Adobe Experience Platform.

## Comprensión del almacenamiento de datos de Adobe Experience Platform

El Experience Platform está compuesto principalmente por dos repositorios de datos: el [!DNL Data Lake] y el Almacenamiento de perfiles.

La variable **[!DNL Data Lake]** sirve principalmente para los siguientes fines:

* Actúa como zona de ensayo para incorporar datos en el Experience Platform;
* Actúa como el almacenamiento de datos a largo plazo para todos los datos del Experience Platform;
* Permite casos de uso como análisis de datos y ciencia de datos.

La variable **Almacenamiento de perfiles** es donde se crean los perfiles de cliente y principalmente sirve para los siguientes fines:

* Actúa como almacenamiento de datos para perfiles que se utilizan para admitir experiencias en tiempo real;
* Habilita casos de uso como segmentación, activación y personalización.

>[!NOTE]
>
>Su acceso a la variable [!DNL Data Lake] puede depender del SKU del producto que haya comprado. Para obtener más información sobre los SKU de producto, póngase en contacto con su representante de Adobe.

## Uso de licencias {#license-usage}

Al Experience Platform de licencias, se le proporcionan derechos de uso de licencias que varían según el SKU:

**[!DNL Addressable Audience]** : el número total de perfiles de cliente que se permiten contractualmente en Experience Platform, incluidos perfiles conocidos y seudónimos.

**[!DNL Profile Richness]** - el tamaño promedio de los datos de perfil en Experience Platform. Puede aumentar su [!DNL Profile Richness] al comprar un paquete de riqueza.

La variable [!DNL Profile Richness] varía en función de la licencia que haya adquirido. Hay dos cálculos para [!DNL Profile Richness] disponible:

* La suma de todos los datos de producción almacenados en Adobe Real-time Customer Data Platform (es decir, el servicio de perfil y el servicio de identidad) en cualquier momento, dividida por la variable [!DNL Addressable Audience];
* La suma de todos los datos almacenados dentro de Platform (incluido, entre otros, el [!DNL Data Lake], servicio de perfil y servicio de identidad) en cualquier momento y cualquier dato que haya transmitido a través (en lugar de almacenarlo en) de Platform en los últimos 12 meses, dividido por el [!DNL Addressable Audience].

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían en función de las licencias que haya adquirido su organización.

## Panel de uso de licencias

La interfaz de usuario de Adobe Experience Platform proporciona un tablero a través del cual puede ver una instantánea de los datos relacionados con las licencias de su organización para Platform. Los datos del tablero se muestran exactamente como aparecen en el momento concreto en que se tomó la instantánea. La instantánea no es una aproximación ni una muestra de datos, y el panel no se actualiza en tiempo real.

Para obtener más información, consulte la guía de [uso del panel de uso de licencias en la interfaz de usuario de Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Prácticas recomendadas de gestión de datos

En las secciones siguientes se describen las prácticas recomendadas a seguir para administrar mejor los datos.

### Comprender los datos

No todos los datos son iguales en Adobe Experience Platform. Algunos datos pueden ser densos, pero de bajo valor, mientras que otros pueden ser dispersos, pero de alto valor. Algunos datos pueden perder valor tan pronto como se generan, mientras que otros pueden ser valiosos durante meses, si no años.

Hay tres dimensiones que se deben tener en cuenta para comprender el valor de los datos:

| Dimensión | Descripción | Ejemplo |
| --- | --- | --- |
| Volumen | Representa la cantidad y la totalidad de los datos introducidos. | Clics web: volumen alto y moderado en fidelidad. El valor puede disminuir rápidamente. |
| Timespan | Representa el tiempo que los datos incorporados siguen siendo valiosos. | Compras sin conexión: volumen y fidelidad moderados, pero pueden ser valiosos durante largos períodos de tiempo. |
| Fidelidad | Representa la riqueza de los datos con la información. | Cuentas de cliente: volumen bajo, pero alta en fidelidad. Puede ser útil más allá de la duración de un cliente. |

### Herramientas de gestión de datos {#data-management-tools}

Hay dos escenarios centrales a tener en cuenta al garantizar que el uso de los datos se mantenga dentro de los límites de la licencia:

### ¿Qué datos se van a incluir en Platform?

Los datos se pueden ingerir en uno o varios sistemas de Platform, concretamente la variable [!DNL Data Lake] o el Almacenamiento de perfiles. Esto significa que pueden existir diferentes datos en ambos sistemas para una variedad de casos de uso diferentes. Por ejemplo, es posible que desee incluir datos históricos en la variable [!DNL Data Lake], pero no en el Almacenamiento de perfiles. Puede seleccionar qué datos desea enviar al Almacenamiento de perfiles habilitando un conjunto de datos para la ingesta de perfiles.

>[!NOTE]
>
>Su acceso a la variable [!DNL Data Lake] puede depender del SKU del producto que haya comprado. Para obtener más información sobre los SKU de producto, póngase en contacto con su representante de Adobe.

### ¿Qué datos se deben conservar?

Puede aplicar tanto filtros de ingesta de datos como reglas de caducidad (también conocidas como &quot;TTL&quot; por el tiempo de vida) para eliminar datos que se hayan vuelto obsoletos en sus casos de uso. Por lo general, los datos de comportamiento (como los datos de Analytics) consumen mucho más almacenamiento que los datos de registro (como los datos CRM). Por ejemplo, muchos usuarios de Platform tienen más del 90 % de los perfiles rellenados solo con datos de comportamiento, en comparación con los datos de registro. Por lo tanto, la administración de los datos de comportamiento es fundamental para garantizar el cumplimiento de las normas en sus derechos de licencia.

Hay varias herramientas que puede aprovechar para mantenerse dentro de sus derechos de uso de licencias:

* [Filtros de ingesta](#ingestion-filters)
* [TTL de servicio de perfil](#profile-service)

### Filtros de ingesta {#ingestion-filters}

Los filtros de ingesta permiten introducir únicamente los datos necesarios para los casos de uso y filtran todos los eventos que no son necesarios.

| Filtro de ingesta | Descripción |
| --- | --- |
| Filtrado de fuentes de Adobe Audience Manager | Al crear una conexión de origen de Adobe Audience Manager, puede elegir qué segmentos y rasgos incluir en la [!DNL Data Lake] y servicio de perfil, en lugar de incorporar los datos del Audience Manager en su totalidad. Consulte la guía de [creación de una conexión de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| Preparación de datos de Adobe Analytics | Puede usar [!DNL Data Prep] al crear una conexión de origen de Analytics para filtrar los datos que no son necesarios para sus casos de uso. Hasta [!DNL Data Prep], puede definir qué atributos/columnas deben publicarse en Perfil. También puede proporcionar afirmaciones condicionales para informar a Platform de si se espera que los datos se publiquen en el perfil o solo en el [!DNL Data Lake]. Consulte la guía de [creación de una conexión de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obtener más información. |
| Compatibilidad para habilitar/deshabilitar conjuntos de datos para Perfil | Para introducir datos en el servicio de perfil, debe habilitar un conjunto de datos para utilizarlo en el almacén de perfiles. Al hacerlo, agrega a su [!DNL Addressable Audience] y [!DNL Profile Richness] derechos. Una vez que ya no se necesita un conjunto de datos para los casos de uso de perfiles de clientes, puede deshabilitar la integración de ese conjunto de datos en Perfil para garantizar que sus datos sigan siendo compatibles con la licencia. Consulte la guía de [activación y desactivación de conjuntos de datos para Perfil](../../catalog/datasets/enable-for-profile.md) para obtener más información. |
| Exclusión de datos del SDK web y del SDK móvil | Existen dos tipos de datos recopilados por el SDK web y móvil: datos que se recopilan automáticamente y datos que el desarrollador recopila explícitamente. Para administrar mejor el cumplimiento de las licencias, puede deshabilitar la recopilación automática de datos en la configuración del SDK mediante la configuración de contexto. El desarrollador también puede eliminar o no establecer los datos personalizados. Consulte la guía de [configuración de los aspectos básicos del SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) para obtener más información. |
| Exclusión de datos de reenvío del lado del servidor | Si está enviando datos a Platform mediante el reenvío del lado del servidor, puede excluir qué datos se envían eliminando la asignación en una acción de regla para excluirla en todos los eventos o agregando condiciones a la regla para que los datos solo se activen para ciertos eventos. Consulte la documentación sobre [eventos y condiciones](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

### Servicio de perfil {#profile-service}

La capacidad TTL (tiempo de vida) del servicio de perfil le permite aplicar TTL en los datos del almacén de perfiles. De este modo, el sistema puede eliminar automáticamente los datos que hayan disminuido su valor con el paso del tiempo.

El Almacenamiento de perfiles está compuesto por los siguientes componentes:

| Componente de Almacenamiento de perfiles | Descripción |
| --- | --- |
| Fragmentos de perfil | Cada perfil de cliente está compuesto por varios **fragmentos de perfil** que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con la marca a través de varios canales, la organización tendrá varios **fragmentos de perfil** relacionado con ese único cliente que aparece en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se vinculan mediante el gráfico de identidad para crear un único perfil para ese cliente. **Fragmentos de perfil** constan de un área de nombres de identidad como identificador, con datos de registro asociados o datos de series temporales. |
| Registrar datos (atributos) | Un perfil es una representación de un sujeto, una organización o un individuo, compuesto por muchos **Atributos** (también conocido como **datos de registro**). Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellido y dirección de correo electrónico. **Registrar datos** por lo general es de volumen bajo/moderado, pero valioso durante largos períodos de tiempo. |
| Datos de series temporales (comportamiento) | **Datos de series temporales** proporciona información sobre el comportamiento de un usuario. Representado por la clase de esquema estándar Experience Data Model (XDM) [!DNL ExperienceEvent], los datos de series temporales pueden describir eventos como elementos que se agregan a un carro, vínculos en los que se hace clic y vídeos vistos. El valor del comportamiento puede disminuir con el tiempo. |
| Área de nombres de identidad (identidades) | A medida que los datos de los clientes se juntan, se combinan en un único perfil mediante el uso de **áreas de nombres de identidad** y la capacidad de unir estas identidades a medida que se conozca más información sobre el usuario. Consulte la [información general sobre áreas de nombres de identidad](../../identity-service/namespaces.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

#### Informes de composición del almacén de perfiles

Hay varios informes disponibles para ayudarle a comprender la composición del Almacenamiento de perfiles. Estos informes le ayudan a tomar decisiones informadas sobre cómo y dónde configurar los TTL de perfil para optimizar mejor el uso de licencias:

* **API de informe de superposición de conjunto de datos**: Expone los conjuntos de datos que contribuyen en mayor medida a la audiencia direccionable. Puede utilizar este informe para identificar qué [!DNL ExperienceEvent] conjuntos de datos para establecer un TTL. Consulte el tutorial en [generación del informe de superposición de conjuntos de datos](../../profile/tutorials/dataset-overlap-report.md) para obtener más información.
* **API de informe de superposición de identidad**: Expone los espacios de nombres de identidad que contribuyen en mayor medida a la audiencia direccionable. Consulte el tutorial en [generación del informe de superposición de identidad](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) para obtener más información.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### [!DNL ExperienceEvent] TTL de conjunto de datos {#dataset-ttl}

Puede aplicar TTL a conjuntos de datos habilitados para perfiles para eliminar datos de comportamiento del Almacenamiento de perfiles que ya no sean útiles para sus casos de uso. Una vez que el TTL se aplica a un conjunto de datos habilitado para el perfil, Platform elimina automáticamente los datos que ya no son necesarios mediante un proceso de dos partes:

* Todos los datos nuevos que avancen tendrán el valor de caducidad del TTL aplicado en el momento de la ingesta;
* Todos los datos existentes tendrán el valor de caducidad de TTL aplicado como parte de un trabajo de sistema de relleno de una sola vez.

Puede esperar que el valor TTL de cada evento pertenezca a la marca de tiempo del evento. Todos los eventos anteriores al valor de caducidad del TTL se pierden inmediatamente cuando se ejecuta el trabajo del sistema. Todos los demás eventos se pierden a medida que se acercan al valor de caducidad del TTL designado en la marca de tiempo del evento.

Consulte el siguiente ejemplo para comprender mejor [!DNL ExperienceEvent] TTL de conjunto de datos.

Si aplica un valor TTL de 30 días el 15 de mayo, entonces:

* Todos los eventos nuevos tendrán un TTL de 30 días aplicados a medida que entren;
* Un trabajo del sistema elimina inmediatamente todos los eventos existentes que tengan una marca de tiempo anterior al 15 de abril.;
* Los eventos que tengan una marca de tiempo después del 15 de abril obtendrán una marca de tiempo de su evento + días TTL. Por lo tanto, un evento con una marca de tiempo del 18 de abril, dejará de celebrarse tres días después del 15 de mayo.

>[!IMPORTANT]
>
>Una vez aplicado un TTL, cualquier dato anterior al número de días TTL seleccionado será **permanentemente** y no se pueden restaurar.

Antes de aplicar TTL, debe asegurarse de mantener una ventana retrospectiva de cualquier segmento dentro del límite TTL. De lo contrario, los resultados del segmento pueden ser incorrectos después de aplicar TTL. Por ejemplo, si ha aplicado un TTL de 30 días para los datos de Adobe Analytics y un TTL de 365 días para los datos de Transacciones en el almacén, el siguiente segmento creará resultados incorrectos:

* Página de producto visualizada en los últimos 60 días seguida de una compra en la tienda;
* Agregue al carro seguido de no comprar en los últimos 60 días.

Por el contrario, lo siguiente seguirá creando resultados correctos:

* Página de producto vista en los últimos 14 días seguida de una compra en la tienda;
* Visualizó una página de ayuda específica en línea en los últimos 30 días;
* Compró un producto sin conexión en los últimos 120 días;
* Se agrega al carro de compras seguido de una compra en los últimos 14 días.

>[!TIP]
>
>Para su comodidad, puede mantener el mismo TTL para todos los conjuntos de datos, de modo que no tenga que preocuparse por el impacto del TTL en todos los conjuntos de datos en la lógica de segmentación.

Para obtener más información sobre la aplicación de TTL a los datos de perfil, consulte la documentación de [TTL de servicio de perfil](../../profile/apply-ttl.md).

## Resumen de las prácticas recomendadas para el cumplimiento de las normas de uso de licencias {#best-practices}

A continuación se ofrece una lista de algunas prácticas recomendadas que puede seguir para garantizar un mejor cumplimiento de su derecho de uso de licencia:

* Utilice la variable [panel de uso de licencias](../../dashboards/guides/license-usage.md) para realizar un seguimiento y monitorizar las tendencias de uso de los clientes. Esto le permite adelantarse a cualquier posible sobrecarga que pueda incurrir.
* Configurar [filtros de ingesta](#ingestion-filters) identificando los eventos necesarios para sus casos de uso de segmentación y personalización. Esto le permite enviar solo los eventos importantes necesarios para sus casos de uso.
* Asegúrese de que solo tiene [conjuntos de datos habilitados para perfil](#ingestion-filters) que son necesarios para los casos de uso de segmentación y personalización.
* Configure un [[!DNL ExperienceEvent] TTL de conjunto de datos](#dataset-ttl) para datos de alta frecuencia como datos web.
* Compruebe periódicamente el [Informes de composición de perfil](#profile-store-composition-reports) para comprender la composición de la tienda de perfiles. Esto le permite comprender las fuentes de datos que más contribuyen al consumo de licencias.

## Resumen de características y disponibilidad {#feature-summary}

Las prácticas recomendadas y las herramientas descritas en este documento le ayudarán a administrar mejor el uso de las autorizaciones de licencia en Adobe Experience Platform. Este documento se actualizará a medida que se lancen funciones adicionales para ayudar a proporcionar visibilidad y control a todos los clientes Experience Platform.

La siguiente tabla describe la lista de funciones disponibles actualmente a su disposición para administrar mejor su derecho de uso de licencias.

| Función | Descripción |
| --- | --- |
| [Habilitar/deshabilitar conjuntos de datos para perfil](../../catalog/datasets/user-guide.md) | Habilitar o deshabilitar la incorporación de conjuntos de datos en el servicio de perfil |
| [!DNL ExperienceEvent] TTL de conjunto de datos | Aplique una caducidad de TTL para conjuntos de datos de comportamiento en el Almacenamiento de perfiles. Póngase en contacto con su representante de asistencia al Adobe. |
| [Filtros de preparación de datos de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Aplicar [!DNL Kafka] filtros para excluir los datos innecesarios de la ingesta |
| [Filtros del conector de origen de Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Aplicar filtros de conexión de origen de Audience Manager para excluir de la ingesta datos innecesarios |
| [Aplicar filtros de datos SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Aplicar filtros de aleación para excluir los datos innecesarios de la ingesta |
| [Filtros de datos del reenvío de eventos](../../tags/ui/event-forwarding/overview.md) | Aplicar del lado del servidor [!DNL Kafka] filtros para excluir los datos innecesarios de la ingesta.  Consulte la documentación sobre [reglas de etiqueta](../../tags/ui/managing-resources/rules.md) para obtener más información. |
| [Interfaz de usuario del panel Uso de licencias](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Ver una instantánea de los datos relacionados con las licencias de su organización para el Experience Platform |
| [API de informe de superposición de conjunto de datos](../../profile/tutorials/dataset-overlap-report.md) | Genera conjuntos de datos que contribuyen en mayor medida a la audiencia direccionable |
| [API de informe de superposición de identidad](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Genera los espacios de nombres de identidad que contribuyen en mayor medida a la audiencia direccionable |

{style=&quot;table-layout:auto&quot;}
