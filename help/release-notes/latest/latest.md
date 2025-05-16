---
title: 'Notas de la versión de Adobe Experience Platform: abril de 2025'
description: Las notas de la versión de abril de 2025 de Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e0740ca9cd6e1d0b92d5504a2869ac03c28d4980
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 100%

---

# Notas de la versión de Adobe Experience Platform

>[!TIP]
>
>Consulte la siguiente documentación para ver las notas de la versión de otras aplicaciones de Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/es/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/latest)

**Fecha de publicación: 29 de abril de 2025**

Actualizaciones de funciones y documentación existentes en Adobe Experience Platform:

- [Experience League](#experience-league)
- [Recopilación de datos](#data-collection)
- [Destinos](#destinations)
- [Modelo de datos de experiencia](#xdm)
- [Servicio de identidad](#identity)
- [Servicio de consultas](#query-service)
- [Zonas protegidas](#sandboxes)
- [Fuentes](#sources)
- [Manuales de tácticas de casos de uso](#use-case-playbooks)

## Experience League {#experience-league}

Experience League es una plataforma de aprendizaje integral que le ayudará a perfeccionar sus habilidades con los productos de Adobe. Ya que ofrece una variedad de recursos, incluidos cursos, documentación, páginas de la comunidad, eventos y acceso a certificaciones.

| Función | Descripción |
| --- | --- |
| Página de inicio personalizada | Acceda a su página de inicio personalizada en [Experience League](https://experienceleague.adobe.com/es/home#) y personalícela aún más. Inicie sesión con sus credenciales de Adobe y, a continuación, seleccione **[!UICONTROL Experience League]** en el menú superior para optimizar su experiencia de aprendizaje. <ul><li>**Marcadores**: utilice la característica [!UICONTROL Marcadores] para guardar y recopilar sus recursos favoritos en un solo lugar. Puede guardar una variedad de contenido, incluidas listas de reproducción, artículos y tutoriales.</li><li>**Personalice su aprendizaje**: mejore su experiencia de aprendizaje al actualizar su perfil de Experience League con las funciones, sectores, productos y niveles de experiencia que mejor se adapten a sus necesidades.</li><li>**Recomendaciones**: vea contenido de aprendizaje recomendado en función de su actividad reciente.</li><li>**Vistos recientemente**: utilice la sección [!UICONTROL Vistos recientemente] para volver rápidamente al contenido visualizado recientemente, como documentación y vídeos.</li><li>**Recursos de aprendizaje**: use el panel [!UICONTROL Todos los recursos de aprendizaje] para ir a tutoriales, documentación, comunidad, eventos y certificaciones.</li><li>**Novedades**: vea la sección [!UICONTROL Novedades] para ver una secuencia del contenido más reciente en Experience League.</li><li>**Ver eventos anteriores bajo demanda**: mire transmisiones en vivo grabadas anteriormente sobre temas destacados de productos, casos de uso y tutoriales en la sección [!UICONTROL Ver eventos anteriores bajo demanda].</li></ul><br> ![Página de inicio personalizada en Experience League.](../2025/assets/april/personalized-home-page.png "Página de inicio personalizada en Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Recopilación de datos {#data-collection}

Adobe Experience Platform proporciona un conjunto de tecnologías que le permiten recopilar datos de experiencia del cliente del lado del cliente y enviarlos a la red perimetral de Adobe Experience Platform, donde se pueden enriquecer, transformar y distribuir a destinos de Adobe o que no sean de Adobe.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Extensión [!DNL Adform] | La extensión del lado del servidor [!DNL Adform] permite que las marcas vuelvan a direccionar fácilmente a los públicos fuera del sitio mediante ECID. Esta extensión del lado del servidor no depende de cookies de terceros ni de ID alternativos de cookies. Además, como esto se realiza completamente en el lado del servidor, no se necesitan píxeles adicionales ni otros cambios en el lado del cliente. Para obtener más información, consulte la [información general de la extensión Adform](/help/tags/extensions/server/adform/overview.md). |
| Extensión de API de eventos web de [!DNL Amazon] | La extensión de API de conversiones de [!DNL Amazon] permite a los anunciantes compartir las interacciones del sitio web directamente con [!DNL Amazon], lo que mejora la atribución, la fiabilidad de los datos y la optimización de la campaña. Esta extensión es compatible con el reenvío de eventos, lo que le permite enviar eventos de conversión como compras, adiciones al carro de compras y mucho más, a la vez que garantiza la anulación de duplicación adecuada para unos informes precisos. Para obtener más información, consulte la [información general de la extensión de Amazon](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Destinos nuevos o actualizados** {#new-updated-destinations}

| Destino | Descripción |
| --- | --- |
| [Sincronización de personas de Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe actualizó el destino de [!DNL Marketo Engage Person Sync] para solucionar un problema que afectaba a los clientes cuando había varios correos electrónicos presentes en el mapa de identidad. |
| [(V2) Conexión de público en tiempo real de Pega CDH](/help/destinations/catalog/personalization/pega-v2.md) | Utilice el destino [!DNL (V2) Pega Customer Decision Hub Realtime Audience] en Adobe Experience Platform para enviar atributos de perfil y datos de abonos del público al Centro de decisiones de clientes de Pega para la toma de decisiones de la mejor acción siguiente, cuando tenga varias aplicaciones del Centro de decisiones de clientes de Pega configuradas en su cuenta de Pega. |

**Funcionalidad nueva o actualizada** {#destinations-new-updated-functionality}

| Función | Descripción |
| --- | --- |
| Opciones de programación **semanales** y **mensuales** para exportaciones de archivos completos | Ahora puede programar exportaciones de archivos completas para personas y públicos de clientes potenciales de forma semanal o mensual al activarlas en destinos basados en archivos de almacenamiento en la nube. [Más información](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) sobre las opciones de programación. |

{style="table-layout:auto"}

**Correcciones, mejoras y otros anuncios** {#destinations-fixes-and-enhancements}

- **La aplicación de las fechas de finalización de la exportación del conjunto de datos se retrasó hasta el 1 de septiembre de 2025**\
  En la [versión de septiembre de 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality), Adobe estableció el 1 de mayo de 2025 como la fecha de finalización predeterminada para cualquier flujo de datos de exportación de conjuntos de datos creado *antes de esa versión*. Adobe extendió esta fecha límite de aplicación al **1 de septiembre de 2025** para proporcionar a los clientes tiempo adicional para actualizar sus programaciones. Consulte la sección de programación del [tutorial de exportación de conjuntos de datos](../../destinations/ui/export-datasets.md#schedule-dataset-export) para obtener información sobre la edición de la fecha de finalización de un flujo de datos de exportación de conjuntos de datos.

- **Se ha mejorado la administración de las transferencias con SFTP fallidas para LiveRamp Onboarding**\
  Adobe ha implementado una corrección para el problema que afecta a las exportaciones de archivos al destino [LiveRamp Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md) a través de SFTP. En ocasiones, las transferencias de archivos fallaban debido a problemas transitorios del lado del servidor y los archivos temporales de los intentos fallidos permanecían en el servidor. Estos archivos que no se podían eliminar bloqueaban los reintentos posteriores, ya que Adobe no tenía permiso para sobrescribirlos.\
  Con la corrección, si al reintentar, no se podía eliminar el archivo temporal, Adobe generaba un nuevo archivo con un sufijo anexado, `attempt2`, para garantizar que el reintento se complete correctamente.

## Modelo de datos de experiencia (XDM) {#xdm}

XDM es una especificación de código abierto que proporciona estructuras y definiciones comunes (esquemas) para los datos que se incorporan a Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común para ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Componentes XDM actualizados**

| Función | Descripción |
| --- | --- |
| Los campos de cadena reciben un valor mínimo de uno | Los nuevos campos de cadena tienen una longitud mínima de uno de forma predeterminada. Los valores nulos para los campos no obligatorios siguen siendo aceptables. Para obtener más información sobre las prácticas recomendadas, lea la guía de [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Para obtener más información sobre XDM en Experience Platform, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Servicio de identidad {#identity}

El servicio de identidad de Adobe Experience Platform le ofrece una vista completa de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Disponibilidad limitada]{type=Informative} [!DNL Identity Graph Linking Rules] Ahora todos los clientes pueden acceder a las reglas de vinculación de gráfico de identidad en las zonas protegidas de desarrollo. <ul><li>**Requisitos de activación**: la característica permanecerá inactiva hasta que configure y guarde su [!DNL Identity Settings]. Sin esta configuración, el sistema seguirá funcionando normalmente, sin cambios en el comportamiento.</li><li>**Notas importantes**: Durante esta fase de disponibilidad limitada, la segmentación de Edge puede producir resultados inesperados en la pertenencia al segmento. Sin embargo, el streaming y la segmentación por lotes funcionarán según lo esperado.</li><li>**Pasos siguientes**: para obtener información sobre la habilitación de esta característica en las zonas protegidas de producción, póngase en contacto con el equipo de cuentas de Adobe.</li></ul> |

{style="table-layout:auto"}

Para obtener más información, consulte la [[!DNL Identity Graph Linking Rules] documentación](../../identity-service/identity-graph-linking-rules/overview.md).

## Servicio de consultas {#query-service}

Consulte datos en el lago de datos de Adobe Experience Platform utilizando SQL estándar con el Servicio de consultas. Combine conjuntos de datos sin problemas y genere otros nuevos a partir de los resultados de su consulta para impulsar la creación de informes, habilitar flujos de trabajo de ciencia de datos o facilitar la ingesta en el Perfil del cliente en tiempo real. Por ejemplo, puede combinar los datos de transacciones de clientes con datos de comportamiento para identificar públicos de alto valor para campañas de marketing dirigidas.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Sobrescritura de públicos de SQL | Actualice la pertenencia a públicos sobrescribiendo los perfiles existentes con los resultados de una nueva consulta SQL. Esto permite administrar los públicos dinámicos de forma más eficaz eliminando registros obsoletos e insertando registros actualizados en una sola operación. Para obtener más información, consulte la [Guía de ampliación de público de SQL](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Descarga y copia de resultados de la consulta | [Descargue los resultados de la consulta directamente desde el Editor de consultas](../../query-service/ui/overview.md#download-query-results) como archivos CSV, XLSX o JSON, o [copie los resultados en el portapapeles](../../query-service/ui/overview.md#copy-results) como valores separados por comas (CSV) para su uso rápido en aplicaciones de hojas de cálculo como Excel. Estas mejoras optimizan los flujos de trabajo de análisis, creación de informes y validación de datos sin conexión. |
| Ver resultados de la consulta en pantalla completa | [Vista previa de los resultados de la consulta en un cuadro de diálogo de pantalla completa](../../query-service/ui/overview.md#view-results) para mejorar la legibilidad, analizar fácilmente conjuntos de datos grandes y seleccionar filas para copiar. La vista de pantalla completa proporciona un diseño de cuadrícula redimensionable, lo que sirve para revisar tablas anchas y resultados detallados de forma más eficaz. |
| Selección de columnas mejorada en la predicción del modelo | Seleccione columnas específicas y aplique alias utilizando la sintaxis extendida `model_predict`. Recupere resultados de predicción intermedios, como vectores de características y puntuaciones de probabilidad. La selección mejorada requiere la activación de un indicador de función. Consulte la [Documentación del ciclo de vida del modelo](../../query-service/advanced-statistics/models.md#select-specific-output-fields) para ver ejemplos de sintaxis y datos de indicadores de función. |
| Guardar salidas de predicción de modelo usando CREATE TABLE e INSERT INTO | [Guarde los resultados de predicción seleccionados en tablas nuevas utilizando CREATE TABLE AS SELECT o inserte en tablas existentes utilizando INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Si se habilita la selección mejorada de columnas, también se pueden mantener los resultados intermedios, como los vectores de características y las probabilidades, junto con las predicciones finales. Para ver ejemplos de uso, consulte la [documentación de sintaxis SQL](../../query-service/sql/syntax.md#create-table-as-select). |

Para obtener más información sobre [!DNL Query Service], consulte la [[!DNL Query Service] Información general](../../query-service/home.md).

## Zonas protegidas {#sandboxes}

Adobe Experience Platform está diseñado para enriquecer las aplicaciones de experiencia digital a escala global. Las empresas suelen ejecutar varias aplicaciones de experiencia digital en paralelo y necesitan encargarse del desarrollo, las pruebas y la implementación de estas aplicaciones, a la vez que garantizan el cumplimiento normativo. Para responder a esta necesidad, Experience Platform proporciona zonas protegidas que dividen una única instancia de Experience Platform en entornos virtuales separados para ayudar a que se desarrollan y evolucionen las aplicaciones de experiencia digital.

**Funciones nuevas o actualizadas**

| Función | Descripción |
| --- | --- |
| Ampliación de compatibilidad de complemento de herramientas de zona protegida | Ahora, las acciones personalizadas se pueden copiar como un objeto dependiente al duplicar objetos de Recorrido en las herramientas de zona protegida. Además, puede seleccionar acciones existentes para reutilizarlas en la zona protegida de destinatario. También se pueden añadir a un paquete de forma independiente. Para obtener información completa sobre los objetos de Adobe Journey Optimizer admitidos, lea la guía de [herramientas de zona protegida](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Para obtener más información sobre las zonas protegidas, lea la [información general sobre zonas protegidas](../../sandboxes/home.md).

## Fuentes {#sources}

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

Utilice fuentes en Experience Platform para introducir datos de una aplicación de Adobe o una fuente de datos de terceros.

**Nuevos orígenes**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | La fuente de [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) ahora está disponible. Utilice esta fuente para llevar sus datos de afinidades de perfiles de usuario de [!DNL Algolia] a Experience Platform. A continuación, puede utilizar estos datos para mejorar la participación del usuario, las tasas de conversión y la experiencia general del cliente mediante el suministro de soluciones de búsqueda de alto rendimiento para sitios web, plataformas de comercio electrónico y aplicaciones. Para más información, lea la guía sobre cómo [ingestar [!DNL Algolia User Profiles]  datos a Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| Compatibilidad con la API [!BADGE Beta]{type=Informative} para [!DNL Azure Databricks] | La fuente [!DNL Azure Databricks] ya está disponible en la API. Use la API de [!DNL Flow Service] para conectar su cuenta de [!DNL Databricks] y llevar los datos de [!DNL Databricks] a Experience Platform. Para obtener más información, lea la documentación sobre [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Se han actualizado los campos XDM para la ingesta de datos de medios de streaming en Experience Platform. | El nuevo grupo de campos XDM `mediaReporting` ya está disponible para la ingesta de datos de medios de streaming a través de la fuente de Adobe Analytics para Experience Platform. Este campo reemplaza el campo `media.mediaTimed`.</br> <br>Durante un período de transición de tres meses, la ingesta de datos en los campos `media.mediaTimed` continuará. Sin embargo, a finales de julio de 2025, los campos `media.mediaTimed` quedarán totalmente obsoletos y dejarán de ser visibles en la interfaz de usuario del esquema de Experience Platform, y los datos solo se enviarán mediante los campos `mediaReporting`.</br><br>Si ha implementado el origen de Analytics para recopilar datos de medios de streaming en Platform antes del 22 de abril de 2025, debe migrar las configuraciones existentes para enviar datos mediante el nuevo grupo de campos. Esta migración debe completarse para finales de julio de 2025. Póngase en contacto con el equipo de cuentas de Adobe para obtener ayuda sobre la migración. |
| Nuevos tipos de autenticación para [!DNL MariaDB] y [!DNL PostgreSQL] | Ahora puede usar la autenticación básica para autenticar las fuentes de [!DNL MariaDB] y [!DNL PostgreSQL] en Experience Platform. Lea la siguiente documentación para obtener más información: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Compatibilidad con filtrado a nivel de fila para [!DNL Amazon Redshift] | Puede usar funcionalidades de filtrado a nivel de fila para sus datos de [!DNL Amazon Redshift] en Experience Platform. Para obtener más información, lea la guía de [filtrado de datos para una fuente mediante la API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Para obtener más información, lea la [Información general de las fuentes](../../sources/home.md).

## Manuales de tácticas de casos de uso {#use-case-playbooks}

Los manuales de tácticas de casos de uso se diseñaron originalmente para superar los desafíos al comenzar con Real-Time Customer Data Platform o Adobe Journey Optimizer. Siguen evolucionando y ahora le permiten poner en marcha casos prácticos de marketing clave y proporcionar inspiración y recursos creados previamente para probar y pasar a la producción.

Los manuales de tácticas de casos de uso han pasado de ser una herramienta de descubrimiento a un marco de trabajo colaborativo. Ahora le ayudan a crear, administrar y compartir sus propios manuales de tácticas entre diferentes organizaciones.

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| [!BADGE Beta]{type=Informative} Cree y comparta sus propios manuales de tácticas | Un nuevo marco de trabajo de creación de manuales de tácticas le permite crear, administrar y compartir sus propios manuales de tácticas de casos de uso. Esto incluye compatibilidad para capturar metadatos clave, editar mapas de recorrido y asociar recursos técnicos relevantes. Puede compartir manuales de tácticas entre organizaciones para estandarizar los enfoques de marketing y mantener la coherencia. |

{style="table-layout:auto"}

Para aprender a crear y compartir sus manuales de tácticas, lea el documento [Crear y compartir sus propios manuales de tácticas](/help/use-case-playbooks/playbooks/author.md).

Para obtener más información, lea la [Información general de los manuales de tácticas de casos de uso](/help/use-case-playbooks/playbooks/overview.md), que proporciona una descripción general de la funcionalidad de los manuales de tácticas, su propósito y una demostración completa, incluyendo cómo crear instancias e importar recursos generados en otros entornos de zona protegida.
