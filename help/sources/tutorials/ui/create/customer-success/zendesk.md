---
keywords: Experience Platform;Zendesk;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK;zendesk;Zendesk
title: Crear una conexión de origen de Zendesk en la interfaz de usuario
description: Aprenda a crear una conexión de origen de Zendesk mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# (Beta) Cree una [!DNL Zendesk] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Zendesk] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona los pasos para crear una [!DNL Zendesk] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Zendesk] En Platform, debe proporcionar valores para las siguientes credenciales:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| Subdomain | El dominio único específico de su cuenta creado durante el proceso de registro. | `yoursubdomain` |
| Token de acceso | Token de API de Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Para obtener más información sobre la autenticación de [!DNL Zendesk] fuente, consulte la [[!DNL Zendesk] descripción general de origen](../../../../connectors/customer-success/zendesk.md).

![Token de API de Zendesk](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Creación de un esquema de Platform para [!DNL Zendesk]

Antes de crear un [!DNL Zendesk] conexión de origen, también debe asegurarse de crear primero un esquema de Platform para utilizarlo en el origen. Consulte el tutorial sobre [creación de un esquema de Platform](../../../../../xdm/schema/composition.md) para obtener información detallada sobre cómo crear un esquema.

Para obtener más información sobre [!DNL Zendesk] esquema necesario para [!DNL Zendesk Search API], consulte la [límites](#limits) más abajo.

![Crear esquema](../../../../images/tutorials/create/zendesk/schema.png)

## Conecte su [!DNL Zendesk] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *Éxito del cliente* categoría, seleccionar **[!UICONTROL Zendesk]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/zendesk/catalog.png)

El **[!UICONTROL Conectar la cuenta de Zendesk]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la *Zendesk* cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/zendesk/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/zendesk/new.png)

### Seleccionar datos

Una vez autenticado el origen, la página se actualiza a un árbol de esquema interactivo que le permite explorar e inspeccionar la jerarquía de los datos. Seleccionar **[!UICONTROL Siguiente]** para continuar.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Pasos siguientes

Al seguir este tutorial, ha autenticado y creado una conexión de origen entre sus [!DNL Zendesk] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de éxito de los clientes a Platform](../../dataflow/customer-success.md).

## Recursos adicionales

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL Zendesk] origen.

### Validación {#validation}

A continuación se describen los pasos que puede seguir para comprobar que se ha conectado correctamente a [!DNL Zendesk] origen y que [!DNL Zendesk] Los perfiles de se están introduciendo en Platform.

En la IU de Platform, seleccione **[!UICONTROL Conjuntos de datos]** desde la navegación izquierda para acceder a [!UICONTROL Conjuntos de datos] workspace. El [!UICONTROL Actividad de conjunto de datos] La pantalla muestra los detalles de las ejecuciones.

![Página de actividad](../../../../images/tutorials/create/zendesk/dataset-activity.png)

A continuación, seleccione el ID de ejecución del flujo de datos que desea ver para ver detalles específicos sobre esa ejecución del flujo de datos.

![Página de flujo de datos](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Finalmente, seleccione **[!UICONTROL Previsualizar conjunto de datos]** para mostrar los datos que se han introducido.

![Conjunto de datos de Zendesk](../../../../images/tutorials/create/zendesk/preview-dataset.png)

También puede verificar los datos de Platform con los datos de su [!DNL Zendesk] > [!DNL Customers] página.

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Esquema de Zendesk

La tabla siguiente enumera las asignaciones compatibles que deben configurarse para Zendesk.

>[!TIP]
>
>Consulte [API de búsqueda de Zendesk > Exportar resultados de búsqueda](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) para obtener más información sobre la API.

| Fuente | Tipo |
|---|---|
| `results.active` | Booleano |
| `results.alias` | Cadena |
| `results.created_at` | Cadena |
| `results.custom_role_id` | Número entero |
| `results.default_group_id` | Número entero |
| `results.details` | Cadena |
| `results.email` | Cadena |
| `results.external_id` | Número entero |
| `results.iana_time_zone` | Cadena |
| `results.id` | Número entero |
| `results.last_login_at` | Cadena |
| `results.locale` | Cadena |
| `results.locale_id` | Número entero |
| `results.moderator` | Booleano |
| `results.name` | Cadena |
| `results.notes` | Cadena |
| `results.only_private_comments` | Booleano |
| `results.organization_id` | Número entero |
| `results.phone` | Cadena |
| `results.photo` | Cadena |
| `results.report_csv` | Booleano |
| `results.restricted_agent` | Booleano |
| `results.result_type` | Cadena |
| `results.role` | Cadena |
| `results.role_type` | Número entero |
| `results.shared` | Booleano |
| `results.shared_agent` | Booleano |
| `results.shared_phone_number` | Booleano |
| `results.signature` | Cadena |
| `results.suspended` | Booleano |
| `results.ticket_restriction` | Cadena |
| `results.time_zone` | Cadena |
| `results.two_factor_auth_enabled` | Booleano |
| `results.updated_at` | Cadena |
| `results.url` | Cadena |
| `results.verified` | Booleano |

{style="table-layout:auto"}

### Límites {#limits}

* El [API de búsqueda de Zendesk > Exportar resultados de búsqueda](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) devuelve un máximo de 1000 registros por página.
   * El valor de ``filter[type]`` El parámetro se ha establecido en ``user`` y por lo tanto, la conexión de Zendesk solo devuelve usuarios.
   * El número de resultados por página lo administra la variable ``page[size]`` parámetro. El valor se establece en ``100``. Esto se hace para reducir el impacto de las restricciones de reducción de velocidad establecidas por Zendesk.
   * Consulte [Límites](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) y [Paginación](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * También puede consultar [Paginación por listas mediante paginación de cursor](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
