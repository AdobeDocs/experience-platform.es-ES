---
keywords: Experience Platform;inicio;temas populares;
title: (Beta) Cree una conexión de origen de Adobe Workfront en la interfaz de usuario
description: Este tutorial proporciona pasos para crear una conexión de origen de Adobe Workfront para llevar los datos de Workfront a Adobe Experience Platform mediante la interfaz de usuario.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# (Beta) Cree una conexión de origen de Adobe Workfront en la interfaz de usuario

>[!NOTE]
>
>La fuente de Adobe Workfront está en versión beta. Consulte la [información general de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Este tutorial proporciona pasos para crear una conexión de origen de Adobe Workfront para llevar los datos de Workfront a Adobe Experience Platform mediante la interfaz de usuario.

## Primeros pasos

>[!IMPORTANT]
>
>Debe estar configurado como administrador en Adobe Admin Console para acceder al origen de Workfront.

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Crear una conexión de origen de Workfront en la interfaz de usuario

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes que pueden utilizarse para crear una cuenta de.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccionar **[!UICONTROL Adobe Workfront]** y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes con la fuente de Adobe Workfront resaltada.](../../../../images/tutorials/create/workfront/catalog.png)

## Seleccionar datos

El [!UICONTROL Seleccionar datos] aparece el paso. Aquí debe proporcionar valores para el subdominio de Workfront y Datalane. El subdominio de Workfront es la misma URL que utiliza para acceder a la instancia de Workfront, por ejemplo `https://acme.workfront.com/`, mientras que el panel de datos representa el entorno de workfront que desea utilizar.

Una vez añadidos el subdominio y el conjunto de datos, seleccione **[!UICONTROL Siguiente]**.

![La página Seleccionar datos con valores de marcador de posición para el subdominio y el conjunto de datos.](../../../../images/tutorials/create/workfront/select-data.png)

## Proporcionar detalles del flujo de datos

El paso de detalles del flujo de datos le permite proporcionar un nombre y una descripción opcional para el flujo de datos. Durante este paso, también puede suscribirse a alertas para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, visite el tutorial sobre [suscripción a alertas en la interfaz de usuario de orígenes](../../alerts.md).

Una vez que haya proporcionado los detalles del flujo de datos y configurado la configuración de alerta deseada, seleccione **[!UICONTROL Siguiente]**.

![La página de detalles del flujo de datos con información sobre el nombre del flujo de datos, la descripción y las notificaciones de alerta](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Consulte

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y la cantidad de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![La página de revisión que resume la información de conexión.](../../../../images/tutorials/create/workfront/review.png)

## Apéndice

Las secciones siguientes proporcionan información adicional sobre el origen de Workfront.

### Esquema de evento de cambio de Workfront

Los datos de Workfront en Platform se representan como datos de registros de series temporales, donde cada fila de los datos tiene una marca de tiempo que se muestra cuando se produjo el evento y los atributos relacionados con ese evento.

Durante la configuración, se crea un esquema denominado Workfront Change Events from Flow.

| Campo de esquema | Descripción |
| --- | --- |
| `timestamp` | Hora a la que se produjo el evento seleccionado. La marca de tiempo se representa en la zona horaria GTM. |
| `_workfront.objectType` | El tipo de objeto. Los valores disponibles pueden incluir `project`, `task`, `portfolio`y otros, según el objeto que se haya cambiado o creado. |
| `_workfront.objectID` | El ID que corresponde al tipo de objeto. |
| `_workfront.created` | Este valor se establece en `1` si el evento representa una creación de objeto. |
| `_workfront.deleted` | Este valor se establece en `1` si se elimina el objeto. |
| `_worfkront.updated` | Este valor se establece en `1` si el objeto se actualiza. |
| `_workfront.completed` | Este valor se establece en `1` si el objeto está marcado como completado. |
| `_workfront.parentObjectType` | (Opcional) El tipo de objeto que corresponde al objeto principal del objeto. |
| `_workfront.parentID` | ID. del objeto principal. |
| `_workfront.customData` | Un mapa de todos los campos de formulario personalizados y los valores rellenados durante el evento. |

>[!IMPORTANT]
>
>Solo se rellenan los atributos que han cambiado o que se han creado como parte de un evento. Por ejemplo, si solo cambia el nombre del objeto, los únicos campos que se rellenarán son:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Pasos siguientes

Al seguir este tutorial, ahora ha creado un flujo de datos para llevar los datos de Workfront a Experience Platform. Ahora puede utilizar servicios como [Servicio de consultas](../../../../../query-service/home.md) para ejecutar más análisis de los datos. Para obtener más información sobre Workfront, lea la [Información general de Workfront](../../../../connectors/adobe-applications/workfront.md).
