---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de origen de Adobe Audience Manager en la interfaz de usuario
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 2%

---


# Creación de un conector de origen de Adobe Audience Manager en la interfaz de usuario

Este tutorial lo acompaña a través de los pasos para crear un conector de origen para Adobe Audience Manager para incorporar datos de Evento de experiencias de consumo a Platform mediante la interfaz de usuario.

## Creación de una conexión de origen con Adobe Audience Manager

Inicie sesión en <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> y, a continuación, seleccione **Fuentes** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La pantalla *Catálogo* muestra una serie de orígenes para los que puede crear conexiones de origen y cada origen muestra el número de conexiones existentes asociadas a ellas.

En la categoría de aplicaciones *de* Adobe, seleccione **Adobe Audience Manager** para mostrar una barra de información en la parte derecha de la pantalla. La barra de información proporciona una breve descripción de la fuente seleccionada, así como opciones para la vista de la documentación o la conexión con la fuente.

Para crear un nuevo conector de origen para Adobe Audience Manager, haga clic en **Conectar origen**.

![](../../../../images/tutorials/create/aam/aam_catalog.png)

Aparecerá un cuadro de diálogo. Haga clic en **Conectar** para crear la conexión.

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

Si se establece una conexión de origen con Adobe Audience Manager, se mostrará la página actividad *de* origen del conector de Audience Manager.

![](../../../../images/tutorials/create/aam/aam_flow.png)

Si desea pausar los datos del Audience Manager entrante, puede hacerlo haciendo clic en la lista de flujo de datos y alternando su *estado* desde la columna derecha *Propiedades* .

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## Pasos siguientes

Mientras un flujo de datos de Audience Manager está activo, los datos entrantes se ingieren automáticamente en Perfiles del cliente en tiempo real. Ahora puede utilizar estos datos entrantes y crear segmentos de audiencia mediante el servicio de segmentación de Platform. Consulte los siguientes documentos para obtener más información:

- [Información general sobre el Perfil del cliente en tiempo real](../../../../../profile/home.md)
- [Descripción general del servicio de segmentación](../../../../../segmentation/home.md)