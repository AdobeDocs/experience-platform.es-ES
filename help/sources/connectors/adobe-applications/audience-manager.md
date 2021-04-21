---
keywords: Experience Platform;inicio;temas populares;conector de Audience Manager;Audience Manager;audience manager
solution: Experience Platform
title: Información general del conector de origen del Audience Manager
topic-legacy: overview
description: El conector de origen de Adobe Audience Manager transmite datos de origen recopilados en Audience Manager a Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Conector del Audience Manager

El conector de datos de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager a Adobe Experience Platform. El conector del Audience Manager incorpora dos categorías de datos en Platform:

- **Datos en tiempo real:** datos capturados en tiempo real en el servidor de recopilación de datos del Audience Manager. Estos datos se utilizan en Audience Manager para rellenar rasgos basados en reglas y aparecerán en Platform en el tiempo de latencia más corto.
- **Datos de perfil:** Audience Manager utiliza datos en tiempo real e incorporados para derivar perfiles de clientes. Estos perfiles se utilizan para rellenar gráficos de identidad y características en las realizaciones de segmentos.

El conector del Audience Manager asigna estas categorías de datos al esquema del Modelo de datos de experiencia (XDM) y las envía a Platform. Los datos en tiempo real se envían como datos de ExperienceEvent XDM, mientras que los datos de perfil se envían como perfiles individuales XDM.

Para obtener instrucciones sobre la creación de una conexión con Adobe Audience Manager mediante la interfaz de usuario de Platform, consulte el tutorial [Conector del Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite incorporar los datos de experiencia del cliente de forma uniforme, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en el Experience Platform, consulte la [información general del sistema XDM](../../../xdm/home.md). Para obtener más información sobre cómo se estructuran los esquemas XDM como Perfil y ExperienceEvent, consulte los [conceptos básicos de la composición del esquema](../../../xdm/schema/composition.md).

## Ejemplos de esquemas XDM

A continuación se muestran ejemplos de la estructura de Audience Manager asignada a ExperienceEvent XDM y Perfil individual XDM en Platform.

### ExperienceEvent : para datos en tiempo real y datos incorporados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM: para datos de perfil

![](images/aam-profile-xdm-for-profile-data.png)

## ¿Cómo se asignan los campos de Adobe Audience Manager a XDM?

Consulte la documentación de [Audience Manager mapping fields](./mapping/audience-manager.md) para obtener más información.

## Gestión de datos en Platform

### Conjuntos de datos

Los conjuntos de datos son una construcción de almacenamiento y administración para una recopilación de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas) y que está disponible mediante una conexión de datos. Los datos del Audience Manager constan de datos en tiempo real, datos de entrada y datos de perfil. Para localizar los conjuntos de datos de Audience Manager, utilice la función de búsqueda en la interfaz de usuario con las convenciones de nomenclatura proporcionadas para cada tipo de datos.

Los conjuntos de datos de Audience Manager están deshabilitados para Perfil de forma predeterminada y los usuarios tienen la capacidad de habilitar o deshabilitar conjuntos de datos en función de sus casos de uso. No se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia a segmentos en Perfil.

| Nombre del conjunto de datos | Descripción |
| ------------ | ----------- |
| AAM Tiempo real | Este conjunto de datos contiene datos recopilados por visitas directas en puntos finales de DCS de Audience Manager y mapas de identidad para perfiles de Audience Manager. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. |
| AAM actualizaciones de perfil en tiempo real | Este conjunto de datos habilita la segmentación en tiempo real de rasgos y segmentos del Audience Manager. Incluye información sobre el enrutamiento regional de Edge, la característica y la pertenencia a segmentos. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar el botón **[!UICONTROL Profile]** para ingerir directamente los datos en Perfil. |
| Datos de dispositivos AAM | Datos de dispositivo con ECID y realizaciones de segmentos correspondientes agregadas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar el botón **[!UICONTROL Profile]** para ingerir directamente los datos en Perfil. |
| Datos de perfil del dispositivo AAM | Se utiliza para diagnósticos de conector de Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar el botón **[!UICONTROL Profile]** para ingerir directamente los datos en Perfil. |
| AAM Perfiles autenticados | Este conjunto de datos contiene perfiles autenticados por el Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar el botón **[!UICONTROL Profile]** para ingerir directamente los datos en Perfil. |
| Metadatos de perfiles autenticados de AAM | Se utiliza para diagnósticos del conector del Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar el botón **[!UICONTROL Profile]** para ingerir directamente los datos en Perfil. |
| Relleno de datos de dispositivos AAM | El conjunto de datos no trae datos de dispositivos anteriores. Contiene ECID y las correspondientes realizaciones de segmentos agregadas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede activar el botón **[!UICONTROL Profile]** para introducir directamente los datos en Perfil. |
| Relleno de perfiles autenticados AAM | El conjunto de datos no trae datos autenticados anteriores. Contiene perfiles autenticados por el Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede activar el botón **[!UICONTROL Profile]** para introducir directamente los datos en Perfil. |

### Conexiones

Adobe Audience Manager crea una conexión en el catálogo: Conexión del Audience Manager. Catálogo es el sistema de registros para la ubicación y linaje de datos dentro de Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de Conectores específica del cliente. Consulte la [Descripción general del servicio de catálogo](../../../catalog/home.md) para obtener más información sobre el catálogo, las conexiones y los conectores.

## ¿Cuál es la latencia esperada para los datos de Audience Manager en Platform?

| Datos del Audience Manager | Latencia | Notas |
| --- | --- | --- |
| Datos en tiempo real | &lt; 35 minutos. | Tiempo desde que se captura en el nodo de Edge del Audience Manager hasta que aparece en el lago de datos de la plataforma. |
| Datos de perfil | &lt; 2 días | Tiempo que transcurre desde la captura a través de datos perimetrales DCS/PCS y datos incorporados, hasta su procesamiento en un perfil de usuario, hasta su aparición en Perfil. Estos datos no llegan a Platform Data Lake directamente en la actualidad. La opción de alternancia de perfiles se puede habilitar para conjuntos de datos de perfil de Audience Manager para introducir estos datos directamente en Perfil. |
