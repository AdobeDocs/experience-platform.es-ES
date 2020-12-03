---
keywords: Experience Platform;home;popular topics;Audience Manager connector;Audience manager;audience manager
solution: Experience Platform
title: Conector del Audience Manager
topic: overview
description: El conector de datos de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager a Adobe Experience Platform. El conector del Audience Manager transfiere tres categorías de datos a la plataforma.
translation-type: tm+mt
source-git-commit: e51f750dae2a76cd05076edfe8c6423efe949891
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Conector del Audience Manager

El conector de datos de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager a Adobe Experience Platform. El conector del Audience Manager transfiere tres categorías de datos a la plataforma:

- **Datos en tiempo real:** Datos capturados en tiempo real en el servidor de recopilación de datos de Audience Manager. Estos datos se utilizan en Audience Manager para rellenar características basadas en reglas y aparecerán en la plataforma en el tiempo de latencia más corto.
- **Datos de perfil:** Audience Manager utiliza datos en tiempo real y datos incorporados para obtener perfiles de clientes. Estos perfiles se utilizan para rellenar los gráficos de identidad y las características en la realización de segmentos.

El conector del Audience Manager asigna estas categorías de datos al esquema del modelo de datos de experiencia (XDM) y las envía a la plataforma. Los datos en tiempo real se envían como datos de ExperienceEvent XDM, mientras que los datos de Perfil se envían como Perfiles individuales XDM.

Para obtener instrucciones sobre cómo crear una conexión con Adobe Audience Manager mediante la interfaz de usuario de la plataforma, consulte el tutorial [del conector del](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager.

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite incorporar de manera uniforme los datos de experiencia del cliente, facilitando la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en Experience Platform, consulte la descripción general [del sistema](../../../xdm/home.md)XDM. Para obtener más información sobre la estructura de Esquemas XDM como Perfil y ExperienceEvent, consulte los [conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquema.

## Ejemplos de esquemas XDM

A continuación se muestran ejemplos de la estructura de Audience Manager asignada a XDM ExperienceEvent y a XDM Individual Perfil en la plataforma.

### ExperienceEvent: para datos en tiempo real y datos incorporados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM: para datos de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## ¿Cómo se asignan los campos de Adobe Audience Manager a XDM?

Consulte la documentación de los campos [de asignación de](./mapping/audience-manager.md) Audience Manager para obtener más información.

## Gestión de datos en la plataforma

### Conjuntos de datos

Los conjuntos de datos son una construcción de almacenamiento y administración para una colección de datos, generalmente una tabla, que contiene esquemas (columnas) y campos (filas) y que está disponible mediante una conexión de datos. Los datos del Audience Manager constan de datos en tiempo real, datos de entrada y datos de Perfil. Para localizar los conjuntos de datos de Audience Manager, utilice la función de búsqueda de la interfaz de usuario con las convenciones de nomenclatura proporcionadas para cada tipo de datos.

Los conjuntos de datos de Audience Manager están deshabilitados para el Perfil de forma predeterminada y los usuarios pueden habilitar o deshabilitar conjuntos de datos en función de sus casos de uso. No se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia a segmentos en Perfil.

| Nombre del conjunto de datos | Descripción |
| ------------ | ----------- |
| Audience Manager en tiempo real | Este conjunto de datos contiene datos recopilados por visitas directas en los extremos de DCS Audience Manager y mapas de identidad para Perfiles Audience Manager. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. |
| Actualizaciones de Perfiles en tiempo real de Audience Manager | Este conjunto de datos permite la segmentación en tiempo real de características y segmentos de Audience Manager. Incluye información sobre el enrutamiento regional, la característica y la pertenencia a segmentos de Edge. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. Los datos no están visibles como lotes en el conjunto de datos. Puede activar la opción de alternancia de Perfil para transferir directamente los datos al Perfil. |
| Datos de dispositivos Audience Manager | Datos del dispositivo con ECID y realizaciones de segmentos correspondientes agregadas en Audience Manager. Los datos no están visibles como lotes en el conjunto de datos. Puede activar la opción de alternancia de Perfil para transferir directamente los datos al Perfil. |
| Datos de Perfil del dispositivo Audience Manager | Se utiliza para diagnósticos de conector de Audience Manager. Los datos no están visibles como lotes en el conjunto de datos. Puede activar la opción de alternancia de Perfil para transferir directamente los datos al Perfil. |
| perfiles autenticados por Audience Manager | Este conjunto de datos contiene perfiles autenticados por el Audience Manager. Los datos no están visibles como lotes en el conjunto de datos. Puede activar la opción de alternancia de Perfil para transferir directamente los datos al Perfil. |
| Metadatos de Perfiles autenticados por Audience Manager | Se utiliza para diagnósticos del conector de Audience Manager. Los datos no están visibles como lotes en el conjunto de datos. Puede activar la opción de alternancia de Perfil para transferir directamente los datos al Perfil. |

### Conexiones

Adobe Audience Manager crea una conexión en el catálogo: Conexión de Audience Manager. Catalog es el sistema de registros para la ubicación y linaje de datos dentro de Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de Conectores específica del cliente. Consulte la información general [del servicio de](../../../catalog/home.md) catálogos para obtener más información sobre el catálogo, las conexiones y los conectores.

## ¿Cuál es la latencia esperada para los datos de Audience Manager en la plataforma?

| Datos del Audience Manager | Latencia | Notas |
| --- | --- | --- |
| Datos en tiempo real | &lt; 35 minutos. | Tiempo que transcurre desde la captura en el nodo Audience Manager Edge hasta la aparición en Platform Data Lake. |
| Datos de perfil | &lt; 2 días | Tiempo que transcurre desde la captura a través de datos perimetrales DCS/PCS y datos incorporados, hasta su procesamiento en un perfil del usuario y su posterior aparición en Perfil. Estos datos no aterrizan directamente en Platform Data Lake hoy. Se puede habilitar la alternancia de perfiles para que los conjuntos de datos de Perfil de Audience Manager ingrese estos datos directamente en Perfil. |