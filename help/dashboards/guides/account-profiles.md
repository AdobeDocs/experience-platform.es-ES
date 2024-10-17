---
title: Panel de perfiles de cuenta
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los perfiles de cuenta B2B de su organización.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8caa10010109f9936271cb45a2166455f3678687
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 5%

---

# Panel de perfiles de cuenta

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los perfiles de la cuenta, tal como se capturan durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel [!UICONTROL Perfiles de cuenta] en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Este documento proporciona información general sobre las características del panel [!UICONTROL Perfiles de cuenta] y detalla la información estándar disponible. Consulte la [[!UICONTROL Guía de la interfaz de usuario de los perfiles de cuenta]](../../rtcdp/accounts/account-profile-ui-guide.md) para obtener información detallada sobre las funciones disponibles.

## Introducción

Debe tener derecho a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) para acceder al tablero de [!UICONTROL Perfiles de cuenta] B2B.

## Datos de perfiles de cuenta {#data}

El panel [!UICONTROL Perfiles de cuenta] muestra una instantánea de la información de la cuenta unificada. Esta información de cuenta proviene de varias fuentes en sus canales de marketing y en los diversos sistemas que su organización utiliza actualmente para almacenar la información de la cuenta del cliente.

Los datos de perfil de la instantánea muestran los datos exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos, y el panel [!UICONTROL Perfiles de cuenta] no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Explorar el panel [!UICONTROL Perfiles de cuenta] {#explore}

Para ir al panel de [!UICONTROL Perfiles de cuenta] en la interfaz de usuario de Platform, seleccione **[!UICONTROL Perfiles]** en [!UICONTROL Cuentas] en el panel de navegación izquierdo.

![Se resaltó la interfaz de usuario de Platform con los perfiles de cuenta en la navegación izquierda y se mostró la ficha de información general.](../images/account-profiles/account-profiles-dashboard.png)

Desde el panel de [!UICONTROL Perfiles de cuenta], puede [examinar los perfiles de cuenta introducidos en su organización](#browse-account-profiles) o [ver la totalidad de los datos del perfil de cuenta de un vistazo mediante widgets](#standard-widgets).

### Filtro de fecha {#date-filter}

La pestaña [!UICONTROL Información general] está compuesta por widgets que proporcionan métricas de solo lectura para transmitir información importante sobre los perfiles de tu cuenta. Seleccione el icono de calendario o las fechas para cambiar el filtro de fecha global de los widgets.

>[!IMPORTANT]
>
>El intervalo de fechas que seleccione en el calendario desplegable afecta a todas las perspectivas, excepto a los dos widgets de puntuación predictivos ([distribución](#predictive-scoring-distribution) y [factores más influyentes](#predictive-scoring-top-influential-factors)).

![Pestaña Información general de perfiles de cuenta con el selector de fecha y el icono de filtro resaltados.](../images/account-profiles/date-filter.png)

### Configurar el servicio de coincidencia de cliente potencial con cuenta {#lead-to-account-matching-service}

Seleccione **[!UICONTROL Configuración]** para configurar el servicio de coincidencia de cliente potencial con cuenta desde el cuadro de diálogo [!UICONTROL Configuración de la cuenta]. Para obtener información detallada sobre cómo configurar la coincidencia de cliente potencial con cuenta, consulte la [guía de la interfaz de usuario](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Para obtener más información sobre la coincidencia de cliente potencial con cuenta, consulte [coincidencia de cliente potencial con cuenta en la documentación de Real-Time CDP B2B](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Panel de perfiles de cuenta con la configuración resaltada.](../images/account-profiles/settings.png)

## Examinar perfiles de cuenta {#browse-account-profiles}

Desde la pestaña [!UICONTROL Examinar], puede buscar y ver los perfiles de cuenta de solo lectura ingeridos en su organización. Utilice un ID de cuenta de un origen empresarial conectado o introduzca directamente los detalles de origen. Desde esta área de trabajo, puede ver información importante que pertenece al perfil de la cuenta, como, por ejemplo, su nombre, sector, ingresos y audiencia.

Seleccione el [!UICONTROL ID de perfil] de los resultados mostrados en la ficha [!UICONTROL Examinar] para abrir la ficha [!UICONTROL Detalles] para el perfil de cuenta.

![La ficha de exploración Perfiles de cuenta muestra los resultados y resalta el identificador de perfil.](../images/account-profiles/account-profiles-browse-tab.png)

La información del perfil de cuenta que se muestra en la ficha [!UICONTROL Detalles] se ha combinado a partir de varios fragmentos de perfil para formar una sola vista de la cuenta individual. Consulte la documentación sobre [examinar perfiles de cuenta en Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) para obtener más información sobre las funciones de visualización de perfiles de cuenta en la interfaz de usuario de Platform.

## Widgets estándar {#standard-widgets}

>[!CONTEXTUALHELP]
>id="platform_dashboards_accountprofiles_customersperaccountoverview"
>title="Información general sobre clientes por cuenta"
>abstract="Este widget de obtención de detalles proporciona perspectivas sobre la estructura de los datos B2B. Ayuda a identificar cuántos perfiles de cuenta no tienen perfiles de cliente vinculados o tienen uno o más perfiles de cliente asociados a ellos.<ul><li>Clientes directos: son perfiles de clientes vinculados directamente a una cuenta a través de la ruta `personComponents`.</li><li>Clientes indirectos: son perfiles de clientes vinculados a una cuenta a través de la ruta `Account-Person`.</li></ul>"

Adobe proporciona widgets estándar que puede utilizar para visualizar diferentes métricas relacionadas con los perfiles de la cuenta.

>[!IMPORTANT]
>
>Si no proporciona un filtro de fecha, el comportamiento predeterminado de las perspectivas analiza los datos agregados desde el año anterior hasta hoy.

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [Perfiles de cuenta añadidos](#account-profiles-added)
* [Nuevas cuentas por sector](#accounts-by-industry)
* [Nuevas cuentas por tipo](#accounts-by-type)
* [Nuevas oportunidades por función de persona](#opportunities-by-person-role)
* [Nuevas oportunidades por ingresos](#opportunities-by-revenue)
* [Nuevas oportunidades por estado y etapa](#opportunities-by-status-&-stage)
* [Nuevas oportunidades ganadas](#opportunities-won)
* [Oportunidades añadidas](#opportunities-added)
* [Distribución de puntuación predictiva](#predictive-scoring-distribution)
* [Factores más influyentes de la puntuación predictiva](#predictive-scoring-top-influential-factors)

### Perfiles de cuenta añadidos {#account-profiles-added}

El widget [!UICONTROL Perfiles de cuenta agregados] usa un gráfico de líneas para mostrar el número de perfiles de cuenta agregados cada día durante un período de tiempo. Utilice el filtro de fecha global situado en la parte superior del panel para determinar el periodo de análisis. Si no se proporciona ningún filtro de fecha, el comportamiento predeterminado enumera los perfiles de cuenta agregados para el año anterior a hoy. Los resultados se pueden utilizar para deducir una tendencia en el número de perfiles de cuenta añadidos.

![Widget agregado de perfiles de cuenta.](../images/account-profiles/account-profiles-added.png)

### Nuevas cuentas por sector {#accounts-by-industry}

El widget [!UICONTROL Nuevas cuentas por sector] muestra el número total de cuentas en una sola métrica dentro de un gráfico circular. El gráfico de anillo ilustra la composición relativa de las diferentes industrias que componen este total. Una clave codificada por colores proporciona un desglose de todas las industrias incluidas. Los recuentos individuales de cada sector se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico circular.

![Widget de nuevas cuentas por sector.](../images/account-profiles/new-accounts-by-industry.png)

### Nuevas cuentas por tipo {#accounts-by-type}

El widget [!UICONTROL Nuevas cuentas por tipo] muestra el número total de cuentas en una sola métrica dentro de un gráfico circular. El gráfico de anillo ilustra la composición relativa de los distintos tipos de cuenta que componen este total. Una clave con códigos de color proporciona un desglose de todos los tipos de cuenta incluidos. Los recuentos individuales de cada tipo de cuenta se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico circular.

![Widget de nuevas cuentas por tipo.](../images/account-profiles/new-accounts-by-type.png)

### Nuevas oportunidades por función de persona {#opportunities-by-person-role}

El widget [!UICONTROL Nuevas oportunidades por función de persona] muestra la cantidad total de tus oportunidades en una sola métrica dentro de un gráfico circular. El gráfico de anillo ilustra la composición relativa de las funciones que componen este número total de oportunidades. Una clave codificada por colores proporciona un desglose de todas las funciones incluidas. Los recuentos individuales de cada rol se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico de anillo.

>[!NOTE]
>
>El error [!UICONTROL No se encontraron datos] o [!UICONTROL No se pudo cargar] se debe a que la tabla de puente &quot;Oportunidad-Persona&quot; no se usa en su esquema. Si su perspectiva muestra uno de estos errores, compruebe el esquema de unión y asegúrese de que el grupo de campos Oportunidad-Persona esté introduciendo datos.

![Widget de nuevas oportunidades por función de persona.](../images/account-profiles/new-opportunities-by-person-role.png)

### Nuevas oportunidades por ingresos {#opportunities-by-revenue}

El widget [!UICONTROL Nuevas oportunidades por ingresos] usa un gráfico de barras para ilustrar la cantidad total estimada de ingresos generados por sus oportunidades. El widget admite hasta seis oportunidades.

Para ver un cuadro de diálogo que contiene el total de ingresos específico de una oportunidad, utilice el cursor para pasar el ratón sobre barras individuales.

![Widget de nuevas oportunidades por ingresos.](../images/account-profiles/new-opportunities-by-revenue.png)

### Nuevas oportunidades por estado y fase {#opportunities-by-status-&-stage}

Este widget utiliza un gráfico de barras para ilustrar la cantidad de oportunidades que están abiertas o cerradas en todas las etapas del canal de marketing/ventas. El widget utiliza colores para diferenciar el escenario de las oportunidades. Una clave codificada por colores indica las etapas disponibles para las oportunidades.

![Las nuevas oportunidades por estado y widget de fase.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Nuevas oportunidades ganadas {#opportunities-won}

El widget [!UICONTROL Nuevas oportunidades ganadas] muestra el número total de oportunidades que se finalizaron correctamente en una sola métrica dentro de un gráfico circular. El gráfico de anillo ilustra la composición relativa de las oportunidades que se ganan o no. Una clave codificada por colores distingue entre oportunidades ganadas y no ganadas. Los recuentos individuales de cada rol se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico de anillo.

![El widget de nuevas oportunidades ganadas.](../images/account-profiles/new-opportunities-won.png)

### Oportunidades añadidas {#opportunities-added}

El widget [!UICONTROL Oportunidades agregadas] usa un gráfico de líneas para mostrar el número de oportunidades agregadas cada día durante un período de tiempo. Utilice el filtro de fecha global situado en la parte superior del panel para determinar el periodo de análisis. Si no se proporciona ningún filtro de fecha, el comportamiento predeterminado enumera las oportunidades agregadas para el año anterior a hoy. Los resultados se pueden utilizar para deducir una tendencia en el número de oportunidades agregadas.

<!-- Link to date filter documentation from Annamalai -->

![Widget de oportunidades agregadas.](../images/account-profiles/opportunities-added.png)

### Distribución de puntuación predictiva {#predictive-scoring-distribution}

El widget [!UICONTROL Distribución de puntuación predictiva] muestra la distribución de puntuación de todos los perfiles de cuenta para ayudarle a comprender el estado de su canalización de ventas de un vistazo. Los datos de puntuación se transmiten mediante un gráfico circular y un gráfico de columnas.

El gráfico de anillo ilustra la proporción de los perfiles totales de la cuenta en cada uno de los bloques de compra alta, media y baja. La clave proporciona más detalles sobre las secciones con códigos de color, incluidos los intervalos del bloque de puntuación y el número de perfiles de cuenta en ese intervalo.

El gráfico de columnas proporciona un desglose de puntuación más granular. Cada columna muestra el número de perfiles de cuenta en cada uno de los 20 bloques de incremento de cinco puntos.

El menú desplegable dentro del widget permite seleccionar el modelo de puntuación de la cuenta.

>[!NOTE]
>
>Los filtros de intervalo de fechas globales no se aplican a las perspectivas de puntuación predictiva. Los widgets de puntuación predictiva analizan los datos en función del modelo de puntuación de cuenta seleccionado en la lista desplegable.

![Widget de distribución de puntuación predictiva.](../images/account-profiles/predictive-scoring-distribution.png)

### Factores más influyentes de la puntuación predictiva {#predictive-scoring-top-influential-factors}

El widget [!UICONTROL Factores más influyentes de puntuación predictiva] le ayuda a comprender los factores más significativos que impulsan las puntuaciones para cada bloque de tendencia.

Este widget muestra los principales factores influyentes para cada uno de los bloques de alta, media y baja tendencia. Una barra para cada factor influyente indica el porcentaje de los perfiles de cuenta en ese bloque de tendencia que contiene el factor influyente específico.

El menú desplegable dentro del widget permite seleccionar el modelo de puntuación de la cuenta.

>[!NOTE]
>
>Los filtros de intervalo de fechas globales no se aplican a las perspectivas de puntuación predictiva. Los widgets de puntuación predictiva analizan los datos en función del modelo de puntuación de cuenta seleccionado en la lista desplegable.

![Widget de factores influyentes principales de puntuación predictiva.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Error de no se pueden cargar los datos {#errors}

Si un widget muestra *[!UICONTROL No se puede cargar. Inténtelo de nuevo.]* esto se debe a que no hay datos disponibles para la entidad B2B. Por ejemplo, el widget mostrado debajo de [!UICONTROL Nuevas oportunidades por rol de persona], muestra el mensaje &quot;[!UICONTROL No se puede cargar. Inténtelo de nuevo.]&quot;, ya que esta zona protegida no tiene datos de oportunidades disponibles.

![Error de no se puede cargar la perspectiva.](../images/account-profiles/unable-to-load.png)

Para resolver el problema, debe ingerir datos de entidad B2B, como datos de *persona de la oportunidad*, en la zona protegida. Después de 48 horas, los datos se reflejan en los widgets.

## Pasos siguientes

Al seguir este documento, debería saber cómo localizar el panel de [!UICONTROL Perfiles de cuenta] y también comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con perfiles de cuenta como parte de los datos B2B en la interfaz de usuario de Experience Platform, consulte [descripción general de los perfiles de cuenta](../../rtcdp/accounts/account-profile-overview.md) para Adobe Real-Time CDP, edición B2B.
