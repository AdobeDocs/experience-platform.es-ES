---
title: Conecte Oracle Eloqua (V2) a Experience Platform en la interfaz de usuario de
description: Aprenda a conectar su cuenta de Oracle Eloqua a Experience Platform en la interfaz de usuario de.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# Conectar [!DNL Oracle Eloqua] (V2) a Experience Platform en la IU

El conector de origen [!DNL Oracle Eloqua (V2)] le permite conectar su cuenta de Oracle Eloqua con Adobe Experience Platform, lo que permite la ingesta automatizada y escalable de datos clave de marketing B2B, incluidos contactos, cuentas, campañas y actividades de participación.

Utilice este conector de origen para configurar la autenticación segura, seleccionar las entidades de datos exactas de Eloqua que necesita y asignarlas a esquemas XDM (Experience Data Model) estandarizados. Las opciones de programación flexibles le permiten configurar cargas de datos iniciales y sincronizaciones recurrentes e incrementales, lo que garantiza que los datos de marketing permanezcan actuales y procesables.

Creado en el marco de trabajo de ingesta empresarial de Adobe, el conector de origen [!DNL Oracle Eloqua (V2)] proporciona una base fiable y ampliable para la optimización de campañas, la medición de rendimiento y la personalización en canales múltiples.

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Oracle Eloqua] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias {#credentials}

Lea la [[!DNL Eloqua] descripción general](../../../../connectors/marketing-automation/eloqua.md) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes {#catalog}

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Sources]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL Eloqua], vaya a la categoría *[!UICONTROL Marketing Automation]*, seleccione la tarjeta de origen **[!UICONTROL (V2) Oracle Eloqua]** y, a continuación, seleccione **[!UICONTROL Set up]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Add data]**.

![Tarjeta de origen Eloqua en el catálogo de orígenes con el botón Configurar resaltado.](../../../../images/tutorials/create/eloqua/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Existing account]** y luego seleccione la cuenta [!DNL Eloqua] que desee usar.

![La opción Cuenta existente seleccionada en la interfaz de creación de cuentas.](../../../../images/tutorials/create/eloqua/existing.png)

## Crear una nueva cuenta {#new}

Para crear una cuenta nueva, seleccione **[!UICONTROL New account]** y proporcione un nombre y una descripción en su [!UICONTROL Source connection details]. A continuación, en [!UICONTROL Account authentication], proporcione valores para **ID de cliente**, **secreto de cliente**, **nombre de usuario**, **contraseña** y **extremo base**. Puede leer la [guía de autenticación](../../../../connectors/marketing-automation/eloqua.md) para obtener más información sobre estas credenciales. Cuando termine, seleccione **[!UICONTROL Connect to source]** y espere unos segundos para que se establezca la conexión.

![Interfaz de la nueva cuenta con campos para los detalles de conexión de origen y las credenciales de autenticación.](../../../../images/tutorials/create/eloqua/new.png)

## Seleccionar datos

Utilice la interfaz de selección de datos para seleccionar la entidad [!DNL Eloqua] que desea introducir en Experience Platform.

>[!TIP]
>
>Al seleccionar datos, observará que, excepto en el caso de las campañas de, las demás entidades muestran datos de muestra representativos. Este método garantiza la vista previa de los campos y la estructura disponibles, ya que [!DNL Eloqua] API públicas actualmente solo recuperan datos reales para las campañas. Para las entidades restantes, se proporcionan datos de ejemplo para admitir el flujo de trabajo de configuración.

![Interfaz de selección de datos que muestra entidades de datos Eloqua disponibles.](../../../../images/tutorials/create/eloqua/select-data.png)

## Detalles del conjunto de datos y flujo de datos {#details}

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos. Durante este paso, puede utilizar un conjunto de datos existente o crear uno nuevo. Además, puede habilitar opcionalmente su conjunto de datos para su ingesta en el Perfil del cliente en tiempo real durante este paso.

![Interfaz de detalles del conjunto de datos y el flujo de datos con opciones para configurar las propiedades del conjunto de datos.](../../../../images/tutorials/create/eloqua/details.png)

## Asignación {#mapping}

Las asignaciones de [!DNL Eloqua] están organizadas en cuatro tipos de entidades principales:

* **Cuentas** - Registros de empresa/organización de [!DNL Eloqua].
* **Actividades** - Eventos de participación y actividad de marketing de [!DNL Eloqua].
* **Campañas** - Registros de campaña de marketing de [!DNL Eloqua].
* **Contactos** - Registros de persona individual de [!DNL Eloqua].

Si necesita acceder a campos adicionales más allá de los proporcionados de forma predeterminada, puede añadir estos campos mediante el proceso de asignación de preparación de datos en Experience Platform. Si el esquema predeterminado (estándar) no admite algunos de los campos obligatorios, tiene la opción de definir un esquema personalizado en Experience Platform. Utilice esta característica para crear y asignar los campos necesarios para que pueda ingerir sin problemas todos los datos relevantes de [!DNL Eloqua] en Experience Platform.

Resumen de los pasos siguientes:

* Revise los campos asignados predeterminados disponibles con la integración.
* Durante el paso de asignación, incluya todos los campos adicionales necesarios de [!DNL Eloqua].
* Si los nuevos campos no están presentes en el esquema estándar, amplíe o cree un esquema personalizado en Experience Platform que incluya estos campos.
* Complete la asignación para asegurarse de que se han introducido todos los datos deseados.

Para garantizar que la información de CRM externa se refleje con precisión, utilice la función de campo calculado en la preparación de datos para actualizar el marcador de posición `{CRM_INSTANCE_ID}` con el ID de instancia de CRM específico en el campo de datos de origen. Esto le proporciona la flexibilidad para adaptar la integración a la configuración única de su organización.

Para utilizar el editor de campos calculados, seleccione el campo de origen que desee actualizar.

![Campo de origen Eloqua con campos calculados.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

Para usuarios de [!DNL Salesforce], use el editor de campos calculados y actualice `{CRM_INSTANCE_ID}` con el identificador de instancia apropiado.

![Campo calculado para Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

Para usuarios de [!DNL Microsoft], use el editor de campos calculados y actualice `{CRM_INSTANCE_ID}` con el identificador de instancia apropiado.

![Campo calculado para Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Una vez que termine de actualizar los campos calculados, seleccione **[!UICONTROL Next]** para continuar.

![Interfaz de asignación que muestra asignaciones de campos para entidades de datos Eloqua.](../../../../images/tutorials/create/eloqua/mapping.png)

## Programación

>[!NOTE]
>
>Los siguientes son los campos delta que se utilizan internamente para la carga de datos incrementales:
>
>* **Contactos:** `C_DateModified`
>* **Cuentas:** `M_DateModified`
>* **Actividad:** `CreatedAt`
>* **Objetos personalizados:** `UpdatedAt`
>* **Campaña:** `updatedAt`

Una vez finalizada la asignación, ahora puede configurar una programación de ingesta para el flujo de datos. Establezca su [!UICONTROL Frequency] en `Once` para configurar una ejecución de ingesta única. Para la ingesta incremental, puede establecer su [!UICONTROL Frequency] en `Hour`, `Day` o `Week`. Al utilizar la ingesta incremental, también debe configurar [!UICONTROL Interval] para definir la cantidad de tiempo que transcurre entre las ejecuciones de ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para ingerir datos cada 15 días.

La frecuencia de ingesta por minuto no está disponible para el origen [!DNL Eloqua]. El horario más frecuente que puede elegir es por hora. Seleccione una programación que coincida con sus necesidades de actualización de datos. Tenga en cuenta que seleccionar una programación más frecuente aumentará los costes de cálculo.

![Interfaz de programación con opciones para configurar la frecuencia y el intervalo de ingesta.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Revisar

Con la programación de ingesta configurada, utilice la interfaz [!UICONTROL Review] para confirmar los detalles del flujo de datos. Seleccione **[!UICONTROL Finish]** para completar la configuración y permitir que el flujo de datos se inicie durante unos momentos.

![La interfaz de revisión muestra un resumen de la configuración del flujo de datos antes de la finalización.](../../../../images/tutorials/create/eloqua/review.png)

## Supervisar

Una vez seleccionado el flujo de datos, se realizará un relleno único de datos y una sincronización incremental posterior de la programación especificada. El estado de sincronización se puede monitorizar navegando hasta el flujo de datos. Para obtener más información, lea la guía sobre [supervisión de orígenes y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

## Próximos pasos

Ahora ha completado la instalación y configuración del origen de [!DNL Eloqua] en Experience Platform. Una vez establecido el flujo de datos, los datos de [!DNL Eloqua] se incorporarán de acuerdo con la programación elegida y se asignarán a esquemas XDM (Experience Data Model) estándar. Continúe monitorizando los flujos de datos y explore los datos ingeridos en Platform para obtener perspectivas y activar los casos de uso de marketing. Para obtener configuraciones y resolución de problemas más avanzados, consulte la documentación relacionada o póngase en contacto con los recursos de asistencia de Adobe.

Para obtener más información, lea la siguiente documentación:

* [Información general de fuentes](../../../../home.md)
* [Real-time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
