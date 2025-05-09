---
title: Crear una  [!DNL Oracle NetSuite Entities] conexión de origen en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de entidades de Oracle NetSuite mediante la interfaz de usuario de Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Oracle NetSuite Entities] en la interfaz de usuario

>[!NOTE]
>
>El origen [!DNL Oracle NetSuite Entities] está en la versión beta. Consulte la [descripción general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Lea el siguiente tutorial para aprender a llevar los datos de contactos y clientes de su cuenta de [!DNL Oracle NetSuite Entities] a Adobe Experience Platform en la interfaz de usuario.

## Introducción {#getting-started}

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Oracle NetSuite] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Lea la [[!DNL Oracle NetSuite] descripción general](../../../../connectors/marketing-automation/oracle-netsuite.md) para obtener información sobre cómo recuperar sus credenciales de autenticación.

## Conectar su cuenta de [!DNL Oracle NetSuite Activities] {#connect-account}

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría *Automatización de marketing*, seleccione **[!DNL Oracle NetSuite Entities]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![Captura de pantalla de la interfaz de usuario de Experience Platform para el catálogo con la tarjeta Oracle NetSuite Entities](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

Aparecerá la página **[!UICONTROL Conectar la cuenta de entidades NetSuite de Oracle]**. En esta página, puede usar credenciales nuevas o existentes.

>[!IMPORTANT]
>
>El token de actualización caduca pasados siete días. Una vez que el token haya caducado, debe crear una cuenta en Experience Platform con el token actualizado. Si no crea una cuenta nueva con el token actualizado, puede que vea el siguiente mensaje de error: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Cuenta existente {#existing-account}

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle NetSuite Entities] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Captura de pantalla de la interfaz de usuario de Experience Platform para conectar la cuenta de entidades de Oracle NetSuite con una cuenta existente](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### Nueva cuenta {#new-account}

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Cuenta nueva]** y, a continuación, proporcione un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Captura de pantalla de la interfaz de usuario de Experience Platform para conectar la cuenta de entidades de Oracle NetSuite con una nueva cuenta](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### Seleccionar datos

A continuación, seleccione el tipo de objeto que desea introducir en Experience Platform.

| Tipo de entidad | Descripción |
| --- | --- |
| Contacto | Recupere nombres de contactos, correos electrónicos, números de teléfono y cualquier campo personalizado relacionado con contactos asociado con clientes. |
| Cliente | Recupere datos específicos del cliente, incluidos detalles como nombres de clientes, direcciones e identificadores clave. |

>[!BEGINTABS]

>[!TAB Contacto]

![Captura de pantalla de la interfaz de usuario de Experience Platform para Oracle Netsuite Entidades que muestran la configuración con la opción Contacto seleccionada](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB Cliente]

![Captura de pantalla de la interfaz de usuario de Experience Platform para Oracle Netsuite Entidades que muestran la configuración con la opción Cliente seleccionada](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Oracle NetSuite Entities]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de automatización de marketing en Experience Platform](../../dataflow/marketing-automation.md).

## Recursos adicionales {#additional-resources}

Las secciones siguientes proporcionan recursos adicionales a los que puede hacer referencia al usar el origen [!DNL Oracle NetSuite Entities].

### Asignación {#mapping}

Experience Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso. En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen y derivar valores calculados o calculados. Para ver los pasos detallados sobre el uso de la interfaz de asignador y los campos calculados, consulte la [guía de la interfaz de usuario de la preparación de datos](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Los campos mostrados dependen de las suscripciones a las que tenga acceso su cuenta de [!DNL Oracle NetSuite]. Por ejemplo, si no tiene acceso a la facturación, no verá los campos relacionados con la facturación.

### Programación {#scheduling}

Al programar el flujo de datos [!DNL Oracle NetSuite Entities] para su ingesta, debe seleccionar la siguiente configuración de frecuencia e intervalo:

| Frecuencia | Intervalo |
| --- | --- |
| `Once` | 1 |

Al recuperar datos, [!DNL Oracle NetSuite] responde con la última fecha de modificación o creación como formato de fecha en lugar de como marca de tiempo. Por lo tanto, la programación está limitada a un día.

Una vez que haya proporcionado los valores para su programación, seleccione **[!UICONTROL Siguiente]**.

![Paso de programación del flujo de trabajo de orígenes.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
