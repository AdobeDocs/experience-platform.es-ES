---
title: Conexión de perfiles de usuario de Algolia a Experience Platform mediante la IU
description: Aprenda a conectar los datos de intención de usuario de Algolia a Adobe Experience Platform
exl-id: d4c936a7-4983-4a12-a813-03b672116e44
source-git-commit: 2ba1f82fbefd9a7af7a1cf305ccafcb2c7814d7b
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# Ingesta de datos de [!DNL Algolia User Profiles] en Experience Platform mediante la IU

Este tutorial lo guiará a través de la ingesta de datos de su cuenta de [!DNL Algolia User Profiles] en Adobe Experience Platform mediante la interfaz de usuario.

## Introducción 

>[!IMPORTANT]
>
>Antes de comenzar, asegúrese de completar los requisitos previos descritos en la [[!DNL Algolia User Profiles] descripción general](../../../../connectors/data-partners/algolia-user-profiles.md#prerequisites).

Este tutorial supone que está familiarizado con los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): el marco estandarizado que utiliza Experience Platform para organizar los datos de la experiencia del cliente.

   * [Conceptos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información acerca de la composición de esquemas, incluidos los principios clave y las prácticas recomendadas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Fuentes](../../../../home.md): ingrese datos de varias fuentes y use los servicios de Experience Platform para estructurar, etiquetar y mejorar los datos.

### Recopilar credenciales necesarias

Para conectar [!DNL Algolia] a Adobe Experience Platform, proporcione las siguientes credenciales:

| Credencial | Descripción |
| -------------- | ----------------------------------------------------------------------------------------- |
| ID de aplicación | El identificador único asignado a su cuenta de [!DNL Algolia]. |
| Clave de API | La credencial para autenticar y autorizar solicitudes de API a los servicios de [!DNL Algolia]. |

Para obtener más información, consulte la [!DNL Algolia] [documentación de autenticación](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

## Conectar su cuenta de [!DNL Algolia]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para abrir el área de trabajo *[!UICONTROL Fuentes]*. Use el panel *[!UICONTROL Categorías]* o la barra de búsqueda para encontrar el origen deseado.

Para conectar a [!DNL Algolia], elige la tarjeta de origen de **[!UICONTROL Algolia]** en *[!UICONTROL Socios de datos e identidad]* y selecciona **[!UICONTROL Configurar]**.

>[!TIP]
>
> Si un origen aún no tiene una cuenta autenticada, muestra la opción **[!UICONTROL Configurar]**. Una vez autenticado, esto cambia a **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con el origen de Perfiles de usuario de Algolia seleccionado.](../../../../images/tutorials/create/algolia/user-profiles/catalog.png)

## Autenticación

### Usar una cuenta existente

Para usar una cuenta existente, elija **[!UICONTROL Cuenta existente]** y seleccione la cuenta [!DNL Algolia User Profiles] que desee usar. Luego selecciona **[!UICONTROL Siguiente]**.

![Interfaz de cuenta existente.](../../../../images/tutorials/create/algolia/user-profiles/existing-account.png)

### Crear una nueva cuenta

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y luego escribe un nombre, una descripción opcional y tus credenciales de [!DNL Algolia]. Seleccione **[!UICONTROL Conectarse al origen]** y esperar a que se establezca la conexión.

![Interfaz de la nueva cuenta.](../../../../images/tutorials/create/algolia/user-profiles/new-account.png)

## Adición de datos

Una vez creada la cuenta de [!DNL Algolia User Profiles], aparecerá el paso **[!UICONTROL Agregar datos]**. Utilícelo para seleccionar y previsualizar datos de perfil de usuario para su ingesta.

* A la izquierda, introduzca **[!UICONTROL Índices]** y **[!UICONTROL Afinidad(es)]** opcionales.
* A la derecha, previsualice hasta 100 filas de perfiles de usuario.

Una vez finalizado, seleccione **[!UICONTROL Siguiente]**.

![Paso para seleccionar datos del flujo de trabajo.](../../../../images/tutorials/create/algolia/user-profiles/select-data.png)

## Proporcionar detalles del flujo de datos

Si utiliza un conjunto de datos existente, elija uno asociado a un esquema que incluya el grupo de campos [!DNL Algolia Profile]. Asegúrese de que el campo [!DNL Algolia User Token] esté usando el área de nombres de identidad [!DNL Algolia User Token].  Si [!DNL Algolia User Token] no se ha creado ni asignado actualmente, se proporcionan las instrucciones a continuación.

![Paso del conjunto de datos existente.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-existing-dataset.png)

Si crea un nuevo conjunto de datos, seleccione un esquema con el grupo de campos [!DNL Algolia Profile].

![El nuevo paso del conjunto de datos.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-new-dataset.png)

### Crear área de nombres de identidad [!DNL Algolia User Token]

Deberá crear el área de nombres de identidad [!DNL Algolia User Token] si aún no existe en su organización.

Use el panel de navegación izquierdo y seleccione **[!UICONTROL Identidades]** para acceder al área de trabajo de la interfaz de usuario del [servicio de identidad](../../../../../identity-service/home.md) y, a continuación, seleccione **[!UICONTROL Crear área de nombres de identidad]**.

A continuación, proporcione un **[!UICONTROL Nombre para mostrar]** y un **[!UICONTROL Símbolo de identidad]** para su área de nombres personalizada. Durante este paso, también debe configurar el tipo del área de nombres. Cuando termine, seleccione **[!UICONTROL Crear]**.

![Crear pantalla del área de nombres de identidad.](../../../../images/tutorials/create/algolia/user-profiles/aep-identity-inputs.png)

| Configuración de área de nombres personalizada | Valor |
| --- | --- |
| **[!UICONTROL Nombre para mostrar]** | [!DNL Algolia User Token] |
| **[!UICONTROL Símbolo de identidad]** | [!DNL AlgoliaUserToken] |
| **[!UICONTROL Seleccionar un tipo]** | [!DNL Cookie ID] |

Una vez agregado, el área de nombres aparece en la lista. Ahora puede aplicarlo en el esquema.

![Creación correcta del área de nombres de identidad de Algolia.](../../../../images/tutorials/create/algolia/user-profiles/aep-algolia-user-token-identity.png)

### Aplicar el área de nombres al esquema

Utilice la barra de navegación izquierda y seleccione **[!UICONTROL Esquemas]** para acceder al área de trabajo de la interfaz de usuario de [Esquemas](../../../../../xdm/ui/overview.md). Utilice el espacio de trabajo de esquemas para crear o actualizar un esquema con el grupo de campos [!DNL Algolia Profile Details]. A continuación, vaya al campo **[!UICONTROL Token de usuario]** y utilice el carril derecho para seleccionar el cuadro **[!UICONTROL Identidad]**. Además, utilice el cuadro de entrada para definir el área de nombres de identidad [!DNL Algolia User Token]. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Establecer identidad en el campo.](../../../../images/tutorials/create/algolia/user-profiles/set-set-identity-on-field.png)

Una vez que el campo **[!UICONTROL Token de usuario]** se asigna al área de nombres de identidad [!DNL Algolia User Token], la identidad aparece en el perfil de usuario de cualquier perfil.

![Interfaz de perfil de usuario.](../../../../images/tutorials/create/algolia/user-profiles/user-profile.png)

## Asignación de campos de datos a un esquema XDM

Utilice la interfaz de asignación para asignar los datos de origen a los campos de esquema. Para obtener más información, consulte la [guía de asignación](../../../../../data-prep/ui/mapping.md).

![Paso de asignación.](../../../../images/tutorials/create/algolia/user-profiles/mapping.png)

## Programar ejecuciones de ingesta

A continuación, utilice la interfaz de programación para definir la programación de ingesta del flujo de datos.

![Paso de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/scheduling.png)

| Configuración de programación | Descripción |
| --- | --- |
| Frecuencia | Configure la frecuencia para indicar con qué frecuencia debe ejecutarse el flujo de datos. Puede establecer su frecuencia en: <ul><li>**Una vez**: establezca su frecuencia en `once` para crear una ingesta única. Las configuraciones para intervalo y relleno no están disponibles al crear un flujo de datos de ingesta único. De forma predeterminada, la frecuencia de programación se establece en una vez.</li><li>**Minuto**: establezca su frecuencia en `minute` para programar el flujo de datos e ingerir datos por minuto.</li><li>**Hora**: establezca su frecuencia en `hour` para programar el flujo de datos e ingerir datos por hora.</li><li>**Día**: Establezca su frecuencia en `day` para programar su flujo de datos e ingerir datos por día.</li><li>**Semana**: establezca su frecuencia en `week` para programar el flujo de datos e ingerir datos por semana.</li></ul> |
| Intervalo | Una vez seleccionada una frecuencia, puede configurar la configuración del intervalo para establecer el lapso de tiempo entre cada ingesta. Por ejemplo, si establece la frecuencia en día y configura el intervalo en 15, el flujo de datos se ejecutará cada 15 días. No puede establecer el intervalo en cero. El valor mínimo del intervalo aceptado para cada frecuencia es el siguiente:<ul><li>**Una vez**: n/a</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Día**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de inicio | La marca de tiempo de la ejecución proyectada, presentada en la zona horaria UTC. |
| Relleno | El relleno determina qué datos se incorporan inicialmente. Si el relleno está habilitado, todos los archivos actuales de la ruta especificada se introducirán durante la primera ingesta programada. Si se desactiva el relleno, solo se incorporarán los archivos que se carguen entre la primera ejecución de la ingesta y la hora de inicio. Los archivos cargados antes de la hora de inicio no se incorporarán. |

## Revisión del flujo de datos

Utilice la página Revisar para obtener un resumen del flujo de datos antes de la ingesta. Los detalles se agrupan en las siguientes categorías:

* **Conexión**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **Asignar campos de conjunto de datos y asignación**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.
* **Programación**: muestra ese período, frecuencia e intervalo activos de la programación de ingesta.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/algolia/user-profiles/review.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para llevar los datos de intención de su origen de [!DNL Algolia] a Experience Platform. Para obtener recursos adicionales, visite la documentación descrita a continuación.

### Monitorización del flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están ingiriendo a través de él para ver información sobre las tasas de ingesta, el éxito y los errores. Para obtener más información sobre cómo supervisar el flujo de datos, visite el tutorial sobre [supervisar cuentas y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

### Actualizar el flujo de datos

Para actualizar configuraciones para la programación, asignación e información general de los flujos de datos, visite el tutorial sobre [actualización de flujos de datos de origen en la interfaz de usuario](../../update-dataflows.md).

### Eliminar el flujo de datos

Puede eliminar flujos de datos que ya no sean necesarios o que se hayan creado incorrectamente mediante la función **[!UICONTROL Delete]** disponible en el área de trabajo **[!UICONTROL Flujos de datos]**. Para obtener más información sobre cómo eliminar flujos de datos, visite el tutorial sobre [eliminar flujos de datos en la interfaz de usuario](../../delete.md).
