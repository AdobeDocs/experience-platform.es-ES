---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;campaña;servicios administrados de campaña
title: Create an Adobe Campaign Managed Services source connection using Platform UI
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Adobe Campaign Managed Services mediante la interfaz de usuario de Platform.
hide: true
hidefromtoc: true
source-git-commit: 1b1f25093db642b394c6e05f15f6d1071096eb36
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---


# Creación de una conexión de origen de Adobe Campaign Managed Services mediante la interfaz de usuario de Platform

Este tutorial proporciona pasos para crear un conector de origen para llevar los datos de Adobe Campaign Managed Services a Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Experience Platform:

* [Sources](../../../../home.md): Platform allows data to be ingested from various sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services.
* [Sandboxes](../../../../../sandboxes/home.md): Platform provides virtual sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

## Conectar Adobe Campaign Managed Services a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

Under the **[!UICONTROL Adobe applications]** category, select **[!UICONTROL Adobe Campaign Managed Services]** and then select **[!UICONTROL Add data]**.

### Select data {#select-data}

La variable [!UICONTROL Seleccionar datos] aparece, proporcionando una interfaz para configurar los valores de [!UICONTROL Instancia de Adobe Campaign], [!UICONTROL Asignación de destino]y [!UICONTROL Nombre del esquema].

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="ACC Instance"
>abstract="Nombre del entorno de Adobe Campaign Classic que desea utilizar."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Asignación de destino"
>abstract="Target mappings are technical objects used by Campaign in order to deliver messages, and contain all the technical settings required to send deliveries (addresses, phone numbers, opt-in indicators, additional identifiers…)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Schema name"
>abstract="The name of the entity defined in the Adobe Campaign database."
>text="Learn more in documentation"
