---
title: Notas de la versión de Adobe Experience Platform, noviembre de 2020
description: Notas de la versión de noviembre de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 11 de noviembre de 2020**

Nuevas funciones de Adobe Experience Platform:

- [Migración de Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Actualizaciones de funciones existentes:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [Servicio [!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migración de Adobe Experience Platform Data Lake {#migration}

Mientras el Adobe migra el lago de datos de Gen1 a Gen2, los usuarios podrán leer del lago de datos, pero todas las capacidades que escriben en él se verán afectadas. El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y para confirmar las fechas y horas de migración de organizaciones específicas.

Para obtener más información, lea la [Guía de migración de Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aprovecha los perfiles de producto de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a usuarios con permisos y zonas protegidas. Los permisos controlan el acceso a una variedad de funcionalidades de Platform, incluido el modelado de datos, la administración de perfiles y la administración de zonas protegidas.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Permisos | En [!DNL Admin Console], la ficha dentro de un perfil de producto de [!DNL Platform] le permite personalizar qué capacidades de [!DNL Platform] están disponibles para los usuarios adjuntos a ese perfil. Las categorías de permisos disponibles incluyen: **[!UICONTROL Modelado de datos]**, **[!UICONTROL Administración de datos]**, **[!UICONTROL Administración de perfiles]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Supervisión de datos]**, **[!UICONTROL Administración de espacio aislado]**, **[!UICONTROL Destinos]**, **[!UICONTROL Ingesta de datos]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Servicio de consultas]** y **[!UICONTROL Gobernanza de datos]**. |
| Acceso a zonas protegidas | La ficha **[!UICONTROL Permisos]** dentro de un perfil de producto de [!DNL Platform] puede otorgar a los usuarios acceso a zonas protegidas específicas. Consulte la sección sobre [zonas protegidas](#sandboxes) más abajo para obtener más información. |

Para obtener más información, consulte la [descripción general del control de acceso](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] es un servicio de aplicaciones integrado con [!DNL Experience Platform]. Le permite aprovechar [!DNL Platform] para ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | Interfaz en la que se crean y administran los diferentes elementos que componen las ofertas y se definen sus reglas y restricciones. |
| Motor de decisión de ofertas | El Motor de decisión de ofertas aprovecha los datos de [!DNL Platform] y [!DNL Real-Time Customer Profiles], junto con la Biblioteca de ofertas, para seleccionar el momento, los clientes y los canales adecuados a los que se enviarán las ofertas. |

Para obtener más información, consulte la documentación de [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=es).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] se ha creado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para resolver esta necesidad, [!DNL Experience Platform] proporciona zonas protegidas que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar aplicaciones de experiencia digital y hacer que evolucionen.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Zona protegida de producción | [!DNL Experience Platform] proporciona una sola zona protegida de producción, que no se puede eliminar ni restablecer. El número total de zonas protegidas disponibles, producción y no producción, viene determinado por la licencia adquirida. |
| Zonas protegidas de no producción | Se pueden crear varias zonas protegidas que no sean de producción para una sola instancia de [!DNL Platform], lo que le permite probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a la zona protegida de producción. |
| Conmutador de zona protegida | En la interfaz de usuario [!DNL Experience Platform], el conmutador de zona protegida en la esquina superior izquierda de la pantalla le permite cambiar entre las zonas protegidas disponibles mediante un menú desplegable. El conmutador de zonas protegidas también proporciona una función de búsqueda que le permite filtrar las zonas protegidas disponibles. |
| `x-sandbox-name` encabezado | Todas las llamadas a las API [!DNL Experience Platform] deben incluir ahora el nuevo encabezado `x-sandbox-name`, cuyo valor hace referencia al atributo `name` de la zona protegida en la que se realizará la operación. |

Para obtener más información, consulte la [descripción general de las zonas protegidas](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Operaciones iterativas | El asignador [!DNL Data Prep] ahora admite realizar operaciones iterativas en una jerarquía. |
| Función asignador | El asignador [!DNL Data Prep] ahora tiene la capacidad de **no** copiar un atributo del origen al XDM de destino. |

Para obtener más información, consulte [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utiliza aprendizaje automático e inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando su contenido y sus recursos de datos en soluciones de Adobe. Una de las formas en que Data Science Workspace logra esto es mediante el uso de [!DNL JupyterLab]. [!DNL JupyterLab] es una interfaz de usuario basada en web para [[!DNL Project Jupyter]](https://jupyter.org/) y está totalmente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con [!DNL Jupyter] blocs de notas, código y datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| [!DNL JupyterLab] plantilla del Generador de fórmulas | Se han actualizado el portátil con los requisitos de fórmula, uso y versiones. La imagen base de tiempo de ejecución de [!DNL Python] ML se ha actualizado para utilizar [!DNL Python] 3.6.7 y un entorno de [!DNL Conda] exclusivamente. |

Para obtener más información, lea el documento sobre [creación de una fórmula con Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## Servicio [!DNL Destinations] {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera perfecta.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| Soldar | Braze es una plataforma completa de participación del cliente que potencia experiencias relevantes y memorables entre los clientes y las marcas que aman. |
| Microsoft Bing | El destino de Microsoft Bing le ayuda a ejecutar campañas digitales de retargeting y segmentación de audiencia en Microsoft Display Advertising. |
| La Oficina de Comercio | Trade Desk es una plataforma de autoservicio para que los compradores de anuncios puedan ejecutar campañas digitales de retargeting y segmentación de audiencia en pantallas, vídeos y fuentes de inventario móviles. |

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Detalles del destino Actualizaciones de UX | El flujo de trabajo de destino de Real-Time CDP ahora incluye la monitorización en línea para que pueda ver qué activaciones por lotes se realizaron correctamente. Esta función permitirá a los usuarios resolver problemas directamente en el flujo de trabajo para destinos por lotes mediante alertas y un panel de monitorización para rastrear errores en la canalización de procesamiento. |
| Cifrado de archivos | Para los destinos basados en archivos, los usuarios ahora pueden agregar cifrado a sus archivos exportados. |
| Programación de archivos | Tanto para los destinos de almacenamiento basados en correo electrónico como para los de almacenamiento en la nube, los usuarios pueden crear una exportación única o instantáneas diarias. |
| Campos obligatorios | Los usuarios pueden marcar los campos como obligatorios, asegurándose de que solo se exportan los campos que contienen el campo obligatorio. |

Para obtener más información, consulte [Información general sobre destinos](../../destinations/home.md).

## Servicios inteligentes {#intelligent-services}

Los servicios inteligentes permiten a los analistas y profesionales de marketing aprovechar el poder de la inteligencia artificial y el aprendizaje automático en casos prácticos de experiencias del cliente. Esto permite a analistas de marketing formular predicciones concretas de las necesidades de una compañía mediante configuraciones de negocio sin necesidad de tener experiencia en la ciencia de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Conjunto de datos de Eventos de experiencia del consumidor (CEE) | La creación de un conjunto de datos de CEE ahora admite la adición de campos de identidad al conjunto de datos con el Editor de esquemas. La inteligencia artificial aplicada al Attribution AI y el cliente utilizan la identidad principal para combinar eventos. |

Para obtener más información, lea la sección sobre [agregar campos de identidad a un conjunto de datos](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) en la guía de preparación de datos de servicios inteligentes.

### Inteligencia artificial aplicada a la atribución

Attribution AI, como parte de Intelligent Services, es un servicio de atribución algorítmica de varios canales que calcula la influencia y el impacto incremental de las interacciones de los clientes con los resultados especificados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de fuente de datos | El vínculo al origen del conjunto de datos original se puede ver y navegar a desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Ahora puede modificar el nombre de una instancia de Attribution AI existente. |
| Clonar instancia | Copia la configuración de la instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Modificar parámetros de configuración de instancia | Ahora puede modificar la configuración de una instancia de Attribution AI existente si aún no ha iniciado la puntuación. |
| Puntuación única | Ahora puede almacenar en déclencheur la puntuación del modelo ad hoc en las instancias de Attribution AI. |
| Paso a través de columnas | Ahora puede configurar columnas adicionales que se añadirán a los archivos de puntuación de salida sin procesar para añadir dimensiones adicionales a las vistas de herramientas de BI. |
| Activación y desactivación de instancias | Ahora puede activar y desactivar la formación y la puntuación del modelo programado de las instancias de Attribution AI. |
| Seguimiento de derechos | Puede encontrar la cantidad total de información de atribución consumida por su cuenta en el contenedor Crear instancia. |
| Desglose por posición del punto de contacto | Un nuevo gráfico de perspectivas que proporciona un análisis de los puntos de contacto por las posiciones de la ruta de conversión. |
| Rutas de conversión principales | Un nuevo gráfico de perspectivas ubicado en la pestaña Análisis de rutas. El gráfico contiene una lista de las cinco rutas de conversión principales que muestran la secuencia de puntos de contacto del canal de marketing que produjeron la mayor cantidad de conversiones. |
| Eficacia de Touchpoint | Proporciona información detallada sobre las tres variables más importantes mediante las que el modelo mide la eficacia de los puntos de contacto. Las variables son la proporción de rutas positivas y negativas tocadas, la eficiencia del punto de contacto y el volumen del punto de contacto. |

Para obtener más información, lea [descripción general de la Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Inteligencia artificial aplicada al cliente

La inteligencia artificial aplicada al cliente, como parte de los servicios inteligentes, proporciona a los especialistas en marketing la capacidad de generar predicciones sobre clientes a nivel individual con explicaciones. Con la ayuda de factores influyentes, la inteligencia artificial aplicada al cliente puede indicarle qué es lo más probable que haga un cliente y por qué. Además, los especialistas en marketing pueden beneficiarse de las predicciones y perspectivas de la inteligencia artificial aplicada al cliente para personalizar las experiencias de los clientes y ofrecerles las ofertas y los mensajes más adecuados.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Vínculo de fuente de datos | El vínculo al origen del conjunto de datos original se puede ver y navegar a desde el carril derecho de una instancia de servicio seleccionada. |
| Editar nombre de instancia | Puede modificar el nombre de una instancia de inteligencia artificial aplicada al cliente existente. |
| Modificar parámetros de configuración de instancia | Ahora puede modificar la configuración de una instancia de inteligencia artificial aplicada al cliente existente si aún no ha iniciado una puntuación. |
| Clonar instancia | Copia la configuración de la instancia de servicio seleccionada actualmente y permite realizar modificaciones. |
| Seguimiento de derechos | Puede encontrar la cantidad total de perfiles clasificados por la inteligencia artificial aplicada al cliente para su cuenta en el contenedor Crear instancia. |
| Objetivo de predicción | La flexibilidad para crear un objetivo de predicción se ha aumentado con nuevas opciones para predecir si algo &quot;ocurrirá&quot; o &quot;no ocurrirá&quot;. Además, se han añadido las opciones para predecir si &quot;todos&quot; los eventos se producen o &quot;cualquiera&quot; de los eventos se producen cuando se utilizan varios eventos. |
| Desglose de factor influyente | Los bloques de factores influyentes principales de tendencia ahora contienen desgloses detallados. Los desgloses detallados son un resumen de nivel más profundo de los valores de cada uno de los principales factores influyentes dentro de un bloque de tendencia. |

Para obtener más información, lea la [Descripción general de la inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/overview.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos de clientes dispares en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Flujo de trabajo de políticas de combinación actualizado | Platform ha actualizado la configuración de la política de combinación a un nuevo flujo de trabajo paso a paso. Este flujo de trabajo permite a los usuarios reunir fragmentos de datos de varios conjuntos de datos de perfil y establecer la prioridad del modo en que se combinan los datos en esos conjuntos de datos para crear una vista completa de cada individuo. Los usuarios pueden combinar los conjuntos de datos de perfil individual XDM seleccionados seleccionando el método de combinación adecuado (Marca de tiempo ordenada o Prioridad de conjuntos de datos) y añadiendo conjuntos de datos ExperienceEvent a los conjuntos de datos de perfil. |
| Vista de esquema de unión | En la IU de Experience Platform, los usuarios pueden encontrar más fácilmente información sobre todos los esquemas y conjuntos de datos que contribuyen al esquema de unión, así como atributos de clave de superficie como los campos de identidad y relación. Estas actualizaciones mejoran la capacidad de solucionar problemas y validar que los perfiles están correctamente configurados, las identidades están correctamente vinculadas y los datos se han introducido correctamente. |

Para obtener más información sobre el perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de [!DNL Profile], lea la [descripción general del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevos orígenes**

| Función | Descripción |
| ------- | ----------- |
| [!DNL Shopify] | Ahora puede conectar [!DNL Shopify] a [!DNL Experience Platform] mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [descripción general del conector Shopify](../../sources/connectors/ecommerce/shopify.md) para obtener más información. |

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualizar información de conexión | Ahora puede actualizar los nombres, descripciones y credenciales de las conexiones por lotes existentes mediante la API [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [actualización de conexiones mediante la API de Flow Service](../../sources/tutorials/api/update.md) y [edición de detalles de cuenta mediante la interfaz de usuario](../../sources/tutorials/ui/monitor.md). |
| Eliminación de conexiones | Las conexiones por lotes que contienen errores o se han vuelto innecesarias ahora se pueden eliminar mediante la API [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [eliminar conexiones mediante la API de Flow Service](../../sources/tutorials/api/delete.md) y [eliminar cuentas mediante la interfaz de usuario](../../sources/tutorials/ui/delete-accounts.md). |
| Asignación jerárquica | Puede obtener una vista previa de un archivo de origen jerárquico, como JSON o Parquet, durante el proceso de ingesta de datos. Consulte el tutorial sobre [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información. |
| Compatibilidad con API para asignación en fuentes de flujo continuo | Ahora puede utilizar las API para realizar funciones de asignación con fuentes de flujo continuo. |
| Compatibilidad con API para delimitadores personalizados para fuentes de almacenamiento en la nube | Ahora puede recopilar archivos no delimitados por CSV mediante fuentes de almacenamiento en la nube. Puede utilizar cualquier delimitador de columna individual, como tabulación, coma, barra vertical, punto y coma o hash, para recopilar archivos planos en cualquier formato. |
| Compatibilidad con zonas protegidas para el conector Adobe Audience Manager | El conector del Audience Manager ahora reconoce la zona protegida. Los usuarios pueden habilitar el conector para enrutar los conjuntos de datos del Audience Manager a la zona protegida que elijan (incluidas las zonas protegidas que no sean de producción). La configuración está limitada a una zona protegida por organización. |
| Mejoras de UX | Ahora se puede acceder a la ingesta basada en archivos a través del catálogo de fuentes. |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
