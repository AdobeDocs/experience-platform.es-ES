---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 11 de noviembre de 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 5ff73aa1745e78f0026ada2c66908888be5f4498
workflow-type: tm+mt
source-wordcount: '2086'
ht-degree: 3%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de noviembre de 2020**

Nuevas funciones de Adobe Experience Platform:

- [Migración a Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Actualizaciones de funciones existentes:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Service](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migración a Adobe Experience Platform Data Lake {#migration}

Mientras que Adobe está migrando el Data Lake de Gen1 a Gen2, los usuarios podrán leer desde Data Lake, pero todas las capacidades que escriban en Data Lake se verán afectadas. El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración para las organizaciones de IMS específicas.

Para obtener más información, lea la guía [de migración de](../../landing/adls2-gen2-migration.md)Data Lake.

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aprovecha los perfiles de productos de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a los usuarios con permisos y entornos limitados. Los permisos controlan el acceso a una variedad de funciones de la Plataforma, incluyendo modelado de datos, administración de perfiles y administración de simuladores de pruebas.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Permisos | En la ficha [!DNL Admin Console], dentro de un perfil de [!DNL Platform] producto, puede personalizar [!DNL Platform] las funciones disponibles para los usuarios conectados a ese perfil. Las categorías de permisos disponibles incluyen: **[!UICONTROL Modelado]** de datos, **[!UICONTROL Gestión de datos]**, Administración **[!UICONTROL de]** Perfiles, **[!UICONTROL Identity Management]**, Monitoreo **[!UICONTROL de]** datos, Administración de ************************ Simuladores, Destinaciones, Ingestión de datos,Servicio de Consulta, Gobierno de Datos. |
| Acceso a los entornos limitados | La ficha **[!UICONTROL Permisos]** de un perfil [!DNL Platform] de producto puede otorgar a los usuarios acceso a entornos limitados específicos. Para obtener más información, consulte la sección sobre [entornos](#sandboxes) limitados más abajo. |

Para obtener más información, consulte la descripción general [del](../../access-control/home.md)control de acceso.

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] es un servicio de aplicaciones integrado con [!DNL Experience Platform]. Le permite aprovechar [!DNL Platform] para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto en el momento adecuado.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | Interfaz en la que se crean y administran los distintos elementos que componen las ofertas y se definen sus reglas y restricciones. |
| Motor de decisión de oferta | El motor de decisión de Oferta aprovecha [!DNL Platform] los datos y [!DNL Real-time Customer Profiles], junto con la biblioteca de Ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas. |

Para obtener más información, consulte la [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentación.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. Las compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales. Para satisfacer esta necesidad, [!DNL Experience Platform] proporciona entornos limitados que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Simulador de pruebas de producción | [!DNL Experience Platform] proporciona un solo entorno limitado de producción, que no se puede eliminar ni restablecer. El número total de zonas protegidas disponibles, producción y no producción, viene determinado por la licencia adquirida. |
| Entornos limitados que no son de producción | Se pueden crear varios entornos limitados que no sean de producción para una sola [!DNL Platform] instancia, lo que permite probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. |
| Mezclador de Simulador para pruebas | En la interfaz de usuario, el conmutador de simulador de pruebas situado en la esquina superior izquierda de la pantalla permite cambiar entre los entornos limitados disponibles mediante un menú desplegable. [!DNL Experience Platform] El conmutador de simulador de pruebas también proporciona una función de búsqueda que le permite filtrar por los entornos limitados disponibles. |
| `x-sandbox-name` header | Todas las llamadas a [!DNL Experience Platform] las API deben ahora incluir el nuevo `x-sandbox-name` encabezado, cuyo valor hace referencia al `name` atributo del simulador para pruebas en el que tendrá lugar la operación. |

Para obtener más información, consulte la descripción general [de los](../../sandboxes/home.md)entornos limitados.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Operaciones iterativas | [!DNL Data Prep] Mapper ahora admite operaciones iterativas en una jerarquía. |
| Mapper, función | [!DNL Data Prep] Mapper ahora tiene la capacidad de **no** copiar un atributo del origen en el destinatario XDM. |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de los datos. Integrado en Adobe Experience Platform, Área de trabajo de ciencia de datos le ayuda a realizar predicciones con sus recursos de contenido y datos en las soluciones de Adobe. Una de las formas en que el Área de trabajo de ciencia de datos lo logra es mediante el uso de [!DNL JupyterLab]. [!DNL JupyterLab] es una interfaz de usuario basada en web para [[!DNL Project Jupyter]](https://jupyter.org/) y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con [!DNL Jupyter] portátiles, código y datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| [!DNL JupyterLab] Plantilla del Generador de fórmulas | Actualización del uso de los requisitos de fórmula para portátiles y de las versiones. [!DNL Python] La imagen base de ML Runtime se ha actualizado para usar [!DNL Python] 3.6.7 y un [!DNL Conda] entorno exclusivamente. |

Para obtener más información, lea el documento sobre la [creación de una fórmula con portátiles](../../data-science-workspace/jupyterlab/create-a-recipe.md)Jupyter.

## [!DNL Destinations] Service {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| Microsoft Bing | El destino de Microsoft Bing le ayuda a ejecutar campañas digitales de objetivo de redireccionamiento y audiencia en toda la publicidad de presentación de Microsoft. |
| La Oficina de Comercio | Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de objetivo de redireccionamiento y audiencia en distintas fuentes de inventario móviles, de vídeo y de visualización. |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Campos obligatorios | Los usuarios pueden marcar los campos como obligatorios, asegurándose de que solo se exporten los campos que contengan el campo obligatorio. |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

Para obtener más información, consulte la información general sobre [los destinos](../../rtcdp/destinations/destinations-overview.md).

## Servicios inteligentes {#intelligent-services}

Los servicios inteligentes potencian a los analistas de marketing y a los profesionales para que aprovechen el poder de la inteligencia artificial y el aprendizaje automático en casos de uso de la experiencia del cliente. Esto permite que los analistas de mercadotecnia configuren predicciones específicas de las necesidades de una compañía mediante configuraciones de nivel empresarial sin necesidad de conocimientos de ciencia de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Conjunto de datos de Eventos de experiencias del consumidor (CEE) | La creación de un conjunto de datos CEE ahora admite la adición de campos de identidad al conjunto de datos con el Editor de Esquemas. Los archivos AI de Attribution AI y cliente utilizan la identidad principal para combinar eventos. |

Para obtener más información, lea la sección sobre [adición de campos de identidad a un conjunto de datos](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) en la guía de preparación de datos de Servicios inteligentes.

### Attribution AI

Attribution AI, como parte de Servicios Inteligentes, es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de fuente de datos | El vínculo al origen del conjunto de datos original puede verse y navegarse desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Ahora puede modificar el nombre de una instancia de Attribution AI existente. |
| Clonar instancia | Copia la configuración de instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Modificar parámetros de configuración de instancia | Ahora puede modificar la configuración de una instancia de Attribution AI existente si aún no ha empezado a marcar. |
| Una de las puntuaciones | Ahora puede activar una puntuación de modelo ad-hoc en las instancias de Attribution AI. |
| Pasar columnas | Ahora puede configurar columnas adicionales que se agregarán a los archivos de puntuación de salida sin procesar para agregar dimensiones adicionales a las vistas de herramientas de BI. |
| Activación y desactivación de instancias | Ahora puede activar y desactivar la formación y puntuación del modelo programado de las instancias de Attribution AI. |
| Seguimiento de asignación de derechos | Puede encontrar la cantidad total de perspectivas de atribución consumidas por su cuenta en el contenedor de creación de instancias. |
| Desglose de puntos de contacto por posición | Un nuevo gráfico de perspectivas que proporciona una análisis de puntos de contacto según las posiciones de las rutas de conversión. |
| Rutas de conversión principales | Un nuevo gráfico de perspectivas ubicado en la ficha Análisis de ruta. El gráfico contiene una lista de las cinco rutas de conversión principales que muestra la secuencia de puntos de contacto de canales de marketing que produjeron la mayor cantidad de conversiones. |
| Eficacia de Touchpoint | Proporciona perspectivas detalladas de las tres variables más importantes por las que el modelo mide la eficacia del punto de contacto. Las variables son la proporción de rutas positivas y negativas tocadas, la eficiencia del punto de contacto y el volumen del punto de contacto. |

Para obtener más información, lea la descripción general de la [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### AI del cliente

La API del cliente, como parte de Servicios inteligentes, proporciona a los especialistas en marketing la capacidad de generar predicciones de clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, la información sobre el cliente puede indicarle qué es lo que probablemente hará un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de la API del cliente para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de fuente de datos | El vínculo al origen del conjunto de datos original puede verse y navegarse desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Puede modificar el nombre de una instancia de AI de cliente existente. |
| Modificar parámetros de configuración de instancia | Ahora puede modificar la configuración de una instancia de AI de cliente existente si aún no ha comenzado a realizar una puntuación. |
| Clonar instancia | Copia la configuración de instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Seguimiento de asignación de derechos | Puede encontrar la cantidad total de perfiles puntuados por la API del cliente para su cuenta en el contenedor de creación de instancias. |
| Objetivo de predicción | La flexibilidad en la creación de un objetivo de predicción se ha incrementado con nuevas opciones para predecir si algo &quot;ocurrirá&quot; o &quot;no ocurrirá&quot;. Además, se han agregado las opciones para predecir si &quot;todos&quot; los eventos se producen o &quot;cualquiera de&quot; los eventos cuando se utilizan varios eventos. |
| Exploración influyente del factor | Los bloques de factores influyentes superiores de tendencia ahora contienen desgloses. Los desgloses son un resumen de nivel más profundo de los valores para cada uno de los factores de mayor influencia dentro de un bloque de propensión. |

Para obtener más información, lea la descripción general [de AI del](../../intelligent-services/customer-ai/overview.md)cliente.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Flujo de trabajo de directivas de combinación actualizado | Platform ha actualizado la configuración de directiva de combinación a un nuevo flujo de trabajo por etapas. Este flujo de trabajo permite a los usuarios reunir fragmentos de datos de varios conjuntos de datos de Perfil y establecer la prioridad para combinar los datos en dichos conjuntos de datos a fin de crear una vista completa de cada individuo. Los usuarios pueden combinar conjuntos de datos de Perfiles individuales XDM seleccionados seleccionando el método de combinación adecuado (marca de tiempo ordenada o prioridad de conjunto de datos) y agregando conjuntos de datos de ExperienceEvent a los conjuntos de datos de Perfil. |
| Vista de esquema de unión | En la interfaz de usuario del Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como campos de identidad y relación. Estas actualizaciones mejoran la capacidad para solucionar problemas y validar que los perfiles estén correctamente configurados, que las identidades estén correctamente vinculadas y que los datos se hayan ingerido correctamente. |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] datos, lea la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas fuentes**
| Función | Descripción |
| — | — |
| [!DNL Shopify] | Ahora puede conectarse [!DNL Shopify] a [!DNL Experience Platform] mediante la [!DNL Flow Service] API o la interfaz de usuario. Consulte la descripción general [del conector](../../sources/connectors/ecommerce/shopify.md) Shopify para obtener más información. |

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualizar información de conexión | Ahora puede actualizar los nombres, las descripciones y las credenciales de las conexiones por lotes existentes mediante la [!DNL Flow Service] API y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre la [actualización de conexiones mediante la API](../../sources/tutorials/api/update.md) de servicio de flujo y la [edición de los detalles de la cuenta mediante la interfaz de usuario](../../sources/tutorials/ui/monitor.md). |
| Eliminar conexiones | Las conexiones por lotes que contienen errores o que se han vuelto innecesarias ahora se pueden eliminar mediante la API y la interfaz [!DNL Flow Service] de usuario. Para obtener más información, consulte el tutorial sobre la [eliminación de conexiones mediante la API](../../sources/tutorials/api/delete.md) de servicio de flujo y la [eliminación de cuentas mediante la interfaz de usuario](../../sources/tutorials/ui/delete-accounts.md). |
| Asignación jerárquica | Durante el proceso de ingestión de datos, puede realizar la previsualización de un archivo de origen jerárquico, como JSON o Parquet. Consulte el tutorial sobre la [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información. |
| Compatibilidad de API con la asignación en fuentes de flujo continuo | Ahora puede utilizar API para realizar funciones de asignación con fuentes de flujo continuo. |
| Compatibilidad de API con delimitadores personalizados para orígenes de almacenamiento en la nube | Ahora puede recopilar archivos no delimitados por CSV mediante fuentes de almacenamiento en la nube. Puede utilizar cualquier delimitador de una sola columna, como una ficha, una coma, una barra vertical, un punto y coma o un hash, para recopilar archivos planos en cualquier formato. El valor predeterminado es una coma si no se proporciona. |
| Compatibilidad de Simulador para pruebas con el conector Adobe Audience Manager | El conector del Audience Manager ahora es compatible con el simulador de pruebas. Los usuarios pueden habilitar el conector para enrutar conjuntos de datos de Audience Manager al simulador para pruebas de su elección (incluidos los entornos limitados que no sean de producción). La configuración está limitada a un simulador para pruebas por organización IMS. |
| Mejoras en los recursos | Ahora se puede acceder a la ingestión basada en archivos a través del catálogo de fuentes. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.