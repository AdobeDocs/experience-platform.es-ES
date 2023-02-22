---
title: Crear una conexión de origen de Marketo Engage y un flujo de datos para datos de actividad personalizados en la interfaz de usuario
description: Este tutorial proporciona pasos para crear una conexión de origen de Marketo Engage y un flujo de datos en la interfaz de usuario para introducir datos de actividades personalizadas en Adobe Experience Platform.
source-git-commit: d049a29d4c39fa41917e8da1dde530966f4cbaf4
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Cree un [!DNL Marketo Engage] conexión de origen y flujo de datos para datos de actividad personalizados en la interfaz de usuario

>[!NOTE]
>
>Este tutorial proporciona pasos específicos sobre cómo configurar y traer **actividad personalizada** datos de [!DNL Marketo] al Experience Platform. Para ver los pasos sobre cómo traer **actividad estándar** información, lea la [[!DNL Marketo] Guía de la interfaz de usuario](./marketo.md).

Además de [actividades estándar](../../../../connectors/adobe-applications/mapping/marketo.md#activities), también puede usar la variable [!DNL Marketo] fuente para traer datos de actividades personalizadas a Adobe Experience Platform. Este documento proporciona pasos sobre cómo crear una conexión de origen y un flujo de datos para datos de actividad personalizados mediante el [!DNL Marketo] fuente en la interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Áreas de nombres B2B y utilidad de generación automática de esquemas](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): La utilidad de generación automática de esquemas y espacios de nombres B2B le permite utilizar [!DNL Postman] para generar automáticamente valores para los esquemas y espacios de nombres B2B. Debe completar primero los esquemas y áreas de nombres B2B antes de crear un [!DNL Marketo] conexión de origen y flujo de datos.
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Crear y editar esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md): Aprenda a crear y editar esquemas en la interfaz de usuario.
* [Espacios de nombres de identidad](../../../../../identity-service/namespaces.md): Las áreas de nombres de identidad son un componente de [!DNL Identity Service] que sirven de indicadores del contexto al que se refiere una identidad. Una identidad completa incluye un valor de ID y un área de nombres.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Recupere los detalles de la actividad personalizada

El primer paso para obtener datos de actividad personalizados de [!DNL Marketo] para el Experience Platform es recuperar el nombre de la API y el nombre para mostrar de su actividad personalizada.

Inicie sesión en su cuenta mediante el [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) interfaz. En el panel de navegación izquierdo, debajo de [!DNL Database Management], seleccione **Actividades personalizadas de Marketo**.

La interfaz se actualiza para mostrar las actividades personalizadas, incluida la información sobre sus respectivos nombres para mostrar y nombres de API. También puede utilizar el carril derecho para seleccionar y ver otras actividades personalizadas de su cuenta.

![Interfaz de actividades personalizadas en la interfaz de usuario de Adobe Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity.png)

Select **Campos** en el encabezado superior para ver los campos asociados con la actividad personalizada. En esta página, puede ver los nombres, nombres de API, descripciones y tipos de datos de los campos en su actividad personalizada. Los detalles sobre campos individuales se utilizarán en un paso posterior, al crear un esquema.

![La página Detalles de los campos de actividad personalizados de Marketo en la interfaz de usuario del Marketo Engage.](../../../../images/tutorials/create/marketo-custom-activities/marketo-custom-activity-fields.png)

## Configurar grupos de campos para actividades personalizadas en el esquema de actividades B2B

En el *[!UICONTROL Esquemas]* tablero de la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Examinar]** y, a continuación, seleccione **[!UICONTROL Actividad B2B]** de la lista de esquemas.

>[!TIP]
>
>Utilice la barra de búsqueda para acelerar la navegación por la lista de esquemas.

![El espacio de trabajo de esquemas en la interfaz de usuario del Experience Platform con el esquema de actividad B2B seleccionado.](../../../../images/tutorials/create/marketo-custom-activities/b2b-activity.png)

### Crear un nuevo grupo de campos para una actividad personalizada

A continuación, agregue un nuevo grupo de campos a la variable [!DNL B2B Activity] esquema. Este grupo de campos debe corresponder a la actividad personalizada que desea introducir y debe utilizar el nombre para mostrar de la actividad personalizada que recuperó anteriormente.

Para agregar un nuevo grupo de campos, seleccione **[!UICONTROL + Agregar]** al lado del *[!UICONTROL Grupos de campo]* panel en *[!UICONTROL Composición]*.

![La estructura del esquema.](../../../../images/tutorials/create/marketo-custom-activities/add-new-field-group.png)

La variable *[!UICONTROL Agregar grupos de campos]* se abre. Select **[!UICONTROL Crear nuevo grupo de campos]** y, a continuación, proporcione el mismo nombre para mostrar para la actividad personalizada que recuperó en un paso anterior y proporcione una descripción opcional para el nuevo grupo de campos. Cuando termine, seleccione **[!UICONTROL Agregar grupos de campos]**.

![La ventana para etiquetar y crear un nuevo grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/create-new-field-group.png)

Una vez creado, el nuevo grupo de campos para la actividad personalizada aparece en la variable [!UICONTROL Grupos de campo] catálogo.

![La estructura de esquema con un nuevo grupo de campos añadido en el panel de grupo de campos.](../../../../images/tutorials/create/marketo-custom-activities/new-field-group-created.png)

### Añadir un nuevo campo a la estructura del esquema

A continuación, añada un nuevo campo al esquema . Este nuevo campo debe configurarse como `type: object` y contendrán los campos individuales de la actividad personalizada.

Para agregar un nuevo campo, seleccione el signo más (`+`) junto al nombre del esquema. Una entrada para *[!UICONTROL Campo sin título | Tipo]* aparece. A continuación, configure las propiedades del campo utilizando la variable *[!UICONTROL Propiedades del campo]* panel. Establezca el nombre del campo como el nombre de la API de su actividad personalizada y establezca el nombre para mostrar como el nombre para mostrar de su actividad personalizada. A continuación, defina el tipo como `object` y asigne el grupo de campos al grupo de campos de actividad personalizados que creó en el paso anterior. Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![La estructura del esquema con el signo más (`+`) seleccionado para que se pueda agregar un nuevo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-object.png)

El nuevo campo aparece en el esquema .

![Se ha añadido un nuevo campo al esquema .](../../../../images/tutorials/create/marketo-custom-activities/new-object-field-added.png)

### Añadir subcampos al campo de objeto {#add-sub-fields-to-the-object-field}

El último paso para preparar el esquema es añadir campos individuales dentro del campo creado en el paso anterior.

![Grupo de subcampos agregados a un campo dentro del esquema.](../../../../images/tutorials/create/marketo-custom-activities/add-sub-fields.png)

## Crear un flujo de datos

Una vez completada la configuración del esquema, puede continuar creando un flujo de datos para los datos de actividad personalizados.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL aplicaciones de Adobe] categoría, seleccione **[!UICONTROL Marketo Engage]**. A continuación, seleccione **[!UICONTROL Añadir datos]** para crear un [!DNL Marketo] flujo de datos.

![El catálogo de fuentes en la interfaz de usuario del Experience Platform con el origen del Marketo Engage seleccionado.](../../../../images/tutorials/create/marketo/catalog.png)

### Seleccionar datos

Select **[!UICONTROL Actividades]** de la lista de [!DNL Marketo] conjuntos de datos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![El paso seleccionar datos en el flujo de trabajo de fuentes con el conjunto de datos de actividades seleccionado.](../../../../images/tutorials/create/marketo-custom-activities/select-data.png)

### Detalles de flujo de datos

Siguiente, [proporcione información para su flujo de datos](./marketo.md#provide-dataflow-details), incluidos nombres y descripciones para su conjunto de datos y flujo de datos, el esquema que utilizará y las configuraciones para [!DNL Profile] ingesta, diagnóstico de errores e ingesta parcial.

![El paso de detalle del flujo de datos.](../../../../images/tutorials/create/marketo-custom-activities/dataflow-detail.png)

### Asignación

Las asignaciones para los campos de actividad estándar se rellenan automáticamente, pero los campos de actividad personalizados deben asignarse manualmente a los campos de destino correspondientes.

Para empezar a asignar los campos de actividad personalizados, seleccione **[!UICONTROL Nuevo tipo de campo]** y, a continuación, seleccione **[!UICONTROL Añadir nuevo campo]**.

![El paso de asignación con el menú desplegable para añadir un nuevo campo.](../../../../images/tutorials/create/marketo-custom-activities/add-new-mapping-field.png)

Desplácese por la estructura de datos de origen y busque el campo de actividad personalizado que desea introducir. Cuando termine, seleccione **[!UICONTROL Select]**.

>[!TIP]
>
>Para evitar confusiones y gestionar nombres de campo duplicados, los campos de actividad personalizados llevan el prefijo API name.

![La estructura de datos de origen.](../../../../images/tutorials/create/marketo-custom-activities/select-new-mapping-field.png)

Para añadir un campo de destino, seleccione el icono de esquema ![icono de esquema](../../../../images/tutorials/create/marketo-custom-activities/schema-icon.png) y, a continuación, seleccione los campos de actividad personalizados del esquema de objetivo.

![La estructura del esquema de destino.](../../../../images/tutorials/create/marketo-custom-activities/add-target-mapping-field.png)

Repita los pasos para agregar el resto de los campos de asignación de actividad personalizados. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Todas las asignaciones para datos de origen y destino.](../../../../images/tutorials/create/marketo-custom-activities/all-mappings.png)

### Consulte

La variable *[!UICONTROL Consulte]* , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta de acceso relevante de la entidad de origen elegida y la cantidad de columnas dentro de esa entidad de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Guardar e incorporar]** y permitir que se cree un flujo de datos.

![El paso de revisión final que resume la información sobre los campos de conexión, conjunto de datos y asignación.](../../../../images/tutorials/create/marketo-custom-activities/review.png)

>[!NOTE]
>
>Una vez finalizada la ingesta, el conjunto de datos ingerido contendrá todas las actividades, incluidas las actividades estándar y personalizadas de su [!DNL Marketo] instancia. Para seleccionar los registros de actividad personalizados en Platform, debe utilizar [Servicio de consultas](../../../../../query-service/home.md) y proporcionar los predicados adecuados.

## Pasos siguientes

Siguiendo este tutorial, ha configurado un esquema de Platform para [!DNL Marketo] datos de actividad personalizados y creó un flujo de datos para llevar esos datos a Platform. Para obtener información general sobre [!DNL Marketo] fuente, lea la [[!DNL Marketo] información general de la fuente](../../../../connectors/adobe-applications/marketo/marketo.md).