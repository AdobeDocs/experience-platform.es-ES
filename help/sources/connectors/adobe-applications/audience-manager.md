---
keywords: Experience Platform;inicio;temas populares;conector de Audience Manager;Audience Manager;audience manager
solution: Experience Platform
title: Información general de origen de Audience Manager
topic-legacy: overview
description: El origen de Adobe Audience Manager transmite datos de origen recopilados en Audience Manager a Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# origen del Audience Manager

El origen de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager para su activación en Adobe Experience Platform. La fuente del Audience Manager ingesta dos tipos de datos en Platform:

- **Datos en tiempo real:** Datos capturados en tiempo real en el servidor de recopilación de datos de Audience Manager. Estos datos se utilizan en Audience Manager para rellenar rasgos basados en reglas y aparecerán en Platform en el tiempo de latencia más corto.
- **Datos de perfil:** Audience Manager utiliza datos en tiempo real e incorporados para derivar perfiles de clientes. Estos perfiles se utilizan para rellenar gráficos de identidad y características en las realizaciones de segmentos.

El origen del Audience Manager asigna estos tipos de datos a un esquema de Experience Data Model (XDM) y, a continuación, los envía a Platform. Los datos en tiempo real se envían como datos de ExperienceEvent XDM, mientras que los datos de perfil se envían como datos de perfil individual XDM.

Para obtener más información, consulte la guía de [creación de una conexión de origen de Audience Manager en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite incorporar los datos de experiencia del cliente de forma uniforme, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en el Experience Platform, lea la [Información general del sistema XDM](../../../xdm/home.md). Para obtener más información sobre cómo se estructuran los esquemas XDM entre perfiles y eventos, lea la [conceptos básicos de la composición del esquema](../../../xdm/schema/composition.md).

## Ejemplos de esquemas XDM

A continuación se muestran ejemplos de la estructura de Audience Manager asignada a ExperienceEvent XDM y Perfil individual XDM en Platform.

### ExperienceEvent : para datos en tiempo real y datos incorporados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM: para datos de perfil

![](images/aam-profile-xdm-for-profile-data.png)

Para obtener información sobre cómo se asignan los campos de Audience Manager a XDM, consulte la documentación sobre [Campos de asignación de Audience Manager](./mapping/audience-manager.md).

## Gestión de datos en Platform

### Conjuntos de datos

Un conjunto de datos es una construcción de almacenamiento y administración para una recopilación de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas) y está disponible mediante una conexión de datos. Los datos del Audience Manager constan de datos en tiempo real, datos de entrada y datos de perfil. Para localizar los conjuntos de datos de Audience Manager, utilice la función de búsqueda en la interfaz de usuario con las convenciones de nomenclatura proporcionadas para cada tipo de datos.

Los conjuntos de datos de Audience Manager están deshabilitados para Perfil de forma predeterminada y los usuarios tienen la capacidad de habilitar o deshabilitar conjuntos de datos en función de sus casos de uso. No se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia a segmentos en Perfil.

>[!NOTE]
>
>AAM Tiempo real es el único conjunto de datos que va al lago de datos. Todos los demás conjuntos de datos del Audience Manager van a [!DNL Profile], si están activados para [!DNL Profile]. Si no están activados para [!DNL Profile], no reciben ningún dato y se muestran como vacíos.

| Nombre del conjunto de datos | Descripción | Clase |
| --- | --- | --- |
| AAM Tiempo real | Este conjunto de datos contiene datos recopilados por visitas directas en puntos finales de DCS de Audience Manager y mapas de identidad para perfiles de Audience Manager. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. | Evento de experiencia |
| AAM actualizaciones de perfil en tiempo real | Este conjunto de datos permite la segmentación en tiempo real de rasgos y segmentos del Audience Manager. Incluye información sobre el enrutamiento regional de Edge, la característica y la pertenencia a segmentos. Mantenga este conjunto de datos habilitado para la ingesta de perfiles. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** para ingerir directamente los datos en Perfil. | Registro |
| Datos de dispositivos AAM | Datos de dispositivo con ECID y realizaciones de segmentos correspondientes agregadas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** para ingerir directamente los datos en Perfil. | Registro |
| Datos de perfil del dispositivo AAM | Se utiliza para diagnósticos de conector de Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** para ingerir directamente los datos en Perfil. | Registro |
| AAM Perfiles autenticados | Este conjunto de datos contiene perfiles autenticados por el Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** para ingerir directamente los datos en Perfil. | Registro |
| Metadatos de perfiles autenticados de AAM | Se utiliza para diagnósticos del conector del Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** para ingerir directamente los datos en Perfil. | Registro |
| Relleno de datos de dispositivos AAM | El conjunto de datos no trae datos de dispositivos anteriores. Contiene ECID y las correspondientes realizaciones de segmentos agregadas en Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** alterne para ingerir directamente los datos en Perfil. | Registro |
| Relleno de perfiles autenticados AAM | El conjunto de datos no trae datos autenticados anteriores. Contiene perfiles autenticados por el Audience Manager. Los datos no son visibles como lotes en el conjunto de datos. Puede habilitar la variable **[!UICONTROL Perfil]** alterne para ingerir directamente los datos en Perfil. | Registro |

### Conexiones

Adobe Audience Manager crea una conexión en el catálogo: Conexión del Audience Manager. Catálogo es el sistema de registros para la ubicación y linaje de datos dentro de Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de conectores específica del cliente. Lea el [Información general del servicio de catálogo](../../../catalog/home.md) para obtener más información sobre Catálogo, conexiones y conectores.

### Segmentación de población en impacto de perfil

Los tamaños de población de segmentos tienen un impacto directo en los números de perfil cuando envía por primera vez un segmento de Audience Manager a Platform. Esto significa que si selecciona todos los segmentos, es posible que se produzcan sobrecargas de perfil que superen su derecho de uso de licencia. Platform también distingue los nuevos datos del historial de ingesta de perfiles. Un segmento con 100 identidades basadas en origen creará 100 perfiles. Sin embargo, si la población de ese mismo segmento se aumentó a 150 y se incorporó a Platform, el número de perfiles solo aumentará en 50, ya que solo hay 50 perfiles nuevos.

También puede comprobar el uso del perfil que su cuenta tiene disponible a través del [Tablero de uso de licencias](../../../dashboards/guides/license-usage.md).

## ¿Cuál es la latencia esperada para los datos de Audience Manager en Platform?

| Datos del Audience Manager | Tipo | Latencia | Notas |
| --- | --- | --- | --- |
| Datos en tiempo real | Eventos | &lt;25 minutos | Tiempo desde que se captura en el nodo Audience Manager Edge hasta que aparece en el lago de datos. |
| Datos en tiempo real | Actualizaciones de perfil | &lt;10 minutos | Hora de aterrizar en el perfil del cliente en tiempo real. |
| Datos en tiempo real e incorporados | Actualizaciones de perfil | de 24 a 36 horas | Tiempo que transcurre desde la captura a través de datos perimetrales DCS/PCS y datos incorporados, hasta su procesamiento en un perfil de usuario, hasta su aparición en Perfil del cliente en tiempo real. Actualmente, estos datos no aterrizan directamente en el lago de datos. La opción de alternancia de perfiles se puede habilitar para conjuntos de datos de perfil de Audience Manager para introducir estos datos directamente en Perfil del cliente en tiempo real. |
