---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;campaña;servicios administrados de campaña
title: Creación de una conexión de origen de Adobe Campaign Managed Services mediante la interfaz de usuario de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Adobe Campaign Managed Services mediante la interfaz de usuario de Platform.
hide: true
hidefromtoc: true
source-git-commit: 57a34b10e40dee80638392477d49c21e107c491f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Creación de una conexión de origen de Adobe Campaign Managed Services mediante la interfaz de usuario de Platform

Este tutorial proporciona pasos para crear un conector de origen para llevar los datos de Adobe Campaign Managed Services a Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Experience Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Conectar Adobe Campaign Managed Services a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccione **[!UICONTROL Adobe Campaign Managed Services]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

### Seleccionar datos {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Instancia ACC"
>abstract="Nombre del entorno de Adobe Campaign Classic que desea utilizar."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Asignación de destino"
>abstract="Las asignaciones de destino son objetos técnicos que Campaign utiliza para enviar mensajes y contienen toda la configuración técnica necesaria para realizar envíos (direcciones, números de teléfono, indicadores de inclusión, identificadores adicionales..)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Nombre del esquema"
>abstract="Nombre de la entidad definida en la base de datos de Adobe Campaign."
>text="Learn more in documentation"

La variable [!UICONTROL Seleccionar datos] aparece, proporcionando una interfaz para configurar los valores de [!UICONTROL Instancia de Adobe Campaign], [!UICONTROL Asignación de destino]y [!UICONTROL Nombre del esquema].
