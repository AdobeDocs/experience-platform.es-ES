---
title: Creación de una conexión de Mixpanel Source en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Mixpanel mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 11%

---

# Crear una conexión de origen [!DNL Mixpanel] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Mixpanel] mediante la interfaz de usuario de Adobe Experience Platform Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Para conectar [!DNL Mixpanel] a Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Nombre de usuario | El nombre de usuario de la cuenta de servicio que corresponde con su cuenta de [!DNL Mixpanel]. Consulte la [[!DNL Mixpanel] documentación de cuentas de servicio](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) para obtener más información. | `Test8.6d4ee7.mp-service-account` |
| Contraseña | Contraseña de la cuenta de servicio que corresponde con su cuenta de [!DNL Mixpanel]. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| Identificador de proyecto | Su ID de proyecto [!DNL Mixpanel]. Este ID es necesario para crear una conexión de origen. Consulte la [[!DNL Mixpanel] documentación sobre la configuración del proyecto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) y la [[!DNL Mixpanel] guía sobre la creación y administración de proyectos](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) para obtener más información. | `2384945` |
| Zona horaria | Zona horaria que corresponde al proyecto [!DNL Mixpanel]. Se requiere zona horaria para crear una conexión de origen. Consulte la [documentación sobre la configuración del proyecto Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) para obtener más información. | `Pacific Standard Time` |

Para obtener más información sobre cómo autenticar el origen de [!DNL Mixpanel], consulte la [[!DNL Mixpanel] descripción general del origen](../../../../connectors/analytics/mixpanel.md).

## Conectar su cuenta de [!DNL Mixpanel]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *Analytics*, seleccione [!DNL Mixpanel] y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Mixpanel]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Mixpanel] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Seleccione el ID de proyecto y la zona horaria {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Establecer una zona horaria para la ingesta de Mixpanel"
>abstract="La zona horaria debe ser la misma que la configuración de la zona horaria del perfil de Mixpanel, ya que Platform utiliza la zona horaria del proyecto designada para ingerir datos relevantes de Mixpanel. Mixpanel ajustará su zona horaria para coordinarse con la zona horaria del proyecto antes de registrar el evento en un almacén de datos de Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=es#project-id-and-timezone" text="Obtenga más información en la documentación"

Una vez que el origen esté autenticado, proporcione el ID de proyecto y la zona horaria y luego seleccione **[!UICONTROL Seleccionar]**.

La zona horaria que designe antes de ingerir los datos de [!DNL Mixpanel] en Platform debe ser la misma que la configuración de zona horaria del perfil [!DNL Mixpanel]. Cualquier cambio en la zona horaria de los datos solo se aplicará a los nuevos eventos y los eventos antiguos permanecerán en la zona horaria que haya designado anteriormente. [!DNL Mixpanel] se adapta al horario de verano y ajustará correctamente la marca de tiempo de ingesta. Para obtener más información sobre cómo afectan las zonas horarias a los datos, consulte la guía [!DNL Mixpanel] sobre [administración de zonas horarias para proyectos](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Después de unos momentos, la interfaz correcta se actualiza a un panel de previsualización, lo que le permite inspeccionar el esquema antes de crear un flujo de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![configuración](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Mixpanel]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de análisis en la plataforma](../../dataflow/analytics.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al usar el origen [!DNL Mixpanel].

### Validación {#validation}

A continuación se describen los pasos que puede seguir para comprobar que ha conectado correctamente el origen de [!DNL Mixpanel] y que se están introduciendo [!DNL Mixpanel] eventos en Platform.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Conjuntos de datos]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Conjuntos de datos]. La pantalla [!UICONTROL Actividad de conjunto de datos] muestra los detalles de las ejecuciones.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

A continuación, seleccione el ID de ejecución del flujo de datos que desea ver para ver detalles específicos sobre esa ejecución del flujo de datos.

![monitorización de flujo de datos](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Finalmente, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para mostrar los datos ingeridos.

![previsualización-conjunto de datos](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Puede comprobar estos datos con los datos de la página [!DNL Mixpanel] > [!DNL Events]. Consulte el [[!DNL Mixpanel] documento sobre Eventos](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) para obtener más información.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Esquema del panel mixto

En la tabla siguiente se enumeran las asignaciones compatibles que deben configurarse para [!DNL Mixpanel].

>[!TIP]
>
>Consulte [API de exportación de eventos > Descargar](https://developer.mixpanel.com/reference/raw-event-export) para obtener más información sobre la API.


| Fuente | Tipo |
|---|---|
| `distinct_id` | cadena |
| `event_name` | cadena |
| `import` | Booleano |
| `insert_id` | cadena |
| `item_id` | cadena |
| `item_name` | cadena |
| `item_price` | cadena |
| `mp_api_endpoint` | cadena |
| `mp_api_timestamp_ms` | entero |
| `mp_processing_time_ms` | entero |
| `time` | entero |

### Límites {#limits}

* Tiene un máximo de 100 consultas simultáneas y 60 consultas por hora, tal como se indica en [Exportar límites de velocidad de API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
