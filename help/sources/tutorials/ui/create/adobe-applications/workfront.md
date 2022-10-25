---
keywords: Experience Platform;inicio;temas populares;
title: Crear una conexión de origen de Adobe Workfront en la interfaz de usuario
description: Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Workfront para llevar los datos de Workfront a Adobe Experience Platform mediante la interfaz de usuario.
source-git-commit: 99741a3be4d50d1a812e945483c9ed1577a0a999
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# Crear una conexión de origen de Adobe Workfront en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Workfront para llevar los datos de Workfront a Adobe Experience Platform mediante la interfaz de usuario.

## Primeros pasos

>[!IMPORTANT]
>
>Debe estar configurado como administrador en Adobe Admin Console para acceder al origen de Workfront.

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Crear una conexión de origen de Workfront en la interfaz de usuario

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes que pueden utilizarse para crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccione **[!UICONTROL Adobe Workfront]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con la fuente de Adobe Workfront resaltada.](../../../../images/tutorials/create/workfront/catalog.png)

## Selección de datos

La variable [!UICONTROL Seleccionar datos] aparece. Aquí debe proporcionar valores para el subdominio de Workfront y el Datalane. El subdominio de Workfront es la misma dirección URL que se utiliza para acceder a la instancia de Workfront, por ejemplo `https://acme.workfront.com/`, mientras que el datalane representa el entorno de área de trabajo que desea utilizar.

Una vez agregado el subdominio y el datalane, seleccione **[!UICONTROL Siguiente]**.

![La página de datos seleccionada con valores de marcador de posición para subdominio y datalane.](../../../../images/tutorials/create/workfront/select-data.png)

## Proporcionar detalles de flujo de datos

El paso detalle del flujo de datos le permite proporcionar un nombre y una descripción opcional para su flujo de datos. Durante este paso, también puede suscribirse a las alertas para recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, visite el tutorial en [suscripción a alertas en la interfaz de usuario de fuentes](../../alerts.md).

Una vez que haya proporcionado los detalles del flujo de datos y configurado la configuración de alerta deseada, seleccione **[!UICONTROL Siguiente]**.

![La página de detalles del flujo de datos con información sobre el nombre del flujo de datos, la descripción y las notificaciones de alerta](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Revisión

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![La página de revisión que resume la información de conexión.](../../../../images/tutorials/create/workfront/review.png)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre la fuente de Workfront.

### Esquema de evento de cambio de Workfront

Los datos de Workfront en Platform se representan como datos de registros de series temporales, en los que cada fila de los datos tiene una marca de tiempo que muestra cuándo se produjo el evento y los atributos relacionados con ese evento.

Durante la configuración, se crea un esquema denominado Workfront Change Events from Flow.

| Campo Esquema | Descripción |
| --- | --- |
| `timestamp` | Hora a la que se produjo el evento seleccionado. La marca de tiempo se representa en la zona horaria de GTM. |
| `_workfront.objectType` | El tipo de objeto. Los valores disponibles pueden incluir `project`, `task`, `portfolio`, y otros, según el objeto que se haya cambiado o creado. |
| `_workfront.objectID` | El ID que corresponde al tipo de objeto. |
| `_workfront.created` | Este valor se establece en `1` si el suceso representa una creación de objeto. |
| `_workfront.deleted` | Este valor se establece en `1` si se elimina el objeto. |
| `_worfkront.updated` | Este valor se establece en `1` si se actualiza el objeto. |
| `_workfront.completed` | Este valor se establece en `1` si el objeto está marcado como completado. |
| `_workfront.parentObjectType` | (Opcional) El tipo de objeto que corresponde al elemento principal del objeto. |
| `_workfront.parentID` | ID del objeto principal. |
| `_workfront.customData` | Mapa de todos los campos y valores de formulario personalizados completados durante el evento. |

>[!IMPORTANT]
>
>Solo se rellenan los atributos que han cambiado o que se han creado como parte de un evento. Por ejemplo, si solo cambia el nombre del objeto, los únicos campos que se rellenarán serán:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Pasos siguientes

Al seguir este tutorial, ahora ha creado un flujo de datos para llevar los datos de Workfront al Experience Platform. Ahora puede utilizar servicios como [Servicio de consultas](../../../../../query-service/home.md) para ejecutar un análisis más detallado de los datos. Para obtener más información sobre Workfront, lea la [Información general de Workfront](../../../../connectors/adobe-applications/workfront.md).