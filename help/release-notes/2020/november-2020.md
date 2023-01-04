---
title: Notas de la versión de Adobe Experience Platform, noviembre de 2020
description: Notas de la versión de noviembre de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de noviembre de 2020**

Nuevas funciones de Adobe Experience Platform:

- [Migración de Data Lake de Adobe Experience Platform](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Actualizaciones de funciones existentes:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Service](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migración de Data Lake de Adobe Experience Platform {#migration}

Mientras el Adobe migra el lago de datos de Gen1 a Gen2, los usuarios podrán leer desde el lago de datos, pero todas las funcionalidades que escriban en el lago de datos se verán afectadas. El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración para organizaciones específicas de IMS.

Para obtener más información, lea la [Guía de migración del lago de datos](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aprovecha [Adobe Admin Console](https://adminconsole.adobe.com) perfiles de producto para vincular usuarios con permisos y entornos limitados. Los permisos controlan el acceso a una variedad de funcionalidades de Platform, que incluyen modelado de datos, administración de perfiles y administración de entornos limitados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Permisos | En el [!DNL Admin Console], la pestaña dentro de un [!DNL Platform] perfil de producto le permite personalizar cuál [!DNL Platform] están disponibles para los usuarios adjuntos a ese perfil. Las categorías de permisos disponibles incluyen: **[!UICONTROL Modelado de datos]**, **[!UICONTROL Gestión de datos]**, **[!UICONTROL Administración de perfiles]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Supervisión de datos]**, **[!UICONTROL Administración de Simuladores para pruebas]**, **[!UICONTROL Destinos]**, **[!UICONTROL Ingesta de datos]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Servicio de consultas]** y **[!UICONTROL Administración de datos]**. |
| Acceso a entornos limitados | La variable **[!UICONTROL Permisos]** dentro de un [!DNL Platform] el perfil de producto puede otorgar a los usuarios acceso a entornos limitados específicos. Consulte la sección sobre [entornos limitados](#sandboxes) más abajo para obtener más información. |

Para obtener más información, consulte la [información general sobre el control de acceso](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] es un servicio de aplicaciones integrado con [!DNL Experience Platform]. Le permite aprovechar [!DNL Platform] para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto en el momento adecuado.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | Interfaz donde se crean y administran los diferentes elementos que componen las ofertas y se definen sus reglas y restricciones. |
| Motor de decisión de oferta | El motor de decisión de oferta aprovecha [!DNL Platform] datos y [!DNL Real-Time Customer Profiles], junto con la Biblioteca de ofertas, para seleccionar la hora, los clientes y los canales adecuados a los que se enviarán las ofertas. |

Para obtener más información, consulte la [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=es) documentación.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. A menudo, las empresas ejecutan varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, asegurando al mismo tiempo el cumplimiento de las normas operacionales. Para hacer frente a esta necesidad, [!DNL Experience Platform] proporciona entornos limitados que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Espacio aislado de producción | [!DNL Experience Platform] proporciona un único simulador para pruebas de producción, que no se puede eliminar ni restablecer. El número total de entornos limitados disponibles, producción y no producción, viene determinado por la licencia adquirida. |
| Entornos limitados que no sean de producción | Se pueden crear varios entornos limitados que no sean de producción para un único [!DNL Platform] , lo que le permite probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno limitado de producción. |
| Conmutador de espacio aislado | En el [!DNL Experience Platform] interfaz de usuario, el conmutador de simulador de pruebas en la esquina superior izquierda de la pantalla le permite cambiar entre entornos limitados disponibles mediante un menú desplegable. El conmutador de simulador de pruebas también proporciona una función de búsqueda que le permite filtrar por los entornos limitados disponibles. |
| `x-sandbox-name` header | Todas las llamadas a [!DNL Experience Platform] Las API ahora deben incluir el nuevo `x-sandbox-name` encabezado, cuyo valor hace referencia a la variable `name` del simulador de pruebas en el que se llevará a cabo la operación. |

Para obtener más información, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Operaciones iterativas | [!DNL Data Prep] Mapper ahora es compatible con la realización de operaciones iterativas en una jerarquía. |
| Función de asignador | [!DNL Data Prep] Mapper ahora tiene la capacidad de **not** copie un atributo del origen al XDM de destino. |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe. Una de las formas en que Data Science Workspace lo consigue es mediante el uso de [!DNL JupyterLab]. [!DNL JupyterLab] es una interfaz de usuario basada en web para [[!DNL Project Jupyter]](https://jupyter.org/) y está estrechamente integrado en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo con el que los científicos de datos pueden trabajar [!DNL Jupyter] portátiles, código y datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| [!DNL JupyterLab] Plantilla de generador de fórmulas | El uso de los requisitos de las fórmulas y las versiones actualizadas del bloc de notas. [!DNL Python] La imagen base del tiempo de ejecución de ML se ha actualizado para su uso [!DNL Python] 3.6.7 y [!DNL Conda] entorno exclusivamente. |

Para obtener más información, lea el documento sobre [crear una fórmula utilizando Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Service {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| Brazo | Braze es una completa plataforma de participación del cliente que ofrece experiencias relevantes e inolvidables entre los clientes y las marcas que les encantan. |
| Microsoft Bing | El destino de Microsoft Bing le ayuda a ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en toda la publicidad de presentación de Microsoft. |
| El mostrador de comercio | Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de redireccionamiento y segmentación de audiencia en distintas fuentes de inventario de dispositivos móviles, vídeo y visualización. |

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Detalles de destino Actualizaciones de experiencia de usuario | El flujo de trabajo de destino de Real-Time CDP ahora incluye supervisión en línea para que pueda ver qué activaciones por lotes se realizaron correctamente. Esta función permite a los usuarios resolver problemas directamente en el flujo de trabajo para los destinos de lote mediante alertas y un panel de monitorización para rastrear errores en la canalización de procesamiento. |
| Cifrado de archivos | Para los destinos basados en archivos, los usuarios ahora pueden agregar cifrado a sus archivos exportados. |
| Programación de archivos | Para destinos de almacenamiento en la nube y basados en correo electrónico, los usuarios pueden crear una exportación única o crear instantáneas diarias. |
| Campos obligatorios | Los usuarios pueden marcar los campos como obligatorios, lo que garantiza que solo se exporten los campos que contienen el campo obligatorio. |

Para obtener más información, consulte la [Información general sobre destinos](../../destinations/home.md).

## Servicios inteligentes {#intelligent-services}

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en los casos de uso de experiencias del cliente. Esto permite que los analistas de marketing configuren predicciones específicas de las necesidades de una empresa mediante configuraciones de nivel empresarial sin necesidad de experiencia en ciencia de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Conjunto de datos de Eventos de experiencias del consumidor (CEE) | La creación de un conjunto de datos CEE ahora admite la adición de campos de identidad al conjunto de datos con el Editor de esquemas. Attribution AI y Customer AI utilizan la identidad principal para combinar eventos. |

Para obtener más información, consulte la sección sobre [adición de campos de identidad a un conjunto de datos](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) en la guía de preparación de datos de servicios inteligentes.

### Inteligencia artificial aplicada a la atribución

Attribution AI, como parte de Servicios inteligentes es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de la fuente de datos | El vínculo al origen del conjunto de datos original se puede ver y navegar hasta desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Ahora puede modificar el nombre de una instancia de Attribution AI existente. |
| Clonar instancia | Copia la configuración de la instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Modificación de los parámetros de configuración de instancias | Ahora puede modificar la configuración de una instancia de Attribution AI existente si aún no ha empezado a puntuar. |
| Una de las calificaciones | Ahora puede almacenar en déclencheur la puntuación de modelos ad hoc en las instancias de Attribution AI. |
| Pasar columnas | Ahora puede configurar columnas adicionales que se agregarán a los archivos de puntuación de salida sin procesar para agregar dimensiones adicionales a las vistas de herramientas de BI. |
| Activación y desactivación de instancias | Ahora puede activar y desactivar la formación y puntuación del modelo programado de las instancias de Attribution AI. |
| Seguimiento de derechos | Puede encontrar la cantidad total de perspectivas de atribución consumidas por su cuenta en el contenedor de creación de instancias. |
| Desglose de puntos de contacto por posición | Un nuevo gráfico de perspectivas que proporciona un análisis de los puntos de contacto por las posiciones de las rutas de conversión. |
| Rutas de conversión principales | Un nuevo gráfico de perspectivas ubicado en la pestaña Análisis de rutas . El gráfico contiene una lista de las cinco rutas de conversión principales que muestran la secuencia de puntos de contacto del canal de marketing que generaron la mayoría de las conversiones. |
| Eficacia de los puntos de contacto | Proporciona una visión detallada de las tres variables más importantes por las que su modelo mide la eficacia del punto de contacto. Las variables son la proporción de rutas positivas y negativas afectadas, la eficiencia de los puntos de contacto y el volumen de los puntos de contacto. |

Para obtener más información, lea la [Información general sobre la Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

Customer AI, como parte de Servicios inteligentes, proporciona a los especialistas en marketing la capacidad de generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, la inteligencia artificial aplicada al cliente puede indicarle qué es lo más probable que haga un cliente y por qué. Además, los expertos en marketing pueden beneficiarse de las predicciones y perspectivas de la inteligencia artificial aplicada al cliente para personalizar las experiencias de los clientes y ofrecerles las ofertas y los mensajes más adecuados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de la fuente de datos | El vínculo al origen del conjunto de datos original se puede ver y navegar hasta desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Puede modificar el nombre de una instancia de Customer AI existente. |
| Modificación de los parámetros de configuración de instancias | Ahora puede modificar la configuración de una instancia de Customer AI existente si aún no ha comenzado una puntuación. |
| Clonar instancia | Copia la configuración de la instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Seguimiento de derechos | Puede encontrar la cantidad total de perfiles calificados por Customer AI para su cuenta en el contenedor crear instancia . |
| Objetivo de predicción | La flexibilidad para crear un objetivo de predicción se ha incrementado con nuevas opciones para predecir si algo &quot;ocurrirá&quot; o &quot;no ocurrirá&quot;. Además, se han añadido las opciones para predecir si &quot;todos&quot; los eventos se producen o &quot;cualquiera de&quot; los eventos se producen cuando se utilizan varios eventos. |
| Desglose de factores influyentes | Los bloques de factores influyentes principales de propensión ahora contienen desgloses. Los desgloses son un resumen a nivel más profundo de los valores para cada uno de los factores de mayor influencia dentro de un bloque de propensión. |

Para obtener más información, lea la [Información general sobre Customer AI](../../intelligent-services/customer-ai/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus diferentes datos de clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Flujo de trabajo actualizado de directivas de combinación | Platform ha actualizado la configuración de la directiva de combinación a un nuevo flujo de trabajo por etapas. Este flujo de trabajo permite a los usuarios agrupar fragmentos de datos de varios conjuntos de datos de perfil y establecer la prioridad para cómo se combinan los datos en dichos conjuntos de datos para crear una vista completa de cada individuo. Los usuarios pueden combinar los conjuntos de datos de perfil individuales XDM seleccionados seleccionando el método de combinación apropiado (marca de tiempo ordenada o prioridad de conjunto de datos) y anexando conjuntos de datos de ExperienceEvent a los conjuntos de datos de perfil. |
| Vista de esquema de unión | En la interfaz de usuario del Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad de solucionar problemas y validar que los perfiles están correctamente configurados, que las identidades se vinculan correctamente y que los datos se han introducido correctamente. |

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] información, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas fuentes**

| Función | Descripción |
| ------- | ----------- |
| [!DNL Shopify] | Ahora puede conectarse [!DNL Shopify] a [!DNL Experience Platform] usando la variable [!DNL Flow Service] o la interfaz de usuario. Consulte la [Resumen del conector de Shopify](../../sources/connectors/ecommerce/shopify.md) para obtener más información. |

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualización de la información de conexión | Ahora puede actualizar los nombres, las descripciones y las credenciales de las conexiones por lotes existentes mediante la función [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [actualización de conexiones mediante la API de servicio de flujo](../../sources/tutorials/api/update.md) y [edición de los detalles de la cuenta mediante la interfaz de usuario](../../sources/tutorials/ui/monitor.md). |
| Eliminación de conexiones | Las conexiones por lotes que contienen errores o que se han vuelto innecesarias ahora se pueden eliminar mediante la función [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [eliminación de conexiones mediante la API de servicio de flujo](../../sources/tutorials/api/delete.md) y [eliminación de cuentas mediante la interfaz de usuario](../../sources/tutorials/ui/delete-accounts.md). |
| Asignación jerárquica | Puede obtener una vista previa de un archivo de origen jerárquico, como JSON o Parquet, durante el proceso de ingesta de datos. Consulte el tutorial en [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información. |
| Compatibilidad de API para la asignación en fuentes de flujo continuo | Ahora puede utilizar API para realizar funciones de asignación con fuentes de flujo continuo. |
| Compatibilidad de API con delimitadores personalizados para fuentes de almacenamiento en la nube | Ahora puede recopilar archivos no delimitados por CSV mediante fuentes de almacenamiento en la nube. Puede utilizar cualquier delimitador de una sola columna, como una tabulación, una coma, una barra vertical, un punto y coma o un hash, para recopilar archivos planos en cualquier formato. |
| Compatibilidad con Sandbox para el conector Adobe Audience Manager | El conector del Audience Manager ahora reconoce el simulador de pruebas. Los usuarios pueden habilitar el conector para enrutar conjuntos de datos de Audience Manager al entorno limitado que elijan (incluidos entornos limitados que no sean de producción). La configuración está limitada a un simulador para pruebas por cada organización de IMS. |
| Mejoras en la experiencia de usuario | Ahora se puede acceder a la ingesta basada en archivos a través del catálogo de fuentes. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
