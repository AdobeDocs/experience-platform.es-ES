---
title: Información general sobre la extensión Microsoft Azure
description: Obtenga información acerca de la extensión de Microsoft Azure para el reenvío de eventos en Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 4%

---

# Información general sobre la extensión [!DNL Microsoft Azure]

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) es un servicio de entrada de datos en tiempo real y altamente escalable que le permite procesar y analizar las grandes cantidades de datos que producen sus dispositivos y aplicaciones conectados. Una vez que los datos se recopilan en un centro de eventos, se pueden transformar y almacenar mediante cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento por lotes.

La extensión [!DNL Microsoft Azure] [reenvío de eventos](../../../ui/event-forwarding/overview.md) aprovecha [!DNL Event Hubs] para enviar eventos del Edge Network de Adobe Experience Platform a [!DNL Azure] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus funcionalidades en una regla de reenvío de eventos.

## Requisitos previos

Para usar esta extensión, debe tener una cuenta de [!DNL Azure] válida con acceso a [!DNL Event Hubs]. También debe [crear un concentrador de eventos usando el [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir los pasos siguientes.

## Instalación de la extensión

Para instalar la extensión Microsoft [!DNL Azure], vaya a la interfaz de usuario de recopilación de datos o de Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez que haya seleccionado o creado la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Catálogo]**. Busque la tarjeta [!UICONTROL Microsoft Azure] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Se está seleccionando el botón [!UICONTROL Instalar] para la extensión [!UICONTROL Microsoft Azure] en la IU de recopilación de datos.](../../../images/extensions/server/azure/install.png)

Dado que la extensión no tiene propiedades de configuración, se añade inmediatamente a la lista de extensiones instaladas. Ahora puede empezar a usar [!DNL Event Hub] tipos de acción al configurar reglas de reenvío de eventos.

## Configuración de una regla de reenvío de eventos {#rule}

Comience a crear una nueva regla de reenvío de eventos y configure sus condiciones como desee. Al seleccionar las acciones de la regla, seleccione **[!UICONTROL Microsoft Azure]** para la extensión y, a continuación, seleccione **[!UICONTROL Enviar datos a los centros de eventos]** para el tipo de acción.

![Se está seleccionando el tipo de acción [!UICONTROL Enviar datos a los centros de eventos] para una regla en la IU de recopilación de datos.](../../../images/extensions/server/azure/select-action-type.png)

El panel derecho se actualiza para mostrar las opciones de configuración de cómo se deben enviar los datos. En concreto, debe asignar [elementos de datos](../../../ui/managing-resources/data-elements.md) a las distintas propiedades que representan su configuración de [!DNL Event Hub].

![Las opciones de configuración para el tipo de acción [!UICONTROL Enviar datos a los centros de eventos] que se muestra en la interfaz de usuario.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Detalles del centro de eventos]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Área de nombres] | Nombre del área de nombres [!DNL Event Hubs] que creó al [configurar el centro de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nombre] | Nombre del centro de eventos. |
| [!UICONTROL Nombre de regla de autorización SAS] | Nombre de la regla de autorización de acceso compartido para todo el espacio de nombres [!DNL Event Hubs] o para la instancia específica del centro de eventos a la que desea enviar datos. Consulte la sección del apéndice sobre [obtención de valores de autorización SAS](#sas) para obtener más información. |
| [!UICONTROL Clave de acceso SAS] | La clave principal de la regla de autorización de acceso compartido para todo el espacio de nombres [!DNL Event Hubs] o para la instancia específica del centro de eventos a la que desea enviar datos. Consulte la sección del apéndice sobre [obtención de valores de autorización SAS](#sas) para obtener más información. |
| [!UICONTROL Id. de partición] | [!DNL Event Hubs] le permite [enviar eventos directamente a particiones específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aprovechar esta función, proporcione el ID de la partición que desea que reciba los eventos. |

{style="table-layout:auto"}

**Datos**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Carga] | Este campo contiene los datos que se reenviarán a [!DNL Event Hubs]. Los datos pueden ser un objeto JSON, una cadena o un elemento de datos. |

{style="table-layout:auto"}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Por último, publique un nuevo reenvío de eventos [build](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Pasos siguientes

Esta guía explica cómo enviar datos a [!DNL Event Hubs] mediante la extensión de reenvío de eventos [!DNL Microsoft Azure]. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [descripción general del reenvío de eventos](../../../ui/event-forwarding/overview.md).

## Apéndice: Obtener valores de autorización SAS {#sas}

A las aplicaciones externas se les ha concedido acceso a [!DNL Event Hubs] mediante [firmas de acceso compartido (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Cada área de nombres [!DNL Event Hubs] e instancia del centro de eventos tiene una regla de autorización SAS predeterminada asignada automáticamente al crearla, pero también puede crear directivas adicionales para cada recurso si lo desea.

Al [configurar una regla de reenvío de eventos](#rule) con la extensión [!DNL Azure], debe proporcionar el nombre y la clave principal de la regla de autorización que rige el área de nombres o el centro de eventos específico al que desea enviar los datos. Para obtener más información sobre cómo obtener estos valores del portal [!DNL Azure], consulte las siguientes secciones en la documentación de [!DNL Azure]:

* [Obtener valores SAS para un [!DNL Event Hubs] espacio de nombres](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtener valores SAS para un concentrador de eventos específico en un espacio de nombres](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Una vez que tenga los valores requeridos, el nombre de la regla de autorización puede proporcionarse directamente como una cadena en la entrada de configuración o puede crear un elemento de datos de tipo cadena para hacer referencia a él en su lugar. Sin embargo, la clave principal debe estar contenida primero dentro de un secreto de reenvío de eventos antes de poder suministrarse en la configuración de reglas para proteger la seguridad de los datos.

En la interfaz de usuario del reenvío de eventos, [cree un nuevo secreto](../../../ui/event-forwarding/secrets.md) y seleccione **[!UICONTROL Token]** como tipo de secreto. Para el valor del token en sí, proporcione la clave principal que copió anteriormente. Después de crear el secreto, cree un elemento de datos con el tipo **[!UICONTROL Secreto]** y seleccione el secreto [!DNL Event Hubs] de la lista. Una vez configurado el elemento de datos secreto, puede hacer referencia a él en el campo **[!UICONTROL Clave de acceso SAS]**.
