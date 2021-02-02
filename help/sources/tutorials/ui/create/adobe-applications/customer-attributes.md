---
keywords: Experience Platform;inicio;temas populares;atributos del cliente
solution: Experience Platform
title: Creación de un conector de origen de atributos del cliente en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial proporciona los pasos para crear un conector de origen en la interfaz de usuario para recopilar datos de perfil de atributos del cliente en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 5%

---


# Creación de un conector de origen de atributos del cliente en la interfaz de usuario

Este tutorial proporciona los pasos para crear un conector de origen en la interfaz de usuario para recopilar datos de perfil de atributos del cliente en Adobe Experience Platform. Para obtener más información sobre los atributos del cliente, consulte el [documento de información general](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

## Creación de una conexión de origen

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La pantalla **[!UICONTROL Catálogo]** muestra los orígenes disponibles para crear conexiones de entrada y cada origen muestra el número de conexiones existentes asociadas a ellas. Seleccione la opción para **[!UICONTROL Atributos del cliente]** y luego seleccione **[!UICONTROL Añadir datos]**. Deje que transcurra algún tiempo para que la conexión se establezca, se le redirigirá si la conexión se realiza correctamente.

>[!NOTE]
>
>Si ya ha establecido un conector de origen para los datos de perfil de atributos del cliente, se desactivará la opción de conexión con el origen.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

La pantalla **actividad de origen** lista todas las conexiones previamente establecidas para los datos de perfil de atributos del cliente. Para crear una nueva conexión, haga clic en **Seleccionar datos**.

>[!NOTE]
>
>Se pueden realizar varias conexiones de entrada a un origen para introducir datos diferentes.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

En la lista de conjuntos de datos de perfiles de atributos del cliente disponibles, seleccione el que desee incluir en [!DNL Platform] y haga clic en **Siguiente**.

>[!NOTE]
>
>Sólo se puede seleccionar un conjunto de datos por conexión de origen de atributos del cliente.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

Aparece el paso **Revisar**, que le permite revisar la nueva conexión entrante antes de crearla. Los detalles de la conexión se agrupan por categorías, entre ellas:

* **Detalles** de la fuente: Muestra el tipo de conexión de origen y los datos de origen seleccionados.
* **Detalles** del destinatario: Al crear otros conectores de origen, este contenedor muestra en qué conjunto de datos se están invirtiendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos. Los datos de perfil de atributos del cliente se asignan automáticamente y se ingieren en Perfiles del cliente en tiempo real.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Pasos siguientes

Una vez creada la conexión, se crea automáticamente un esquema de destinatario y un conjunto de datos para contener los datos entrantes. Cuando se completa la ingestión inicial, los datos de perfil de atributos del cliente se pueden utilizar en servicios de flujo descendente [!DNL Platform] como [!DNL Real-time Customer Profile] y [!DNL Segmentation Service]. Consulte los siguientes documentos para obtener más información:

* Información general del [[!DNL Real-time Customer Profile] ](../../../../../profile/home.md)
* Información general del [[!DNL Segmentation Service] ](../../../../../segmentation/home.md)
