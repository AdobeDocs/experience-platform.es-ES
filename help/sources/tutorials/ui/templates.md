---
description: Adobe Experience Platform proporciona plantillas preconfiguradas que puede utilizar para acelerar el proceso de ingesta de datos. Las plantillas incluyen recursos generados automáticamente, como esquemas, conjuntos de datos, reglas de asignación, identidades, áreas de nombres de identidad y flujos de datos que puede utilizar al traer datos de un origen a un Experience Platform.
title: (Beta) Cree un flujo de datos de fuentes con plantillas en la interfaz de usuario de
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (Beta) Cree un flujo de datos de fuentes con plantillas en la interfaz de usuario de

>[!IMPORTANT]
>
>Las plantillas están en versión beta y son compatibles con las siguientes fuentes:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>La documentación y las funcionalidades están sujetas a cambios.

Adobe Experience Platform proporciona plantillas preconfiguradas que puede utilizar para acelerar el proceso de ingesta de datos. Las plantillas incluyen recursos generados automáticamente, como esquemas, conjuntos de datos, identidades, reglas de asignación, áreas de nombres de identidad y flujos de datos que puede utilizar al traer datos de un origen a un Experience Platform.

Con las plantillas, puede:

* Reduzca el tiempo de respuesta de la ingesta mediante la aceleración de la creación de recursos con plantillas.
* Minimice los errores que pueden producirse durante el proceso de ingesta manual de datos.
* Actualice los recursos generados automáticamente en cualquier momento para adaptarlos a sus casos de uso.

El siguiente tutorial proporciona pasos sobre cómo utilizar las plantillas en la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Uso de plantillas en la IU de Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Seleccionar tipo de negocio"
>abstract="Seleccione el tipo de empresa adecuado para su caso de uso. El acceso puede variar según la cuenta de suscripción de Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=es" text="Información general de Real-Time CDP"

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace y vea un catálogo de fuentes disponibles en Experience Platform.

Utilice el *[!UICONTROL Categorías]* para filtrar los orígenes por categoría. También puede introducir un nombre de origen en la barra de búsqueda para buscar un origen específico del catálogo.

Vaya a la [!UICONTROL aplicaciones de Adobe] para ver la [!DNL Marketo Engage] tarjeta de origen y, a continuación, seleccione [!UICONTROL Añadir datos] para empezar.

![Catálogo del espacio de trabajo de orígenes con el origen de Marketo Engage resaltado.](../../images/tutorials/templates/catalog.png)

Aparece una ventana emergente que presenta la opción de examinar las plantillas o utilizar esquemas y conjuntos de datos existentes.

* **Examinar plantillas**: las plantillas de fuentes crean automáticamente esquemas, identidades, conjuntos de datos y flujos de datos con reglas de asignación para usted. Puede personalizar estos recursos según sea necesario.
* **Usar mis recursos existentes**: realice la ingesta de datos utilizando los conjuntos de datos y esquemas existentes que ha creado. También puede crear nuevos conjuntos de datos y esquemas si es necesario.

Para utilizar recursos generados automáticamente, seleccione **[!UICONTROL Examinar plantillas]** y luego seleccione **[!UICONTROL Seleccionar]**.

![Ventana emergente con opciones para examinar plantillas o utilizar recursos existentes.](../../images/tutorials/templates/browse-templates.png)

### Autenticación

Aparece el paso de autenticación, que le solicita que cree una nueva cuenta o que utilice una cuenta existente.

>[!BEGINTABS]

>[!TAB Usar una cuenta existente]

Para usar una cuenta existente, seleccione [!UICONTROL Cuenta existente] y, a continuación, seleccione la cuenta que desee utilizar en la lista que aparece.

![La página de selección de una cuenta existente con una lista de cuentas existentes a las que puede acceder.](../../images/tutorials/templates/existing-account.png)

>[!TAB Crear una nueva cuenta]

Para crear una nueva cuenta, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione los detalles de conexión de origen y las credenciales de autenticación de cuenta. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y espere un poco para que se establezca la nueva conexión.

![La página de autenticación de una nueva cuenta con detalles de conexión de origen y credenciales de autenticación de cuenta.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Seleccionar plantillas

Según el tipo de empresa seleccionado, aparecerá una lista de plantillas. Seleccione el icono de previsualización ![icono de previsualización](../../images/tutorials/templates/preview-icon.png) junto al nombre de una plantilla para previsualizar los datos de ejemplo de la plantilla.

![Lista de plantillas con el icono de vista previa resaltado.](../../images/tutorials/templates/templates.png)

Aparecerá la ventana de vista previa, que le permitirá explorar e inspeccionar datos de ejemplo de la plantilla. Cuando termine, seleccione **[!UICONTROL Lo tengo]**.

![La ventana de vista previa de datos de ejemplo.](../../images/tutorials/templates/preview-sample-data.png)

A continuación, seleccione la plantilla que desee utilizar en la lista. Puede seleccionar varias plantillas y crear varios flujos de datos a la vez. Sin embargo, una plantilla solo se puede utilizar una vez por cuenta. Una vez seleccionadas las plantillas, seleccione **[!UICONTROL Finalizar]** y espere unos momentos para que se generen los recursos.

Si selecciona uno o parte de los elementos de la lista de plantillas disponibles, todos los esquemas B2B y las áreas de nombres de identidad se generarán para garantizar que las relaciones B2B entre esquemas estén correctamente configuradas.

>[!NOTE]
>
>Las plantillas que ya se hayan utilizado se desactivarán de la selección.

![La lista de plantillas con la plantilla de la función de contacto de oportunidad seleccionada.](../../images/tutorials/templates/select-template.png)

### Establecer una programación

El [!DNL Microsoft Dynamics] y el [!DNL Salesforce] ambas fuentes admiten la programación de flujos de datos.

Utilice la interfaz de programación para configurar una programación de ingesta para los flujos de datos. Establezca la frecuencia de ingesta en **Una** para crear una ingesta única.

![Interfaz de programación para plantillas de Dynamics y Salesforce.](../../images/tutorials/templates/schedule.png)

También puede establecer la frecuencia de ingesta en **Minuto**, **Hora**, **Día**, o **Semana**. Si programa el flujo de datos para varias ingestas, debe establecer un intervalo para establecer un intervalo de tiempo entre cada ingesta. Por ejemplo, una frecuencia de ingesta establecida en **Hora** y un intervalo establecido en **15** significa que el flujo de datos está programado para introducir datos cada **15 horas**.

Durante este paso, también puede activar **relleno** y defina una columna para la ingesta incremental de datos. El relleno se utiliza para introducir datos históricos, mientras que la columna que defina para la ingesta incremental permite diferenciar los nuevos datos de los datos existentes.

Una vez que haya completado la configuración de la programación de ingesta, seleccione **[!UICONTROL Finalizar]**.

![La interfaz de programación para plantillas de Dynamics y Salesforce con relleno habilitado.](../../images/tutorials/templates/backfill.png)

### Revisar recursos {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Revisión de los recursos generados automáticamente"
>abstract="Puede tardar hasta cinco minutos en generar todos los recursos. Si decide salir de la página, recibirá una notificación para que se devuelva una vez que se hayan completado los recursos. Puede revisar los recursos una vez que se generen y realizar configuraciones adicionales en el flujo de datos en cualquier momento."

El [!UICONTROL Revisar recursos de plantilla] Esta página muestra los recursos generados automáticamente como parte de la plantilla. En esta página, puede ver los esquemas, conjuntos de datos, áreas de nombres de identidad y flujos de datos generados automáticamente y asociados a la conexión de origen. Puede tardar hasta cinco minutos en generar todos los recursos. Si decide salir de la página, recibirá una notificación para que se devuelva una vez que se hayan completado los recursos. Puede revisar los recursos una vez que se generen y realizar configuraciones adicionales en el flujo de datos en cualquier momento.

Los flujos de datos generados automáticamente están habilitados de forma predeterminada. Seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y seleccione **[!UICONTROL Previsualizar asignaciones]** para ver los conjuntos de asignaciones creados para el flujo de datos.

![Ventana desplegable con la opción de previsualización de asignaciones seleccionada.](../../images/tutorials/templates/preview.png)

Aparecerá una página de vista previa que le permitirá inspeccionar la relación de asignación entre los campos de datos de origen y los campos de esquema de destino. Una vez vistas las asignaciones del flujo de datos. Seleccionar **[!UICONTROL Lo tengo.]**

![Ventana de vista previa de asignación.](../../images/tutorials/templates/preview-mappings.png)

Puede actualizar los flujos de datos en cualquier momento después de la ejecución. Seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y seleccione **[!UICONTROL Actualizar flujo de datos]**. Se le redirige a la página de flujo de trabajo de fuentes, donde puede actualizar los detalles del flujo de datos, incluida la configuración de la ingesta parcial, los diagnósticos de error y las notificaciones de alerta, así como la asignación del flujo de datos.

Puede utilizar la vista del editor de esquemas para realizar actualizaciones en el esquema generado automáticamente. Visite la guía en [uso del editor de esquemas](../../../xdm/tutorials/create-schema-ui.md) para obtener más información.

![Ventana desplegable con la opción update data fllows seleccionada.](../../images/tutorials/templates/update.png)

## Pasos siguientes

Al seguir este tutorial, ha creado flujos de datos, así como recursos como esquemas, conjuntos de datos y áreas de nombres de identidad mediante plantillas. Para obtener información general sobre las fuentes, visite la [información general de orígenes](../../home.md).

## Apéndice

La siguiente sección proporciona información adicional sobre las plantillas.

### Utilice el panel de notificaciones para volver a la página de revisión

Las plantillas son compatibles con las alertas de Adobe Experience Platform y puede utilizar el panel de notificaciones para recibir actualizaciones sobre el estado de sus recursos y también para volver a la página de revisión.

Seleccione el icono de notificación en el encabezado superior de la interfaz de usuario de Platform y, a continuación, seleccione la alerta de estado para ver los recursos que desea revisar.

![El panel Notificaciones en la IU de Platform con una notificación que alerta sobre un flujo de datos fallido resaltado.](../../images/tutorials/templates/notifications.png)
