---
description: Adobe Experience Platform proporciona plantillas preconfiguradas que puede utilizar para acelerar el proceso de consumo de datos. Las plantillas incluyen recursos generados automáticamente, como esquemas, conjuntos de datos, reglas de asignación, identidades, áreas de nombres de identidad y flujos de datos, que se pueden utilizar al importar datos de un origen a un Experience Platform.
title: (Beta) Cree un flujo de datos de fuentes mediante plantillas en la interfaz de usuario
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 10%

---

# (Beta) Cree un flujo de datos de fuentes mediante plantillas en la interfaz de usuario

>[!IMPORTANT]
>
>Las plantillas están en versión beta y son compatibles con las siguientes fuentes:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>La documentación y las funcionalidades están sujetas a cambios.

Adobe Experience Platform proporciona plantillas preconfiguradas que puede utilizar para acelerar el proceso de consumo de datos. Las plantillas incluyen recursos generados automáticamente, como esquemas, conjuntos de datos, identidades, reglas de asignación, áreas de nombres de identidad y flujos de datos, que se pueden utilizar al importar datos de un origen a un Experience Platform.

Con las plantillas, puede:

* Reduzca el tiempo de respuesta al valor de la ingesta mediante la aceleración de la creación de recursos con plantilla.
* Minimice los errores que se pueden producir durante el proceso de ingesta manual de datos.
* Actualice los recursos generados automáticamente en cualquier momento para adaptarlos a sus casos de uso.

El siguiente tutorial proporciona pasos sobre cómo utilizar plantillas en la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Uso de plantillas en la interfaz de usuario de Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Seleccionar tipo de negocio"
>abstract="Seleccione el tipo de negocio adecuado para su caso de uso. El acceso puede variar en función de la cuenta de suscripción a Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=es" text="Información general sobre Real-Time CDP"

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo y ver un catálogo de fuentes disponibles en Experience Platform.

Utilice la variable *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. Como alternativa, introduzca un nombre de origen en la barra de búsqueda para encontrar un origen específico del catálogo.

Vaya a la [!UICONTROL aplicaciones de Adobe] para ver la [!DNL Marketo Engage] tarjeta de origen y, a continuación, seleccione [!UICONTROL Añadir datos] para comenzar.

![Catálogo del espacio de trabajo de fuentes con el origen del Marketo Engage resaltado.](../../images/tutorials/templates/catalog.png)

Aparece una ventana emergente que le presenta la opción de examinar plantillas o utilizar esquemas y conjuntos de datos existentes.

* **Examinar plantillas**: Las plantillas de fuentes crean automáticamente esquemas, identidades, conjuntos de datos y flujos de datos con reglas de asignación. Puede personalizar estos recursos según sea necesario.
* **Usar mis recursos existentes**: Ingeste los datos mediante conjuntos de datos y esquemas existentes que haya creado. También puede crear nuevos conjuntos de datos y esquemas si es necesario.

Para utilizar recursos generados automáticamente, seleccione **[!UICONTROL Examinar plantillas]** y, a continuación, seleccione **[!UICONTROL Select]**.

![Ventana emergente con opciones para examinar plantillas o utilizar recursos existentes.](../../images/tutorials/templates/browse-templates.png)

### Autenticación

Aparece el paso de autenticación, que le solicita que cree una cuenta nueva o que utilice una existente.

>[!BEGINTABS]

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione [!UICONTROL Cuenta existente] y, a continuación, seleccione la cuenta que desee utilizar en la lista que aparece.

![La página de selección de una cuenta existente con una lista de cuentas existentes a las que puede acceder.](../../images/tutorials/templates/existing-account.png)

>[!TAB Crear una cuenta nueva]

Para crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione los detalles de conexión de origen y las credenciales de autenticación de la cuenta. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y permitir que la nueva conexión se establezca algún tiempo.

![La página de autenticación de una cuenta nueva con detalles de conexión de origen y credenciales de autenticación de cuenta.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Seleccionar plantillas

Según el tipo de negocio que haya seleccionado, aparecerá una lista de plantillas. Seleccione el icono de vista previa ![icono de vista previa](../../images/tutorials/templates/preview-icon.png) junto al nombre de una plantilla para obtener una vista previa de los datos de ejemplo de la plantilla.

![Una lista de plantillas con el icono de vista previa resaltado.](../../images/tutorials/templates/templates.png)

Aparece la ventana de vista previa que le permite explorar e inspeccionar datos de ejemplo de la plantilla. Cuando termine, seleccione **[!UICONTROL Lo tengo]**.

![La ventana de datos de muestra de vista previa.](../../images/tutorials/templates/preview-sample-data.png)

A continuación, seleccione la plantilla que desee utilizar en la lista. Puede seleccionar varias plantillas y crear varios flujos de datos a la vez. Sin embargo, una plantilla solo se puede utilizar una vez por cuenta. Una vez seleccionadas las plantillas, seleccione **[!UICONTROL Finalizar]** y permitir que se generen unos momentos para los recursos.

Si selecciona uno o varios elementos de la lista de plantillas disponibles, todos los esquemas B2B y áreas de nombres de identidad se generarán aún para garantizar que las relaciones B2B entre esquemas estén configuradas correctamente.

>[!NOTE]
>
>Las plantillas que ya se hayan utilizado se desactivarán en la selección.

![La lista de plantillas con la plantilla Rol de contacto de oportunidad seleccionada.](../../images/tutorials/templates/select-template.png)

### Configuración de una programación

La variable [!DNL Microsoft Dynamics] y [!DNL Salesforce] los orígenes de ambos son compatibles con la programación de flujos de datos.

Utilice la interfaz de programación para configurar una programación de ingesta para sus flujos de datos. Configure la frecuencia de ingesta en **Una vez** para crear una ingesta única.

![Interfaz de programación para plantillas de Dynamics y Salesforce.](../../images/tutorials/templates/schedule.png)

Como alternativa, puede establecer la frecuencia de ingesta en **Minuto**, **Hora**, **Día** o **Semana**. Si programa el flujo de datos para varias ingestas, debe establecer un intervalo para establecer un intervalo de tiempo entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en **Hora** y un intervalo establecido en **15** significa que el flujo de datos está programado para introducir datos cada **15 horas**.

Durante este paso, también puede activar **relleno** y defina una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar nuevos datos de los datos existentes.

Una vez que haya completado la configuración de la programación de ingesta, seleccione **[!UICONTROL Finalizar]**.

![Interfaz de programación para plantillas de Dynamics y Salesforce con relleno habilitado.](../../images/tutorials/templates/backfill.png)

### Revisar recursos {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Revise los recursos generados automáticamente"
>abstract="La generación de todos los recursos puede tardar hasta cinco minutos. Si decide salir de la página, recibirá una notificación para regresar una vez que se hayan completado los recursos. Puede revisar los recursos una vez que se hayan generado y realizar configuraciones adicionales en el flujo de datos en cualquier momento."

La variable [!UICONTROL Revisar recursos de plantilla] muestra los recursos generados automáticamente como parte de la plantilla. En esta página, puede ver los esquemas, conjuntos de datos, áreas de nombres de identidad y flujos de datos generados automáticamente y asociados con la conexión de origen. La generación de todos los recursos puede tardar hasta cinco minutos. Si decide salir de la página, recibirá una notificación para regresar una vez que se hayan completado los recursos. Puede revisar los recursos una vez que se hayan generado y realizar configuraciones adicionales en el flujo de datos en cualquier momento.

Los flujos de datos generados automáticamente están habilitados de forma predeterminada. Seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Previsualizar asignaciones]** para ver los conjuntos de asignación creados para su flujo de datos.

![Ventana desplegable con la opción de vista previa de asignaciones seleccionada.](../../images/tutorials/templates/preview.png)

Aparece una página de vista previa que le permite inspeccionar la relación de asignación entre los campos de datos de origen y los campos de esquema de destino. Una vez que haya visto las asignaciones de su flujo de datos. Select **[!UICONTROL Lo tengo.]**

![La ventana de vista previa de la asignación.](../../images/tutorials/templates/preview-mappings.png)

Puede actualizar los flujos de datos en cualquier momento después de la ejecución. Seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Actualizar flujo de datos]**. Se le redirige a la página de flujo de trabajo de fuentes donde puede actualizar sus detalles del flujo de datos, incluida la configuración para la ingesta parcial, el diagnóstico de errores y las notificaciones de alerta, así como la asignación del flujo de datos.

Puede utilizar la vista del editor de esquemas para realizar actualizaciones en el esquema generado automáticamente. Visite la guía de [uso del editor de esquemas](../../../xdm/tutorials/create-schema-ui.md) para obtener más información.

![Una ventana desplegable con la opción de actualización de flujos de datos seleccionada.](../../images/tutorials/templates/update.png)

## Pasos siguientes

Al seguir este tutorial, ahora ha creado flujos de datos, así como recursos como esquemas, conjuntos de datos y áreas de nombres de identidad mediante plantillas. Para obtener información general sobre las fuentes, visite [información general sobre fuentes](../../home.md).

## Apéndice

La siguiente sección proporciona información adicional sobre las plantillas.

### Utilice el panel de notificaciones para volver a la página de revisión

Las plantillas son compatibles con las alertas de Adobe Experience Platform, y puede utilizar el panel de notificaciones para recibir actualizaciones sobre el estado de sus recursos y también para volver a la página de revisión.

Seleccione el icono de notificación en el encabezado superior de la interfaz de usuario de Platform y, a continuación, seleccione la alerta de estado para ver los recursos que desea revisar.

![El panel de notificaciones de la interfaz de usuario de Platform con una notificación que avisa de un flujo de datos fallido resaltado.](../../images/tutorials/templates/notifications.png)
