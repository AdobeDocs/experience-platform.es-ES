---
title: Información general de la extensión de Microsoft Azure
description: Obtenga información sobre la extensión de Microsoft Azure para el reenvío de eventos en Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: 8b972841c8412d510fce4c970a09d9c1eecd401e
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# [!DNL Microsoft Azure] información general de la extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) es un servicio de ingreso de datos en tiempo real altamente escalable que le permite procesar y analizar las cantidades masivas de datos que producen sus aplicaciones y dispositivos conectados. Una vez que los datos se recopilan en un centro de eventos, se pueden transformar y almacenar utilizando cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento/lotes.

La variable [!DNL Microsoft Azure] [reenvío de eventos](../../../ui/event-forwarding/overview.md) aprovechamientos de extensión [!DNL Event Hubs] para enviar eventos desde la red perimetral de Adobe Experience Platform a [!DNL Azure] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus capacidades en una regla de reenvío de eventos.

## Requisitos previos

Para utilizar esta extensión, debe tener una [!DNL Azure] cuenta con acceso a [!DNL Event Hubs]. También debe [crear un centro de eventos utilizando [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir los pasos a continuación.

## Instalación de la extensión

Para instalar Microsoft [!DNL Azure] , vaya a la IU de recopilación de datos o a la IU del Experience Platform y seleccione **[!UICONTROL Reenvío de eventos]** desde el panel de navegación izquierdo. Desde aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Catálogo]** pestaña . Busque la variable [!UICONTROL Microsoft Azure] tarjeta y, a continuación, seleccione **[!UICONTROL Instalar]**.

![La variable [!UICONTROL Instalar] botón seleccionado para la variable [!UICONTROL Microsoft Azure] en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/azure/install.png)

Dado que la extensión no tiene propiedades de configuración, se agrega inmediatamente a la lista de extensiones instaladas. Ahora puede empezar a usar [!DNL Event Hub] tipos de acción al configurar reglas de reenvío de eventos.

## Configuración de una regla de reenvío de eventos {#rule}

Comience a crear una nueva regla de reenvío de eventos y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione **[!UICONTROL Microsoft Azure]** para la extensión, seleccione **[!UICONTROL Envío de datos a centros de eventos]** para el tipo de acción.

![La variable [!UICONTROL Envío de datos a centros de eventos] tipo de acción que se está seleccionando para una regla en la interfaz de usuario de la recopilación de datos.](../../../images/extensions/server/azure/select-action-type.png)

El panel de la derecha se actualiza para mostrar las opciones de configuración de cómo se deben enviar los datos. Específicamente, debe asignar [elementos de datos](../../../ui/managing-resources/data-elements.md) a las distintas propiedades que representan su [!DNL Event Hub] configuración.

![Las opciones de configuración para la variable [!UICONTROL Envío de datos a centros de eventos] tipo de acción que se muestra en la interfaz de usuario.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Detalles del centro de eventos]**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Área de nombres] | El nombre del [!DNL Event Hubs] espacio de nombres que creó al [configuración del centro de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nombre] | Nombre del centro de eventos. |
| [!UICONTROL Nombre de la regla de autorización de SAS] | El nombre de la regla de autorización de acceso compartido para todo el [!DNL Event Hubs] o la instancia de centro de eventos específica a la que desea enviar los datos. Consulte la sección del apéndice sobre [obtención de valores de autorización SAS](#sas) para obtener más información. |
| [!UICONTROL Clave de acceso de SAS] | La clave principal de la regla de autorización de acceso compartido para todo el [!DNL Event Hubs] o la instancia de centro de eventos específica a la que desea enviar los datos. Consulte la sección del apéndice sobre [obtención de valores de autorización SAS](#sas) para obtener más información. |
| [!UICONTROL ID de partición] | [!DNL Event Hubs] le permite [enviar eventos directamente a particiones específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aprovechar esta función, proporcione el ID de la partición que desea que reciba los eventos. |

{style=&quot;table-layout:auto&quot;}

**Datos**

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Carga útil] | Este campo contiene los datos que se reenviarán al [!DNL Event Hubs]. Los datos pueden ser un objeto JSON, una cadena o un elemento de datos. |

{style=&quot;table-layout:auto&quot;}

Cuando termine, seleccione **[!UICONTROL Conservar cambios]** para agregar la acción a la configuración de regla. Cuando esté satisfecho con la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Finalmente, publicar un nuevo reenvío de eventos [versión](../../../ui/publishing/builds.md) para activar los cambios en la biblioteca.

## Pasos siguientes

Esta guía trata sobre cómo enviar datos a [!DNL Event Hubs] usando la variable [!DNL Microsoft Azure] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [información general sobre el reenvío de eventos](../../../ui/event-forwarding/overview.md).

## Apéndice: Obtener valores de autorización SAS {#sas}

Las solicitudes externas tienen acceso a [!DNL Event Hubs] hasta [firmas de acceso compartido (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Cada [!DNL Event Hubs] la instancia de espacio de nombres y centro de eventos tiene una regla de autorización SAS predeterminada asignada automáticamente al crearla, pero también puede crear directivas adicionales para cada recurso si lo desea.

When [configuración de una regla de reenvío de eventos](#rule) usando la variable [!DNL Azure] , debe proporcionar el nombre y la clave principal para la regla de autorización que rige el área de nombres o el centro de eventos específico al que desea enviar los datos. Para obtener más información sobre cómo obtener estos valores, consulte [!DNL Azure] , consulte las secciones siguientes en la sección [!DNL Azure] documentación:

* [Obtenga valores SAS para un [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtener valores SAS para un centro de eventos específico en un espacio de nombres](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Una vez que tenga los valores requeridos, el nombre de la regla de autorización se puede proporcionar directamente como una cadena en la entrada de configuración o puede crear un elemento de datos de tipo cadena para hacer referencia a él en su lugar. Sin embargo, la clave principal debe estar contenida primero dentro de un secreto de reenvío de eventos antes de proporcionarla en la configuración de reglas para proteger la seguridad de los datos.

Dentro de la interfaz de usuario del reenvío de eventos, [crear un nuevo secreto](../../../ui/event-forwarding/secrets.md) y seleccione **[!UICONTROL Token]** como tipo secreto. Para el propio valor de token, proporcione la clave principal que ha copiado anteriormente. Después de crear el secreto, cree un elemento de datos con el tipo **[!UICONTROL Secreto]** y seleccione [!DNL Event Hubs] secreto de la lista. Una vez configurado el elemento de datos secreto, puede hacer referencia a ese elemento de datos en la variable **[!UICONTROL Clave de acceso de SAS]** campo .
