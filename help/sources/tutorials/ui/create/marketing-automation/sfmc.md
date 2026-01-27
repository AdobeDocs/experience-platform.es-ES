---
title: Conecte su cuenta de Salesforce Marketing Cloud (V2) a Experience Platform a través de la interfaz de usuario de
description: Aprenda a conectar su cuenta de Salesforce Marketing Cloud (V2) a Experience Platform a través de la interfaz de usuario de.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform mediante el área de trabajo de orígenes en la interfaz de usuario de Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Lea la [[!DNL Salesforce Marketing Cloud] descripción general](../../../../connectors/marketing-automation/sfmc.md#prerequisites) para obtener información sobre la autenticación.

## Navegar por el catálogo de fuentes

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo *[!UICONTROL Sources]*. Elija una categoría o utilice la barra de búsqueda para encontrar el origen.

Para conectarse a [!DNL Salesforce Marketing Cloud], vaya a la categoría *[!UICONTROL Marketing Automation]*, seleccione la tarjeta de origen **[!UICONTROL (V2) Salesforce Marketing Cloud]** y, a continuación, seleccione **[!UICONTROL Set up]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez creada una cuenta autenticada, esta opción cambia a **[!UICONTROL Add data]**.

![El catálogo de orígenes con el origen de Salesforce Marketing Cloud seleccionado.](../../../../images/tutorials/create/sfmc/catalog.png)

## Usar una cuenta existente {#existing}

Para usar una cuenta existente, seleccione **[!UICONTROL Existing account]** y luego seleccione la cuenta [!DNL Salesforce Marketing Cloud] que desee usar.

![Interfaz de cuenta existente del flujo de trabajo de orígenes](../../../../images/tutorials/create/sfmc/existing.png)

## Crear una nueva cuenta {#new}

Para crear una cuenta nueva, seleccione **[!UICONTROL New account]** y proporcione un nombre y una descripción en su [!UICONTROL Source connection details]. A continuación, en [!UICONTROL Account authentication], proporcione valores para **ID de cliente**, **secreto de cliente** y **extremo base**. Puede leer la [guía de autenticación](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials) para obtener más información sobre estas credenciales. Cuando termine, seleccione **[!UICONTROL Connect to source]** y espere unos segundos para que se establezca la conexión.

![La nueva interfaz de cuenta del flujo de trabajo de orígenes.](../../../../images/tutorials/create/sfmc/new.png)

## Seleccionar datos

El origen [!DNL Salesforce Marketing Cloud] solo admite la ingesta de datos desde las extensiones de datos [!DNL Salesforce Marketing Cloud].

Utilice la interfaz [!UICONTROL Select data] para seleccionar la extensión de datos que desea introducir desde la instancia [!DNL Salesforce Marketing Cloud]. Una vez seleccionada la extensión de datos, puede utilizar el panel de vista previa para confirmar que el conjunto de datos contiene los campos esperados antes de continuar.

![Paso para seleccionar datos del flujo de trabajo de orígenes](../../../../images/tutorials/create/sfmc/select-data.png)

## Detalles del conjunto de datos y flujo de datos

A continuación, debe proporcionar información sobre el conjunto de datos y el flujo de datos. Durante este paso, puede utilizar un conjunto de datos existente o crear uno nuevo. Además, puede habilitar opcionalmente su conjunto de datos para su ingesta en el Perfil del cliente en tiempo real durante este paso.

![El conjunto de datos y el paso de detalles de flujo de datos del flujo de trabajo de orígenes.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Asignación

En [!DNL Salesforce Marketing Cloud], las extensiones de datos no se consideran objetos estándar. Por lo tanto, no hay campos de asignación predefinidos o fijos a un esquema de Experience Platform. Mientras que la preparación de datos en Experience Platform realiza una alineación óptima entre los campos de origen de [!DNL Salesforce Marketing Cloud] y el esquema de destino del modelo de datos de experiencia (XDM), puede haber algunos casos en los que se requiera una revisión manual o un ajuste para resolver los campos no asignados o erróneos.

![Paso de asignación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/sfmc/mapping.png)

## Programar un flujo de datos

Una vez finalizada la asignación, ahora puede configurar una programación de ingesta para el flujo de datos. Establezca su [!UICONTROL Frequency] en `Once` para configurar una ejecución de ingesta única. Para la ingesta incremental, puede establecer su [!UICONTROL Frequency] en `Hour`, `Day` o `Week`. Al utilizar la ingesta incremental, también debe configurar [!UICONTROL Interval] para definir la cantidad de tiempo que transcurre entre las ejecuciones de ingesta. Por ejemplo, una frecuencia de ingesta establecida en `Day` y un intervalo establecido en `15` significa que el flujo de datos está programado para ingerir datos cada 15 días.

>[!TIP]
>
> La frecuencia de ingesta por minuto no está disponible para el origen [!DNL Salesforce Marketing Cloud]. El horario más frecuente que puede elegir es por hora. Seleccione una programación que coincida con sus necesidades de actualización de datos. Tenga en cuenta que seleccionar una programación más frecuente aumentará los costes de cálculo.

Debe seleccionar un campo delta (fecha/hora) en el conjunto de datos para habilitar la sincronización incremental. Si el conjunto de datos no contiene un campo delta adecuado, no podrá crear el flujo de datos.

![Paso de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/sfmc/schedule.png)

## Revisar

Con la programación de ingesta configurada, utilice la interfaz [!UICONTROL Review] para confirmar los detalles del flujo de datos. Seleccione **[!UICONTROL Finish]** para completar la configuración y permitir que el flujo de datos se inicie durante unos momentos.

![Paso de revisión del flujo de trabajo de orígenes.](../../../../images/tutorials/create/sfmc/review.png)

## Supervisar

Una vez seleccionado el flujo de datos, se realizará un relleno único de datos y una sincronización incremental posterior de la programación especificada. El estado de sincronización se puede monitorizar navegando hasta el flujo de datos. Para obtener más información, lea la guía sobre [supervisión de orígenes y flujos de datos en la interfaz de usuario](../../../../../dataflows/ui/monitor-sources.md).

## Próximos pasos

Este tutorial le guió a través de la conexión de su cuenta de [!DNL Salesforce Marketing Cloud] (V2) a Experience Platform mediante la interfaz de usuario. Ha aprendido a seleccionar o crear una cuenta de origen, proporcionar las credenciales necesarias, elegir extensiones de datos para la ingesta, especificar detalles de conjuntos de datos y flujos de datos, asignar los datos, configurar una programación para la ingesta de datos y monitorizar los flujos de datos. Al seguir estos pasos, integró correctamente los datos de [!DNL Salesforce Marketing Cloud] con Experience Platform para su activación y análisis.

Para obtener más información, lea la siguiente documentación:

* [Información general de fuentes](../../../../home.md)
* [Real-time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

