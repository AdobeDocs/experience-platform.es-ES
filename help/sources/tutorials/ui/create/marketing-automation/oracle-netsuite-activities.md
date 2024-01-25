---
title: Crear un [!DNL Oracle NetSuite Activities] conexión de origen en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de actividades de NetSuite de Oracle mediante la IU de Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 053cf0af327b39830f025686e0f8f67c27f1c45c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---

# Crear un [!DNL Oracle NetSuite Activities] conexión de origen en la interfaz de usuario

>[!NOTE]
>
>El [!DNL Oracle NetSuite Activities] el origen está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Lea el siguiente tutorial para aprender a extraer datos de eventos de su [!DNL Oracle NetSuite Activities] a Adobe Experience Platform en la interfaz de usuario.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Oracle NetSuite] cuenta de, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Lea el [[!DNL Oracle NetSuite] descripción general](../../../../connectors/marketing-automation/oracle-netsuite.md) para obtener información sobre cómo recuperar las credenciales de autenticación.

## Conecte su [!DNL Oracle NetSuite] account {#connect-account}

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el *Automatización de marketing* categoría, seleccionar **[!DNL Oracle NetSuite Activities]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![Captura de pantalla de la IU de Platform para el catálogo con la tarjeta Actividades de Oracle NetSuite](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

El **[!UICONTROL Conectar Oracle Cuenta de actividades de NetSuite]** página. En esta página, puede usar credenciales nuevas o existentes.

>[!IMPORTANT]
>
>El token de actualización caduca pasados siete días. Una vez que el token haya caducado, debe crear una cuenta en el Experience Platform con el token actualizado. Si no crea una cuenta nueva con el token actualizado, puede que vea el siguiente mensaje de error: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Cuenta existente {#existing-account}

Para utilizar una cuenta existente, seleccione la [!DNL Oracle NetSuite Activities] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la IU de Platform para conectar la cuenta de actividades de NetSuite de Oracle con una cuenta existente](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### Nueva cuenta {#new-account}

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![Captura de pantalla de la IU de Platform para conectar la cuenta de actividades de NetSuite de Oracle con una nueva cuenta](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha establecido una conexión con su [!DNL Oracle NetSuite Activities] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Platform](../../dataflow/marketing-automation.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al utilizar el [!DNL Oracle NetSuite Activities] origen.

### Asignación {#mapping}

Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o el conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignación y los campos calculados, consulte la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Los campos mostrados dependen de las suscripciones que su [!DNL Oracle NetSuite] tiene acceso a. Por ejemplo, si no tiene acceso a la facturación, no verá los campos relacionados con la facturación.

### Programación {#scheduling}

Al programar su [!DNL Oracle NetSuite Activities] flujo de datos para la ingesta, debe seleccionar la siguiente configuración de frecuencia e intervalo:

| Frecuencia | Intervalo |
| --- | --- |
| `Once` | 1 |

Al recuperar los datos, la variable [!DNL Oracle NetSuite] responde con la última fecha de modificación o creación como formato de fecha en lugar de como marca de tiempo. Por lo tanto, la programación está limitada a un día.

Una vez que haya proporcionado los valores para la programación, seleccione **[!UICONTROL Siguiente]**.

![La etapa de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)