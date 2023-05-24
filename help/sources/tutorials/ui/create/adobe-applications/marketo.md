---
title: Crear una conexión de origen y un flujo de datos de Marketo Engage en la IU
description: Este tutorial proporciona pasos para crear una conexión de origen y un flujo de datos de Marketo Engage en la IU para introducir datos B2B en Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: b271d28677543f773fe1ba471fc08574e7c5542b
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Crear un [!DNL Marketo Engage] conexión de origen y flujo de datos en la IU

>[!IMPORTANT]
>
>Antes de crear un [!DNL Marketo Engage] conexión de origen y un flujo de datos, primero debe asegurarse de que tiene [asignado su ID de organización de Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=en) in [!DNL Marketo]. Además, también debe asegurarse de que ha completado [rellenar automáticamente su [!DNL Marketo] Espacios de nombres y esquemas B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) antes de crear una conexión de origen y un flujo de datos.

Este tutorial proporciona los pasos para crear una [!DNL Marketo Engage] (en lo sucesivo, &quot;[!DNL Marketo]&quot;) en la interfaz de usuario para introducir datos B2B en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Utilidad de generación automática de esquemas y áreas de nombres B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): la utilidad de generación automática de esquemas y áreas de nombres B2B le permite utilizar [!DNL Postman] para generar automáticamente valores para los esquemas y áreas de nombres B2B. Primero debe completar los espacios de nombres y esquemas B2B antes de crear un [!DNL Marketo] conexión de origen y flujo de datos.
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Crear y editar esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md): Aprenda a crear y editar esquemas en la interfaz de usuario.
* [Áreas de nombres de identidad](../../../../../identity-service/namespaces.md): las áreas de nombres de identidad son un componente de [!DNL Identity Service] que sirven como indicadores del contexto al que se relaciona una identidad. Una identidad completa incluye un valor de ID y un área de nombres.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Marketo] en Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `munchkinId` | El ID de Munchkin es el identificador único de un [!DNL Marketo] ejemplo. |
| `clientId` | El ID único de cliente de su [!DNL Marketo] ejemplo. |
| `clientSecret` | El secreto de cliente único de su [!DNL Marketo] ejemplo. |

Para obtener más información sobre la adquisición de estos valores, consulte la [[!DNL Marketo] guía de autenticación](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos de la siguiente sección.

## Conecte su [!DNL Marketo] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL aplicaciones de Adobe] categoría, seleccionar **[!UICONTROL Marketo Engage]**. A continuación, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Marketo] flujo de datos.

![catalogar](../../../../images/tutorials/create/marketo/catalog.png)

El **[!UICONTROL Conectar cuenta de Marketo Engage]** página. En esta página, puede utilizar una cuenta nueva o acceder a una cuenta existente.

### Cuenta existente

Para crear un flujo de datos con una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la [!DNL Marketo] cuenta que desea utilizar. Seleccionar **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/marketo/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre de cuenta, una descripción opcional y su [!DNL Marketo] credenciales de autenticación. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/marketo/new.png)

## Selección de un conjunto de datos

Después de crear su [!DNL Marketo] cuenta de, el siguiente paso proporciona una interfaz para que pueda explorar [!DNL Marketo] conjuntos de datos.

La mitad izquierda de la interfaz es un explorador de directorios, que muestra el 10 [!DNL Marketo] conjuntos de datos. Un sistema que funciona a pleno rendimiento [!DNL Marketo] la conexión de origen requiere la ingesta de los nueve conjuntos de datos diferentes. Si también está utilizando la variable [!DNL Marketo] función de marketing basado en cuentas (ABM); a continuación, también debe crear un décimo flujo de datos para introducir la variable [!UICONTROL Cuentas con nombre] conjunto de datos.

>[!NOTE]
>
>Para fines de brevedad, el siguiente tutorial utiliza [!UICONTROL Oportunidades] como ejemplo, pero los pasos descritos a continuación se aplican a cualquiera de los 10 [!DNL Marketo] conjuntos de datos.

Seleccione primero el conjunto de datos que desea introducir y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Proporcionar detalles del flujo de datos {#provide-dataflow-details}

El [!UICONTROL Detalles del flujo de datos] le permite seleccionar si desea utilizar un conjunto de datos existente o uno nuevo. Durante este proceso, también puede configurar las opciones de [!UICONTROL Conjunto de datos de perfil], [!UICONTROL Diagnósticos de error], [!UICONTROL Ingesta parcial], y [!UICONTROL Alertas].

![dataflow-details](../../../../images/tutorials/create/marketo/dataflow-details.png)

>[!BEGINTABS]

>[!TAB Usar un conjunto de datos existente]

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]**. Puede recuperar un conjunto de datos existente mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de conjuntos de datos existentes en el menú desplegable. Una vez seleccionado un conjunto de datos, proporcione un nombre y una descripción para el flujo de datos.

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!TAB Usar un nuevo conjunto de datos]

Para introducir en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y, a continuación, proporcione un nombre del conjunto de datos de salida y una descripción opcional. A continuación, seleccione un esquema al que asignar mediante la variable [!UICONTROL Búsqueda avanzada] o desplazándose por la lista de esquemas existentes en el menú desplegable. Una vez seleccionado un esquema, proporcione un nombre y una descripción para el flujo de datos.

![new-dataset](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!ENDTABS]

### Activar [!DNL Profile] Diagnósticos de error y

A continuación, seleccione la **[!UICONTROL Conjunto de datos de perfil]** para habilitar el conjunto de datos para [!DNL Profile]. Esto le permite crear una vista integral de los atributos y comportamientos de una entidad. Datos de todos [!DNL Profile]Los conjuntos de datos habilitados para se incluirán en [!DNL Profile] Los cambios y se aplican al guardar el flujo de datos.

[!UICONTROL Diagnósticos de error] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] permite la ingesta de datos que contienen errores, hasta un determinado umbral que se define manualmente. Consulte la [resumen de ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

>[!IMPORTANT]
>
>El [!DNL Marketo] source utiliza la ingesta por lotes para introducir todos los registros históricos y utiliza la ingesta de transmisión para actualizaciones en tiempo real. Esto permite que el origen siga transmitiendo mientras se ingieren registros erróneos. Habilite la **[!UICONTROL Ingesta parcial]** alternar y luego establecer [!UICONTROL Umbral de error %] al máximo para evitar que falle el flujo de datos.

![profile-and-errors](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### Habilitar alertas

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la IU](../../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![alertas](../../../../images/tutorials/create/marketo/alerts.png)

### Omitir cuentas no reclamadas al ingerir datos de compañías

Al crear un flujo de datos para introducir datos del conjunto de datos de empresas, puede configurar lo siguiente [!UICONTROL Excluir cuentas no reclamadas] para excluir o incluir cuentas no reclamadas de la ingesta.

Cuando las personas rellenan un formulario, [!DNL Marketo] crea un registro de cuenta fantasma basado en el Nombre de la compañía que no contiene otros datos. Para los nuevos flujos de datos, la opción para excluir las cuentas no reclamadas está habilitada de forma predeterminada. Para los flujos de datos existentes, puede habilitar o deshabilitar la función, con cambios que se aplican a los datos recién ingeridos y no a los datos existentes.

![cuentas no reclamadas](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Asigne su [!DNL Marketo] campos de origen del conjunto de datos a campos XDM de destino

El [!UICONTROL Asignación] Este paso aparece y le proporciona una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Cada [!DNL Marketo] el conjunto de datos tiene sus propias reglas de asignación específicas que seguir. Consulte lo siguiente para obtener más información sobre cómo asignar [!DNL Marketo] conjuntos de datos a XDM:

* [Actividades](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programas](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Pertenencia a programas](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Compañías](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Listas estáticas](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Pertenencia a lista estática](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Cuentas con nombre](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Oportunidades](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Funciones de contacto de oportunidad](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personas](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

![asignación](../../../../images/tutorials/create/marketo/mapping.png)

Una vez que los conjuntos de asignaciones estén listos, seleccione **[!UICONTROL Siguiente]** y espere unos momentos para crear el nuevo flujo de datos.

## Revisión del flujo de datos

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante de la entidad de origen elegida y la cantidad de columnas dentro de esa entidad de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Guardar e introducir]** y deje pasar un tiempo para crear el flujo de datos.

![reseña](../../../../images/tutorials/create/marketo/review.png)

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar flujos de datos, consulte el tutorial sobre [monitorización de flujos de datos en la IU](../../../../../dataflows/ui/monitor-sources.md).

## Eliminar los atributos

Los atributos personalizados de los conjuntos de datos no se pueden ocultar ni eliminar de forma retroactiva. Si desea ocultar o quitar un atributo personalizado de un conjunto de datos existente, debe crear un nuevo conjunto de datos sin este atributo personalizado, un nuevo esquema XDM y configurar un nuevo flujo de datos para el nuevo conjunto de datos que cree. También debe deshabilitar o eliminar el flujo de datos original que consta del conjunto de datos con el atributo personalizado que desea ocultar o quitar.

## Eliminar el flujo de datos

Puede eliminar los flujos de datos que ya no son necesarios o que se crearon incorrectamente utilizando **[!UICONTROL Eliminar]** función disponible en el [!UICONTROL Flujos de datos] workspace. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminación de flujos de datos en la IU](../../delete.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para incorporar [!DNL Marketo] datos. Ahora, los servicios de Platform posteriores pueden utilizar los datos entrantes, como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](/help/profile/home.md)
* [Información general del [!DNL Data Science Workspace]](/help/data-science-workspace/home.md)

## Apéndice {#appendix}

En las secciones siguientes se proporcionan directrices adicionales que puede seguir al utilizar el [!DNL Marketo] origen.

### Mensajes de error en la IU {#error-messages}

Los siguientes mensajes de error se muestran en la interfaz de usuario cuando Platform detecta problemas con la configuración:

#### [!DNL Munchkin ID] no está asignado a la organización adecuada

Se denegará la autenticación si su [!DNL Munchkin ID] no está asignado a la organización de Platform que está utilizando. Configure la asignación entre sus [!DNL Munchkin ID] y su organización mediante el [[!DNL Marketo] interfaz](https://app-sjint.marketo.com/#MM0A1).

![Mensaje de error que muestra que la instancia de Marketo no está asignada correctamente a la organización de Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Falta la identidad principal

Un flujo de datos no se puede guardar ni introducir si falta una identidad principal. Asegúrese de que [existe una identidad principal dentro del esquema XDM](../../../../../xdm/tutorials/create-schema-ui.md), antes de intentar configurar un flujo de datos.

![Mensaje de error que muestra que falta la identidad principal en el esquema XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

