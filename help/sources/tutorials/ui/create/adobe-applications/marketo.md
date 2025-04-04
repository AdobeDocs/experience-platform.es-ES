---
title: Creación de una conexión y un flujo de datos de Marketo Engage Source en la IU
description: Este tutorial proporciona pasos para crear una conexión de origen y un flujo de datos de Marketo Engage en la IU para introducir datos B2B en Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 2%

---

# Crear una conexión de origen y un flujo de datos de [!DNL Marketo Engage] en la interfaz de usuario

>[!IMPORTANT]
>
>Antes de crear una conexión de origen y un flujo de datos de [!DNL Marketo Engage], primero debe asegurarse de que ha [asignado su ID de organización de Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) en [!DNL Marketo]. Además, también debe asegurarse de haber completado [rellenar automáticamente [!DNL Marketo] esquemas y áreas de nombres B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) antes de crear una conexión de origen y un flujo de datos.

Este tutorial proporciona los pasos para crear un conector de origen [!DNL Marketo Engage] (denominado en adelante &quot;[!DNL Marketo]&quot;) en la interfaz de usuario para incorporar datos B2B a Adobe Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Utilidad de generación automática de esquemas y áreas de nombres B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): La utilidad de generación automática de esquemas y áreas de nombres B2B le permite usar [!DNL Postman] para generar automáticamente valores para sus esquemas y áreas de nombres B2B. Primero debe completar los esquemas y áreas de nombres B2B antes de crear una conexión de origen y un flujo de datos de [!DNL Marketo].
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Crear y editar esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md): Aprenda a crear y editar esquemas en la interfaz de usuario.
* [Áreas de nombres de identidad](../../../../../identity-service/features/namespaces.md): Las áreas de nombres de identidad son un componente de [!DNL Identity Service] que sirven como indicadores del contexto al que se relaciona una identidad. Una identidad completa incluye un valor de ID y un área de nombres.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL Marketo] en Experience Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---- | ---- |
| `munchkinId` | El identificador de Munchkin es el identificador único de una instancia de [!DNL Marketo] específica. |
| `clientId` | El ID de cliente único de su instancia de [!DNL Marketo]. |
| `clientSecret` | El secreto de cliente único de su instancia de [!DNL Marketo]. |

Para obtener más información sobre cómo adquirir estos valores, consulte la [[!DNL Marketo] guía de autenticación](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos de la siguiente sección.

## Conectar su cuenta de [!DNL Marketo]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *aplicaciones de Adobe*, seleccione **[!UICONTROL Marketo Engage]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.

![Catálogo de orígenes con el origen de Marketo Engage seleccionado.](../../../../images/tutorials/create/marketo/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta de Marketo Engage]**. En esta página, puede utilizar una cuenta nueva o acceder a una cuenta existente.

>[!BEGINTABS]

>[!TAB Crear una nueva cuenta]

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre, una descripción opcional y tus credenciales.

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta para autenticar una nueva cuenta de Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar del catálogo de cuentas existente.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![Interfaz de cuenta existente donde puede seleccionar una cuenta existente de Marketo.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Selección de un conjunto de datos

Después de crear su cuenta de [!DNL Marketo], el siguiente paso proporciona una interfaz para explorar [!DNL Marketo] conjuntos de datos.

La mitad izquierda de la interfaz es un explorador de directorios que muestra los 10 conjuntos de datos de [!DNL Marketo]. Una conexión de origen [!DNL Marketo] que funciona completamente requiere la ingesta de los nueve conjuntos de datos diferentes. Si también está usando la característica de marketing basado en cuentas (ABM) de [!DNL Marketo], también debe crear un décimo flujo de datos para ingerir el conjunto de datos de [!UICONTROL Cuentas con nombre].

>[!NOTE]
>
>A efectos de brevedad, el siguiente tutorial utiliza [!UICONTROL Oportunidades] como ejemplo, pero los pasos descritos a continuación se aplican a cualquiera de los 10 conjuntos de datos de [!DNL Marketo].

Seleccione el conjunto de datos que desea introducir. Esto actualiza la interfaz para mostrar una previsualización del conjunto de datos. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Interfaz de vista previa](../../../../images/tutorials/create/marketo/preview.png)

## Proporcionar detalles del conjunto de datos y flujo de datos {#provide-dataset-and-dataflow-details}

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos.

### Detalles del conjunto de datos {#dataset-details}

Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los datos que se incorporan correctamente a Experience Platform se almacenan dentro del lago de datos como conjuntos de datos. Durante este paso, puede crear un nuevo conjunto de datos o utilizar uno existente.

>[!BEGINTABS]

>[!TAB Usar un nuevo conjunto de datos]

Para usar un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** y proporcione un nombre y una descripción opcional para su conjunto de datos. También debe seleccionar un esquema del Modelo de datos de experiencia (XDM) al que se adhiera el conjunto de datos.

![La nueva interfaz de selección de conjuntos de datos.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Usar un conjunto de datos existente]

Si ya tiene un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, utilice la opción **[!UICONTROL Búsqueda avanzada]** para ver una ventana de todos los conjuntos de datos de su organización, incluidos sus detalles respectivos, como si están habilitados para la ingesta en el Perfil del cliente en tiempo real o no.

![Interfaz de selección de conjuntos de datos existente.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configuraciones de flujo de datos {#dataflow-configurations}

>[!IMPORTANT]
>
>El origen [!DNL Marketo] utiliza la ingesta por lotes para ingerir todos los registros históricos y la ingesta por secuencias para las actualizaciones en tiempo real. Esto permite que el origen siga transmitiendo mientras se ingieren registros erróneos. Habilite la opción **[!UICONTROL Ingesta parcial]** y, a continuación, establezca el [!UICONTROL Umbral de error %] en el máximo para evitar que el flujo de datos falle.

Si el conjunto de datos está habilitado para Perfil del cliente en tiempo real, durante este paso, puede alternar **[!UICONTROL Conjunto de datos de perfil]** para habilitar los datos para la ingesta de perfiles. También puede usar este paso para habilitar **[!UICONTROL diagnósticos de error]** y **[!UICONTROL ingesta parcial]**.

* **[!UICONTROL Diagnósticos de error]**: seleccione **[!UICONTROL Diagnósticos de error]** para indicar a la fuente que produzca diagnósticos de error a los que pueda hacer referencia posteriormente al supervisar la actividad del conjunto de datos y el estado del flujo de datos.
* **[!UICONTROL Ingesta parcial]**: [La ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) es la capacidad de ingerir datos que contengan errores, hasta un determinado umbral configurable. Esta función le permite introducir correctamente todos los datos exactos en Experience Platform, mientras que todos los datos incorrectos se agrupan por separado con información sobre los motivos por los que no son válidos.

Durante este paso, puede habilitar **[!UICONTROL Flujo de datos de ejemplo]** para limitar la ingesta de datos y evitar costos adicionales que se producen con la ingesta de todos los datos históricos, incluidas las identidades de persona.

>[!BEGINSHADEBOX]

**Guía rápida sobre el uso del flujo de datos de ejemplo**

El flujo de datos de ejemplo es una configuración que puede establecer para su flujo de datos de [!DNL Marketo] a fin de limitar la tasa de ingesta y, a continuación, probar las características de Experience Platform sin tener que ingerir grandes cantidades de datos.

* Habilite el flujo de datos de ejemplo para limitar los datos históricos mediante la ingesta de hasta 100 000 registros (desde el ID de registro más grande) o hasta los últimos 10 días de actividad durante el trabajo de relleno.
* Al utilizar la configuración de flujo de datos de ejemplo para todas las entidades B2B, debe tener en cuenta que es posible que falten algunos registros relacionados porque no se incorpora todo el historial de los datos de origen.

>[!ENDSHADEBOX]

![La sección de configuraciones de flujo de datos de la página de detalles del flujo de datos.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Además, si está asimilando datos del conjunto de datos de compañías, puede habilitar **[!UICONTROL Excluir cuentas no reclamadas]** para excluir las cuentas no reclamadas de la ingesta.

Cuando las personas rellenan un formulario, [!DNL Marketo] crea un registro de cuenta fantasma basado en el Nombre de la compañía que no contiene otros datos. Para los nuevos flujos de datos, la opción para excluir las cuentas no reclamadas está habilitada de forma predeterminada. Para los flujos de datos existentes, puede habilitar o deshabilitar la función, con cambios que se aplican a los datos recién ingeridos y no a los datos existentes.

![Excluir cuentas no reclamadas](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Asignar los campos de origen del conjunto de datos [!DNL Marketo] a los campos XDM de destino

Aparecerá el paso [!UICONTROL Mapping], que le proporcionará una interfaz para asignar los campos de origen del esquema de origen a sus campos XDM de destino adecuados en el esquema de destino.

Cada conjunto de datos [!DNL Marketo] tiene sus propias reglas de asignación específicas que seguir. Consulte lo siguiente para obtener más información sobre cómo asignar [!DNL Marketo] conjuntos de datos a XDM:

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

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación, consulte la [Guía de la interfaz de usuario para la preparación de datos](../../../../../data-prep/ui/mapping.md).

![Interfaz de asignación para datos de Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Una vez que los conjuntos de asignaciones estén listos, seleccione **[!UICONTROL Siguiente]** y espere unos momentos para crear el nuevo flujo de datos.

## Revisión del flujo de datos

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante de la entidad de origen elegida y la cantidad de columnas dentro de esa entidad de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Guardar e ingerir]** y espere un poco para que se cree el flujo de datos.

![Página de revisión en la que puede confirmar los detalles del flujo de datos antes de la ingesta.](../../../../images/tutorials/create/marketo/review.png)

## Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar flujos de datos, consulte el tutorial sobre [supervisión de flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

## Eliminar los atributos

Los atributos personalizados de los conjuntos de datos no se pueden ocultar ni eliminar de forma retroactiva. Si desea ocultar o quitar un atributo personalizado de un conjunto de datos existente, debe crear un nuevo conjunto de datos sin este atributo personalizado, un nuevo esquema XDM y configurar un nuevo flujo de datos para el nuevo conjunto de datos que cree. También debe deshabilitar o eliminar el flujo de datos original que consta del conjunto de datos con el atributo personalizado que desea ocultar o quitar.

## Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo [!UICONTROL Flujos de datos]. Para obtener más información sobre cómo eliminar flujos de datos, consulte el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para introducir datos B2B de su origen de [!DNL Marketo Engage] en Experience Platform.

## Apéndice {#appendix}

Las secciones siguientes proporcionan directrices adicionales que puede seguir al utilizar el origen [!DNL Marketo].

### Mensajes de error en la IU {#error-messages}

Los siguientes mensajes de error se muestran en la interfaz de usuario cuando Experience Platform detecta problemas con la configuración:

#### [!DNL Munchkin ID] no está asignado a la organización apropiada

Se denegará la autenticación si [!DNL Munchkin ID] no está asignado a la organización de Experience Platform que está utilizando. Configure la asignación entre su [!DNL Munchkin ID] y su organización mediante la [[!DNL Marketo] interfaz](https://app-sjint.marketo.com/#MM0A1).

![Mensaje de error que muestra que la instancia de Marketo no está asignada correctamente a la organización de Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Falta la identidad principal

Un flujo de datos no se puede guardar ni introducir si falta una identidad principal. Asegúrese de que [existe una identidad principal dentro del esquema XDM](../../../../../xdm/tutorials/create-schema-ui.md) antes de intentar configurar un flujo de datos.

![Mensaje de error que muestra que falta la identidad principal en el esquema XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

