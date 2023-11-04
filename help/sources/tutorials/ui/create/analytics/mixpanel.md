---
title: Creación de una conexión de origen de Mixpanel en la IU
description: Obtenga información sobre cómo crear una conexión de origen de Mixpanel mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 10%

---

# Crear un [!DNL Mixpanel] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Mixpanel] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Para poder conectarse [!DNL Mixpanel] En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Nombre de usuario | El nombre de usuario de la cuenta de servicio que corresponde con su [!DNL Mixpanel] cuenta. Consulte la [[!DNL Mixpanel] documentación de cuentas de servicio](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) para obtener más información. | `Test8.6d4ee7.mp-service-account` |
| Una contraseña | La contraseña de la cuenta de servicio que corresponde con su [!DNL Mixpanel] cuenta. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID del proyecto | Su [!DNL Mixpanel] ID del proyecto. Este ID es necesario para crear una conexión de origen. Consulte la [[!DNL Mixpanel] documentación de configuración del proyecto](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) y el [[!DNL Mixpanel] guía sobre creación y administración de proyectos](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) para obtener más información. | `2384945` |
| Zona horaria | La zona horaria que corresponde a su [!DNL Mixpanel] proyecto. Se requiere zona horaria para crear una conexión de origen. Consulte la [Documentación de configuración del proyecto Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) para obtener más información. | `Pacific Standard Time` |

Para obtener más información sobre la autenticación de [!DNL Mixpanel] fuente, consulte la [[!DNL Mixpanel] descripción general de origen](../../../../connectors/analytics/mixpanel.md).

## Conecte su [!DNL Mixpanel] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *Analytics* categoría, seleccionar [!DNL Mixpanel], y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

El **[!UICONTROL Conectar cuenta de Mixpanel]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Mixpanel] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Seleccione el ID de proyecto y la zona horaria {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Establecer una zona horaria para la ingesta de Mixpanel"
>abstract="La zona horaria debe ser la misma que la configuración de la zona horaria del perfil de Mixpanel, ya que Platform utiliza la zona horaria del proyecto designada para ingerir datos relevantes de Mixpanel. Mixpanel ajustará su zona horaria para coordinarse con la zona horaria del proyecto antes de registrar el evento en un almacén de datos de Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html#project-id-and-timezone" text="Obtenga más información en la documentación"

Una vez autenticado el origen, proporcione el ID de proyecto y la zona horaria y, a continuación, seleccione **[!UICONTROL Seleccionar]**.

La zona horaria que designe antes de ingerir su [!DNL Mixpanel] Los datos de Platform deben ser los mismos que los de [!DNL Mixpanel] configuración de zona horaria de perfil. Cualquier cambio en la zona horaria de los datos solo se aplicará a los nuevos eventos y los eventos antiguos permanecerán en la zona horaria que haya designado anteriormente. [!DNL Mixpanel] adapta el horario de verano y ajustará correctamente la marca de tiempo de ingesta. Para obtener más información sobre cómo afectan las zonas horarias a los datos, consulte la [!DNL Mixpanel] guía sobre [administración de zonas horarias para proyectos](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Después de unos momentos, la interfaz correcta se actualiza a un panel de previsualización, lo que le permite inspeccionar el esquema antes de crear un flujo de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![configuración](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Mixpanel] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de análisis en Platform](../../dataflow/analytics.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL Mixpanel] origen.

### Validación {#validation}

A continuación se describen los pasos que puede seguir para comprobar que se ha conectado correctamente a [!DNL Mixpanel] origen y que [!DNL Mixpanel] eventos se están introduciendo en Platform.

En la IU de Platform, seleccione **[!UICONTROL Conjuntos de datos]** desde la barra de navegación izquierda para acceder a [!UICONTROL Conjuntos de datos] workspace. El [!UICONTROL Actividad de conjunto de datos] La pantalla muestra los detalles de las ejecuciones.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

A continuación, seleccione el ID de ejecución del flujo de datos que desea ver para ver detalles específicos sobre esa ejecución del flujo de datos.

![control de flujo de datos](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Finalmente, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para mostrar los datos que se han introducido.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Puede comprobar estos datos con los datos de la [!DNL Mixpanel] > [!DNL Events] página. Consulte la [[!DNL Mixpanel] documento sobre eventos](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) para obtener más información.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Esquema del panel mixto

En la tabla siguiente se enumeran las asignaciones compatibles que deben configurarse para [!DNL Mixpanel].

>[!TIP]
>
>Consulte [API de exportación de eventos > Descargar](https://developer.mixpanel.com/reference/raw-event-export) para obtener más información sobre la API.


| Fuente | Tipo |
|---|---|
| `distinct_id` | string |
| `event_name` | string |
| `import` | Booleano |
| `insert_id` | string |
| `item_id` | string |
| `item_name` | string |
| `item_price` | string |
| `mp_api_endpoint` | string |
| `mp_api_timestamp_ms` | entero |
| `mp_processing_time_ms` | entero |
| `time` | entero |

### Límites {#limits}

* Tiene un máximo de 100 consultas simultáneas y 60 consultas por hora, como se indica en [Exportar límites de velocidad de API](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
