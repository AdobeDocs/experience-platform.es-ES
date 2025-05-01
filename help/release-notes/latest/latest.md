---
title: 'Notas de la versión de Adobe Experience Cloud: abril de 2025'
description: Las notas de la versión de abril de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3836b369d609448146a273fc6cf29061fd1ea422
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 29%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para Notas de la versión de otras aplicaciones Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: miércoles, 29 de abril de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Experience League](#experience-league)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Servicio de identidad](#identity)
- [Servicio de consultas](#query-service)
- [Perfil del cliente en tiempo real](#profile)
- [Zonas protegidas](#sandboxes)
- [Fuentes](#sources)
- [Manuales de tácticas de casos de uso](#use-case-playbooks)

## Experience League {#experience-league}

Experience League es una plataforma de aprendizaje integral diseñada para ayudarlo a mejorar sus habilidades con Adobe Systems productos. Ofrece una variedad de recursos, que incluyen: cursos, documentación, páginas de comunidad, eventos y acceso a certificaciones.

| Función | Descripción |
| --- | --- |
| Página de inicio personalizada | Acceda a su página de inicio personalizada en [Experience League](https://experienceleague.adobe.com/en/home#) y personalícela. Inicie sesión con sus credenciales de Adobe y, a continuación, seleccione **[!UICONTROL Experience League]** en el menú superior para comenzar a optimizar su experiencia de aprendizaje: <ul><li>**Marcadores**: usa la característica [!UICONTROL Marcadores] para guardar y recopilar tus recursos favoritos en un solo lugar. Puede guardar una variedad de contenido, incluidas listas de reproducción, artículos y tutoriales.</li><li>**Personalice su aprendizaje**: mejore su experiencia de aprendizaje actualizando su perfil de Experience League con las funciones, industrias, productos y experiencia nivel que mejor se adapten a sus necesidades.</li><li>**Recommendations**: Ver contenido de aprendizaje recomiendan en función de sus actividad recientes.</li><li>**Vistos** recientemente: utilice la [!UICONTROL sección Vistos] recientemente para volver rápidamente a los contenido vistos recientemente, como documentación y vídeos.</li><li>**Recursos** de aprendizaje: use el panel Todos los [!UICONTROL recursos] de aprendizaje para navegar a tutoriales, documentación, comunidad, eventos y certificaciones.</li><li>**Novedades**: Ver la [!UICONTROL sección Novedades] para ver una emisión de los últimos contenido de Experience League.</li><li>**Vea eventos pasados a pedido**: vea transmisiones en vivo previamente grabadas sobre aspectos destacados de productos, casos de uso y tutoriales con la [!UICONTROL sección Ver eventos anteriores a pedido] .</li></ul><br> ![página de inicio personalizados en Experience League.](../2025/assets/april/personalized-home-page.png "página de inicio personalizados en Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Sincronización de persona de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe actualizó el destino [!DNL Marketo Engage Person Sync] para solucionar un problema que afectaba a los clientes cuando había varios correos electrónicos presentes en el mapa de identidad. |
| [(V2) Pega CDH Conexión de audiencia en tiempo real](/help/destinations/catalog/personalization/pega-v2.md) | Utilice el destino en Adobe Experience Platform [!DNL (V2) Pega Customer Decision Hub Realtime Audience] para enviar atributos de perfil y datos de abono de audiencia a Pega Customer Decision Hub para tomar decisiones de la siguiente mejor acción, cuando tenga varias aplicaciones de Pega Customer Decision Hub configuradas en su cuenta de Pega. |

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| **Opciones de programación semanal** y **mensual** para la exportación de archivos completos | Ahora puede programar exportaciones de archivos completos para personas y audiencias cliente potencial semanal o mensualmente al realizar la activación para nube destinos basados en archivos almacenamiento. [Obtenga más información](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) sobre las opciones de programación. |

{style="table-layout:auto"}

**Correcciones, mejoras y otros anuncios** {#destinations-fixes-and-enhancements}

- **La aplicación de las fechas de finalización de conjunto de datos exportación se retrasa hasta el 1 de septiembre de 2025**\
  Como parte de la [versión](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality) de septiembre de 2024, Adobe Systems establecer una fecha de finalización predeterminada del 1 de mayo de 2025 para cualquier flujo de datos de exportación conjunto de datos creado *antes de esa versión*. Adobe Systems ahora está extendiendo este plazo de cumplimiento hasta **el 1 de septiembre de 2025** para proporcionar a los clientes tiempo adicional para actualizar sus horarios. Consulte la sección de programación de los [conjuntos de datos de exportación tutorial](../../destinations/ui/export-datasets.md#schedule-dataset-export) para obtener información sobre cómo editar la fecha de finalización de un flujo de datos de exportación de conjunto de datos.

- **Se ha mejorado la gestión de las transferencias SFTP fallidas para la integración de LiveRamp**\
  Adobe Systems ha implementado una solución para un problema que afectaba a las exportaciones de archivos al destino de integración de [](/help/destinations/catalog/advertising/liveramp-onboarding.md) LiveRamp a través de SFTP. Ocasionalmente, las transferencias de archivos fallaban debido a problemas de del lado del servidor transitorios y los archivos temporales de intentos fallidos permanecían en el servidor. Estos archivos imborrables bloquearon los reintentos posteriores, ya Adobe Systems no tenían permiso para sobrescribirlos.\
  Con la corrección, si un intento de reintento no puede eliminar el archivo temporal, Adobe Systems generará un nuevo archivo con un sufijo anexado ,`attempt2`, para garantizar que el reintento se complete correctamente.

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Componentes XDM actualizados**

| Función | Descripción |
| --- | --- |
| Los campos de cadena reciben un valor mínimo de uno | Nuevo campos de cadena tienen una longitud mínima de uno de forma predeterminada. Los valores nulos para los campos no obligatorios siguen siendo aceptables. Para obtener más información sobre las prácticas recomendadas, lea la guía de [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Disponibilidad limitada]{type=Informative} [!DNL Identity Graph Linking Rules] | Las reglas de vinculación de gráficos de identidad ahora están en disponibilidad limitada y todos los clientes pueden acceder a ellas en los entornos limitados de desarrollo. <ul><li>**Requisitos de activación**: la característica permanecerá inactiva hasta que configure y guarde su [!DNL Identity Settings]. Sin esta configuración, el sistema seguirá funcionando normalmente, sin cambios en el comportamiento.</li><li>**Notas importantes**: durante esta fase de disponibilidad limitada, la segmentación de Edge puede producir resultados inesperados en los miembros del segmento. Sin embargo, la transmisión y la segmentación por lotes funcionarán según lo esperado.</li><li>**Pasos siguientes**: para obtener información sobre cómo habilitar esta característica en los entornos limitados de producción, póngase en contacto con el equipo de la cuenta de Adobe.</li></ul> |

{style="table-layout:auto"}

Para obtener más información, lea la [[!DNL Identity Graph Linking Rules] documentación](../../identity-service/identity-graph-linking-rules/overview.md).

## Servicio de consultas {#query-service}

Consulte datos en el lago de datos de Adobe Experience Platform utilizando SQL estándar con el Servicio de consultas. Combine conjuntos de datos sin problemas y genere otros nuevos a partir de los resultados de su consulta para impulsar la creación de informes, habilitar flujos de trabajo de ciencia de datos o facilitar la ingesta en el Perfil del cliente en tiempo real. Por ejemplo, puede combinar los datos de transacciones de clientes con datos de comportamiento para identificar públicos de alto valor para campañas de marketing dirigidas.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Sobrescritura de audiencia SQL | Actualice la pertenencia a audiencias sobrescribiendo los perfiles existentes con los resultados de una nueva consulta SQL. Esto le permite administrar audiencias dinámicas de manera más eficiente eliminando registros obsoletos e insertando registros actualizados en una sola operación. Para obtener más información, consulte el guía extensión de [SQL audiencia](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Descargar y copiar los resultados de la consulta | [Descargue consulta resultados directamente desde el Editor](../../query-service/ui/overview.md#download-query-results) de consultas como archivos CSV, XLSX o JSON, o [bien copie los resultados a su portapapeles](../../query-service/ui/overview.md#copy-results) como valores separados por comas (CSV) para utilizarlos rápidamente en aplicaciones de hoja de cálculo gustar Excel. Estas mejoras optimizan la sin conexión flujos de trabajo de análisis, sistema de informes y validación de datos. |
| Ver resultados de la consulta en pantalla completa | [Vista previa consulta da como resultado un cuadro de diálogo](../../query-service/ui/overview.md#view-results) de pantalla completa para mejorar la legibilidad, escanear fácilmente conjuntos de datos grandes y seleccionar filas para copiar. El vista de pantalla completa proporciona un diseño de cuadrícula redimensionable, lo que le ayuda a revisar tablas anchas y resultados detallados de manera más eficiente. |
| Selección de columnas mejorada en la predicción del modelo | Seleccione columnas específicas y aplique alias utilizando la sintaxis extendida `model_predict`. Recupere resultados de predicción intermedios, como vectores de características y puntuaciones de probabilidad. La selección mejorada requiere la activación de un indicador de funcionalidad. Consulte [Documentación del ciclo de vida del modelo](../../query-service/advanced-statistics/models.md#select-specific-output-fields) para ver ejemplos de sintaxis y detalles de indicadores de características. |
| Resultados de la predicción del modelo Guardar usando CREATE TABLE e INSERT INTO | [Guardar las salidas de predicción seleccionadas en tablas nuevas mediante CREAR TABLA COMO SELECT o insertar en tablas existentes mediante INSERT INTO SELECT.](../../query-service/advanced-statistics/models.md#predict) Si se habilita la selección mejorada de columnas, también se pueden mantener los resultados intermedios, como los vectores de características y las probabilidades, junto con las predicciones finales. Para ver ejemplos de uso, consulte la [documentación de sintaxis SQL](../../query-service/sql/syntax.md#create-table-as-select). |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../../query-service/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción del cliente.

| Función | Descripción |
| ------- | ----------- |
| Caducidad de los datos de perfil seudónimo | Administrar el seudónimo perfil caducidad de los datos en el panel de perfil. Para obtener más información acerca de esta función y los perfiles seudónimos, lea la [Guía de caducidad de datos de perfil seudónimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Para obtener más información sobre el perfil del cliente en tiempo real, lea la [descripción general del perfil](../../profile/home.md)

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Experience Platform en entornos virtuales separados para ayudar a que se desarrollan y evolucionen las aplicaciones de experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Las herramientas de Sandbox plug-in admiten la expansión | Las acciones personalizadas ahora se pueden copiar como un objeto dependiente al duplicar objetos Journey en herramientas de simulador para pruebas. Además, puede seleccionar acciones existentes para reutilizarlas en el destino entorno de pruebas. También se pueden añadir a un paquete de forma independiente. Para obtener información completa sobre los objetos Adobe Journey Optimizer admitidos, lea la guía [herramientas de espacio aislado](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Nuevos orígenes**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | El origen [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) ya está disponible. Utilice esta fuente para llevar los datos de afinidades de perfiles de usuario de [!DNL Algolia] a Experience Platform. A continuación, puede utilizar estos datos para mejorar la participación del usuario, las tasas de Conversión y la experiencia del cliente general proporcionando soluciones de búsqueda de alto rendimiento para sitios web, plataformas comercio electrónico y aplicaciones. Para obtener más información, lea la guía sobre cómo [incorporar [!DNL Algolia User Profiles] datos en Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| [!BADGE ]{type=Informative} Compatibilidad API de Beta con[!DNL Azure Databricks] | El origen [!DNL Azure Databricks] ya está disponible en la API. Use la API [!DNL Flow Service] para conectar su cuenta de [!DNL Databricks] y llevar los datos de [!DNL Databricks] a Experience Platform. Para obtener más información, lea la documentación sobre [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Se han actualizado los campos XDM para la ingesta de datos de medios de streaming en Experience Platform. | El nuevo grupo de campos XDM `mediaReporting` ya está disponible para la ingesta de datos de medios de streaming a través del origen de Adobe Analytics en Experience Platform. Este campo reemplaza el campo `media.mediaTimed`.</br> <br>Durante un período de transición de tres meses, continuará la ingesta de datos en `media.mediaTimed` los campos. Sin embargo, a finales de julio de 2025, los `media.mediaTimed` campos quedarán totalmente obsoletos y dejarán de ser visibles en el IU de esquema de Experience Platform, y los datos solo se enviarán utilizando los `mediaReporting` campos.</br><br>Si ha implementado el origen Analytics para recopilar datos de Streaming Media en Platform antes del 22 de abril de 2025, debe migrar las configuraciones existentes para enviar datos mediante el nuevo campo grupo. Esta migración debe completarse a finales de julio de 2025. Póngase en contacto con su equipo de cuentas Adobe Systems para obtener asistencia relacionada con la migración. |
| Nuevo tipos de autenticación para [!DNL MariaDB] y [!DNL PostgreSQL] | Ahora puede usar la autenticación básica para autenticar los orígenes de [!DNL MariaDB] y [!DNL PostgreSQL] en Experience Platform. Lea la siguiente documentación para obtener más información: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Compatibilidad con filtrado a nivel de fila para [!DNL Amazon Redshift] | Puede usar capacidades de filtrado a nivel de fila para los [!DNL Amazon Redshift] datos en Experience Platform. Para obtener más información, lea la guía sobre [filtrado de datos de nivel de fila para orígenes en la API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

## Manuales de tácticas de casos de uso {#use-case-playbooks}

Los manuales de casos de uso se diseñaron originalmente para ayudar a superar los desafíos al comenzar con Real-Time Customer Data Platform o Adobe Journey Optimizer. Siguen evolucionando y ahora le permiten poner en marcha casos prácticos de marketing clave y proporcionar inspiración y recursos creados previamente para probar y pasar a la producción.

Los manuales de casos de uso han pasado de ser una herramienta de descubrimiento a un marco de trabajo colaborativo. Ahora le ayudan a crear, administrar y compartir sus propios libros de reproducción entre diferentes organizaciones.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} Crea y comparte tus propios libros de reproducción | Un nuevo módulo de creación de libros de estrategias le permite crear, administrar y compartir sus propios libros de casos de uso. Esto incluye compatibilidad con la captura de metadatos clave, la edición de mapas de viaje y la asociación de activos técnicos relevantes. Puede compartir manuales entre organizaciones para estandarizar los enfoques de marketing y mantener la coherencia. |

{style="table-layout:auto"}

Para saber cómo puede crear y compartir sus propios libros de estrategias, lea la Autor y comparta sus propios libros](/help/use-case-playbooks/playbooks/author.md) de [estrategias documento.

Para obtener más información, lea la [Descripción general de los libros de casos de uso](/help/use-case-playbooks/playbooks/overview.md), que proporciona información general sobre la funcionalidad de los libros de reproducción, su propósito y una demostración completa, incluyendo cómo crear instancias e importar recursos generados en otros entornos de espacio aislado.
