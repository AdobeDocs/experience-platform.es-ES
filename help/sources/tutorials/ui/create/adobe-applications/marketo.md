---
title: Crear una conexión de origen y un flujo de datos de Marketo Engage en la IU
description: Este tutorial proporciona pasos para crear una conexión de origen y un flujo de datos de Marketo Engage en la IU para introducir datos B2B en Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# Crear un [!DNL Marketo Engage] conexión de origen y flujo de datos en la IU

>[!IMPORTANT]
>
>Antes de crear un [!DNL Marketo Engage] conexión de origen y un flujo de datos, primero debe asegurarse de que tiene [asignado su ID de organización de Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Además, también debe asegurarse de que ha completado [rellenar automáticamente su [!DNL Marketo] Espacios de nombres y esquemas B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) antes de crear una conexión de origen y un flujo de datos.

Este tutorial proporciona los pasos para crear una [!DNL Marketo Engage] (en lo sucesivo, &quot;[!DNL Marketo]&quot;) en la interfaz de usuario para introducir datos B2B en Adobe Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Utilidad de generación automática de esquemas y áreas de nombres B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): la utilidad de generación automática de esquemas y áreas de nombres B2B le permite utilizar [!DNL Postman] para generar automáticamente valores para los esquemas y áreas de nombres B2B. Primero debe completar los espacios de nombres y esquemas B2B antes de crear un [!DNL Marketo] conexión de origen y flujo de datos.
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Crear y editar esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md): Aprenda a crear y editar esquemas en la interfaz de usuario.
* [Áreas de nombres de identidad](../../../../../identity-service/features/namespaces.md): las áreas de nombres de identidad son un componente de [!DNL Identity Service] que sirven como indicadores del contexto al que se relaciona una identidad. Una identidad completa incluye un valor de ID y un área de nombres.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Marketo] cuenta en el Experience Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---- | ---- |
| `munchkinId` | El ID de Munchkin es el identificador único de un [!DNL Marketo] ejemplo. |
| `clientId` | El ID único de cliente de su [!DNL Marketo] ejemplo. |
| `clientSecret` | El secreto de cliente único de su [!DNL Marketo] ejemplo. |

Para obtener más información sobre la adquisición de estos valores, consulte la [[!DNL Marketo] guía de autenticación](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos de la siguiente sección.

## Conecte su [!DNL Marketo] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *aplicaciones de Adobe* categoría, seleccionar **[!UICONTROL Marketo Engage]**, y luego seleccione **[!UICONTROL Añadir datos]**.

>[!TIP]
>
>Las fuentes del catálogo de fuentes muestran el **[!UICONTROL Configuración de]** cuando una fuente determinada aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con el origen del Marketo Engage seleccionado.](../../../../images/tutorials/create/marketo/catalog.png)

El **[!UICONTROL Conectar cuenta de Marketo Engage]** página. En esta página, puede utilizar una cuenta nueva o acceder a una cuenta existente.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y proporcione un nombre, una descripción opcional y sus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![La nueva interfaz de cuenta para autenticar una nueva cuenta de Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y, a continuación, seleccione la cuenta que desee utilizar en el catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente donde puede seleccionar una cuenta existente de Marketo.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Selección de un conjunto de datos

Después de crear su [!DNL Marketo] cuenta de, el siguiente paso proporciona una interfaz para que pueda explorar [!DNL Marketo] conjuntos de datos.

La mitad izquierda de la interfaz es un explorador de directorios, que muestra el 10 [!DNL Marketo] conjuntos de datos. Un sistema que funciona a pleno rendimiento [!DNL Marketo] la conexión de origen requiere la ingesta de los nueve conjuntos de datos diferentes. Si también está utilizando la variable [!DNL Marketo] función de marketing basado en cuentas (ABM); a continuación, también debe crear un décimo flujo de datos para introducir la variable [!UICONTROL Cuentas con nombre] conjunto de datos.

>[!NOTE]
>
>Para fines de brevedad, el siguiente tutorial utiliza [!UICONTROL Oportunidades] como ejemplo, pero los pasos descritos a continuación se aplican a cualquiera de los 10 [!DNL Marketo] conjuntos de datos.

Seleccione el conjunto de datos que desea introducir. Esto actualiza la interfaz para mostrar una previsualización del conjunto de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Interfaz de previsualización](../../../../images/tutorials/create/marketo/preview.png)

## Proporcionar detalles del conjunto de datos y flujo de datos {#provide-dataset-and-dataflow-details}

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos {#dataset-details}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los datos que se incorporan correctamente en Experience Platform se almacenan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

>[!BEGINTABS]

>[!TAB Usar un nuevo conjunto de datos]

Para utilizar un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** a continuación, proporcione un nombre y una descripción opcional para el conjunto de datos. También debe seleccionar un esquema del Modelo de datos de experiencia (XDM) al que se adhiera el conjunto de datos.

![La nueva interfaz de selección de conjuntos de datos.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Usar un conjunto de datos existente]

Si ya tiene un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, utilice el **[!UICONTROL Búsqueda avanzada]** para ver una ventana de todos los conjuntos de datos de su organización, incluidos sus respectivos detalles, como si están habilitados para su ingesta en el Perfil del cliente en tiempo real o no.

![Interfaz de selección de conjuntos de datos existente.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configuraciones de flujo de datos {#dataflow-configurations}

>[!IMPORTANT]
>
>El [!DNL Marketo] source utiliza la ingesta por lotes para introducir todos los registros históricos y utiliza la ingesta de transmisión para actualizaciones en tiempo real. Esto permite que el origen siga transmitiendo mientras se ingieren registros erróneos. Habilite la **[!UICONTROL Ingesta parcial]** alternar y luego establecer [!UICONTROL Umbral de error %] al máximo para evitar que falle el flujo de datos.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Conjunto de datos de perfil]** para habilitar los datos para la ingesta de perfiles. También puede utilizar este paso para habilitar **[!UICONTROL Diagnósticos de error]** y **[!UICONTROL Ingesta parcial]**.

* **[!UICONTROL Diagnósticos de error]**: Seleccionar **[!UICONTROL Diagnósticos de error]** para indicar a la fuente que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al monitorizar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Ingesta parcial]**: [Ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos precisos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

Durante este paso, puede activar **[!UICONTROL Flujo de datos de muestra]** para limitar la ingesta de datos y evitar costes adicionales que conlleva la ingesta de todos los datos históricos, incluidas las identidades de las personas.

>[!BEGINSHADEBOX]

**Guía rápida sobre el uso del flujo de datos de ejemplo**

El flujo de datos de ejemplo es una configuración que puede establecer para su [!DNL Marketo] flujo de datos para limitar la tasa de ingesta y, a continuación, probar las funciones de Experience Platform sin tener que ingerir grandes cantidades de datos.

* Habilite el flujo de datos de ejemplo para limitar los datos históricos mediante la ingesta de hasta 100 000 registros (desde el ID de registro más grande) o hasta los últimos 10 días de actividad durante el trabajo de relleno.
* Al utilizar la configuración de flujo de datos de ejemplo para todas las entidades B2B, debe tener en cuenta que es posible que falten algunos registros relacionados porque no se incorpora todo el historial de los datos de origen.

>[!ENDSHADEBOX]

![La sección de configuraciones de flujo de datos de la página de detalles del flujo de datos.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Además, si está introduciendo datos del conjunto de datos de empresas, puede habilitar lo siguiente **[!UICONTROL Excluir cuentas no reclamadas]** para excluir de la ingesta las cuentas no reclamadas.

Cuando las personas rellenan un formulario, [!DNL Marketo] crea un registro de cuenta fantasma basado en el Nombre de la compañía que no contiene otros datos. Para los nuevos flujos de datos, la opción para excluir las cuentas no reclamadas está habilitada de forma predeterminada. Para los flujos de datos existentes, puede habilitar o deshabilitar la función, con cambios que se aplican a los datos recién ingeridos y no a los datos existentes.

![Excluir cuentas no reclamadas](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

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

![Interfaz de asignación para datos de Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Una vez que los conjuntos de asignaciones estén listos, seleccione **[!UICONTROL Siguiente]** y espere unos momentos para crear el nuevo flujo de datos.

## Revisión del flujo de datos

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante de la entidad de origen elegida y la cantidad de columnas dentro de esa entidad de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Guardar e introducir]** y deje pasar un tiempo para crear el flujo de datos.

![La página de revisión donde puede confirmar los detalles del flujo de datos antes de la ingesta.](../../../../images/tutorials/create/marketo/review.png)

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo monitorizar flujos de datos, consulte el tutorial sobre [monitorización de flujos de datos en la IU](../../../../../dataflows/ui/monitor-sources.md).

## Eliminar los atributos

Los atributos personalizados de los conjuntos de datos no se pueden ocultar ni eliminar de forma retroactiva. Si desea ocultar o quitar un atributo personalizado de un conjunto de datos existente, debe crear un nuevo conjunto de datos sin este atributo personalizado, un nuevo esquema XDM y configurar un nuevo flujo de datos para el nuevo conjunto de datos que cree. También debe deshabilitar o eliminar el flujo de datos original que consta del conjunto de datos con el atributo personalizado que desea ocultar o quitar.

## Eliminar el flujo de datos

Puede eliminar los flujos de datos que ya no son necesarios o que se crearon incorrectamente utilizando **[!UICONTROL Eliminar]** función disponible en el [!UICONTROL Flujos de datos] workspace. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminación de flujos de datos en la IU](../../delete.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para introducir datos B2B de su [!DNL Marketo Engage] origen a Experience Platform.

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

