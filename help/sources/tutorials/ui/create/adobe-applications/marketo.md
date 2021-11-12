---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Marketo;Conector de Marketo;Origen de Marketo;Marketo
solution: Experience Platform
title: Creación de un conector de origen de Marketo Engage en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Este tutorial proporciona pasos para crear un conector de origen de Marketo Engage en la interfaz de usuario para introducir datos B2B en Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 0%

---

# Cree un [!DNL Marketo Engage] conector de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Marketo Engage] (en lo sucesivo, &quot;el[!DNL Marketo]&quot;) conector de origen en la interfaz de usuario para introducir datos B2B en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Crear y editar esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md): Aprenda a crear y editar esquemas en la interfaz de usuario.
* [Espacios de nombres de identidad](../../../../../identity-service/namespaces.md): Las áreas de nombres de identidad son un componente de [!DNL Identity Service] que sirven de indicadores del contexto al que se refiere una identidad. Una identidad completa incluye un valor de ID y un área de nombres.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Marketo] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `munchkinId` | El ID de Munchkin es el identificador único de un [!DNL Marketo] instancia. |
| `clientId` | El ID de cliente único de su [!DNL Marketo] instancia. |
| `clientSecret` | El secreto de cliente único de su [!DNL Marketo] instancia. |

Para obtener más información sobre la adquisición de estos valores, consulte la [[!DNL Marketo] guía de autenticación](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos de la siguiente sección.

## Conecte su [!DNL Marketo] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL aplicaciones de Adobe] categoría, seleccione **[!UICONTROL Marketo Engage]**. A continuación, seleccione **[!UICONTROL Añadir datos]** para crear un [!DNL Marketo] flujo de datos.

![catálogo](../../../../images/tutorials/create/marketo/catalog.png)

La variable **[!UICONTROL Conectarse al Marketo Engage]** se abre. En esta página puede usar una cuenta nueva o acceder a una existente.

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre de cuenta, una descripción opcional y su [!DNL Marketo] credenciales de autenticación. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new-account](../../../../images/tutorials/create/marketo/new.png)

### Cuenta existente

Para crear un flujo de datos con una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione [!DNL Marketo] cuenta que desee utilizar. Select **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/marketo/existing.png)

## Seleccionar un conjunto de datos

Después de crear el [!DNL Marketo] cuenta, el siguiente paso proporciona una interfaz que puede explorar [!DNL Marketo] conjuntos de datos.

La mitad izquierda de la interfaz es un navegador de directorios, que muestra los 10 [!DNL Marketo] conjuntos de datos. Un funcionamiento completo [!DNL Marketo] la conexión de origen requiere la ingesta de los nueve conjuntos de datos diferentes. Si también utiliza la variable [!DNL Marketo] característica de marketing basado en cuentas (ABM), también debe crear un décimo flujo de datos para introducir la variable [!UICONTROL Cuentas con nombre] conjunto de datos.

>[!NOTE]
>
>A efectos de abreviación, el siguiente tutorial utiliza [!UICONTROL Cuentas con nombre] como ejemplo, pero los pasos descritos a continuación se aplican a cualquiera de los 10 [!DNL Marketo] conjuntos de datos.

Seleccione el conjunto de datos que desee ingerir primero y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Mapa [!DNL Marketo] esquemas para Platform

La variable [!UICONTROL Asignación] aparece un paso que proporciona una interfaz para asignar [!DNL Marketo] esquemas para Platform.

Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede usar un conjunto de datos existente o crear un conjunto de datos nuevo.

### Usar un conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, seleccione el icono del conjunto de datos.

![conjunto de datos existente](../../../../images/tutorials/create/marketo/existing-dataset.png)

La variable **[!UICONTROL Seleccionar conjunto de datos]** se abre. Busque el conjunto de datos con el esquema adecuado que desee utilizar, selecciónelo y, a continuación, seleccione **[!UICONTROL Confirmar]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Usar un nuevo conjunto de datos

Para introducir datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados.

Puede buscar un esquema introduciendo su nombre en la variable **[!UICONTROL Seleccionar esquema]** barra de búsqueda. También puede seleccionar el icono desplegable para ver una lista de los esquemas existentes. También puede seleccionar **[!UICONTROL Búsqueda avanzada]** para acceder a la página de los esquemas existentes, incluidos sus respectivos detalles.

Alternar el **[!UICONTROL Conjunto de datos del perfil]** para habilitar el conjunto de datos de target [!DNL Profile], lo que le permite crear una vista holística de los atributos y comportamientos de una entidad. Datos de todos [!DNL Profile]Los conjuntos de datos habilitados para se incluirán en [!DNL Profile] Los cambios y se aplican cuando guarda el flujo de datos.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Una vez que haya seleccionado un esquema, desplácese hacia abajo para ver el cuadro de diálogo de asignación para empezar a asignar su [!DNL Marketo] los campos del conjunto de datos a los campos XDM de destino correspondientes.

### Asigne un [!DNL Marketo] campos de origen del conjunto de datos para dirigirse a campos XDM

Cada [!DNL Marketo] el conjunto de datos tiene que seguir sus propias reglas de asignación específicas. Consulte lo siguiente para obtener más información sobre cómo asignar [!DNL Marketo] conjuntos de datos para XDM:

* [Actividades](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programas](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Pertenencia a programas](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Compañías](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Listas estáticas](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Pertenencia a listas estáticas](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Cuentas con nombre](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Oportunidades](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Funciones de contacto de oportunidad](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personas](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Select **[!UICONTROL Vista previa de datos]** para ver los resultados de asignación en función del conjunto de datos seleccionado.

![asignación](../../../../images/tutorials/create/marketo/mapping.png)

La variable [!UICONTROL Vista previa] popover proporciona una interfaz para explorar los resultados de asignación de hasta 100 filas de datos de ejemplo del conjunto de datos seleccionado.

![vista previa](../../../../images/tutorials/create/marketo/mapping-preview.png)

Una vez que los campos de origen estén asignados a los campos de destino adecuados, seleccione **[!UICONTROL Cerrar]**.

## Proporcionar detalles de flujo de datos

La variable [!UICONTROL Detalles de flujo de datos] , lo que le permite proporcionar un nombre y una breve descripción del nuevo flujo de datos.

![dataflow-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Active la variable **[!UICONTROL Diagnóstico de errores]** para permitir la generación detallada de mensajes de error para lotes recién ingestados, que puede descargar mediante la API. Para obtener más información, consulte el tutorial sobre [recuperación de diagnóstico de error de ingesta de datos](../../../../../ingestion/quality/error-diagnostics.md).

![errors](../../../../images/tutorials/create/marketo/errors.png)

La variable [!DNL Marketo] El conector utiliza la ingesta por lotes para introducir todos los registros históricos y utiliza la ingesta de flujo continuo para las actualizaciones en tiempo real. Esto permite que el conector continúe transmitiendo durante la ingesta de registros erróneos. Active la variable **[!UICONTROL Ingesta parcial]** alterne y establezca la variable [!UICONTROL Umbral de error %] para evitar que falle el flujo de datos.

**[!UICONTROL Ingesta parcial]** permite introducir datos que contengan errores hasta un umbral determinado. Para obtener más información, consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md).

Una vez que haya proporcionado los detalles del flujo de datos y haya establecido el umbral de error en max, seleccione **[!UICONTROL Siguiente]**.

![ingesta parcial](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Revise el flujo de datos

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta de acceso relevante de la entidad de origen elegida y la cantidad de columnas dentro de esa entidad de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![review](../../../../images/tutorials/create/marketo/review.png)

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se incorporan a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar los flujos de datos, consulte el tutorial en [monitorización de flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

## Eliminar los atributos

Los atributos personalizados de los conjuntos de datos no se pueden ocultar ni eliminar de forma retroactiva. Si desea ocultar o eliminar un atributo personalizado de un conjunto de datos existente, debe crear un nuevo conjunto de datos sin este atributo personalizado, un nuevo esquema XDM y configurar un nuevo flujo de datos para el nuevo conjunto de datos que cree. También debe deshabilitar o eliminar el flujo de datos original que consta del conjunto de datos con el atributo personalizado que desea ocultar o eliminar.

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente empleando la función **[!UICONTROL Eliminar]** en la función [!UICONTROL Flujos de datos] espacio de trabajo. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminación de flujos de datos en la interfaz de usuario](../../delete.md).

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para [!DNL Marketo] datos. Los datos entrantes ahora se pueden usar en servicios de Platform descendentes como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-time Customer Profile]](/help/profile/home.md)
* [Información general del [!DNL Data Science Workspace]](/help/data-science-workspace/home.md)
