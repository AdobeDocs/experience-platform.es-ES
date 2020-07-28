---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector del Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: fb4ffa2c95365905f5417586fa7ecf88523009a0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# Conector del Audience Manager

El conector de datos de Adobe Audience Manager transmite datos de origen recopilados en Adobe Audience Manager a Adobe Experience Platform. El conector del Audience Manager transfiere tres categorías de datos a Platform:

- **Datos en tiempo real:** Datos capturados en tiempo real en el servidor de recopilación de datos de Audience Manager. Estos datos se utilizan en Audience Manager para rellenar características basadas en reglas y aparecerán en Platform en el tiempo de latencia más corto.
- **Datos incorporados (de entrada):** Estos son los archivos cargados por un usuario en una ubicación de Amazon S3 alojada por un Audience Manager. Audience Manager utiliza estos datos para rellenar las características integradas con el método de archivo de entrada y tendrá cierta latencia.
- **Datos de Perfil:** Audience Manager utiliza datos en tiempo real y datos incorporados para derivar perfiles de clientes. Estos perfiles se utilizan para rellenar los gráficos de identidad y las características en la realización de segmentos.

El conector del Audience Manager asigna estas categorías de datos al esquema del modelo de datos de experiencia (XDM) y las envía a Platform. Los datos en tiempo real y los datos incorporados se envían como datos de ExperienceEvent XDM, mientras que los datos de Perfil se envían como Perfiles individuales XDM.

Para obtener instrucciones sobre cómo crear una conexión con Adobe Audience Manager mediante la interfaz de usuario de Platform, consulte el tutorial [del conector del](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager.

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite incorporar de manera uniforme los datos de experiencia del cliente, facilitando la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en Experience Platform, consulte la descripción general [del sistema](../../../xdm/home.md)XDM. Para obtener más información sobre la estructura de Esquemas XDM como Perfil y ExperienceEvent, consulte los [conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquema.

## Ejemplos de esquemas XDM

A continuación se muestran ejemplos de la estructura de Audience Manager asignada a XDM ExperienceEvent y al Perfil individual XDM en Platform.

### ExperienceEvent: para datos en tiempo real y datos integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM: para datos de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## ¿Cómo se asignan los campos de Adobe Audience Manager a XDM?

Consulte la documentación de los campos [de asignación de](./mapping/audience-manager.md) Audience Manager para obtener más información.

## Gestión de datos en Platform

### Conjuntos de datos

Los conjuntos de datos son una construcción de almacenamiento y administración para una colección de datos, generalmente una tabla, que contiene esquemas (columnas) y campos (filas) y que está disponible mediante una conexión de datos. Los datos del Audience Manager constan de datos en tiempo real, datos de entrada y datos de Perfil. Para localizar los conjuntos de datos de Audience Manager, utilice la función de búsqueda de la interfaz de usuario con las convenciones de nomenclatura proporcionadas para cada tipo de datos.

Los conjuntos de datos de Audience Manager están deshabilitados para el Perfil de forma predeterminada y los usuarios pueden habilitar o deshabilitar conjuntos de datos en función de sus casos de uso. No se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia a segmentos en Perfil.

| Nombre del conjunto de datos | Descripción |
| ------------ | ----------- |
| Tiempo real del Audience Manager | Este conjunto de datos contiene datos recopilados por visitas directas en los extremos de DCS Audience Manager y mapas de identidad para Perfiles Audience Manager. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. |
| Actualizaciones de Perfil en tiempo real de Audience Manager | Este conjunto de datos permite la segmentación en tiempo real de características y segmentos de Audience Manager. Incluye información sobre el enrutamiento regional, la característica y la pertenencia a segmentos de Edge. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. |
| Datos de dispositivos Audience Manager | Datos del dispositivo con ECID y realizaciones de segmentos correspondientes agregadas en Audience Manager. |
| Datos de Perfil del dispositivo Audience Manager | Se utiliza para diagnósticos de conector de Audience Manager. |
| Perfiles autenticados por Audience Manager | Este conjunto de datos contiene perfiles autenticados por el Audience Manager. |
| Metadatos de Perfiles autenticados por Audience Manager | Se utiliza para diagnósticos del conector de Audience Manager. |
| {Id. de origen de datos} de entrada de Audience Manager **(obsoleto)** | Este conjunto de datos representa los registros incorporados en el Audience Manager a través del método de archivo de entrada. Este flujo de datos está obsoleto y se eliminará en una versión posterior. |
| Metadatos de entrada de Audience Manager **(obsoleto)** | Se utiliza para diagnósticos de conector de Audience Manager. Este flujo de datos está obsoleto y se eliminará en una versión posterior. |

### Conexiones

Adobe Audience Manager crea una conexión en el catálogo: **Conexión** de Audience Manager. Catalog es el sistema de registros para la ubicación y linaje de datos dentro del Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de Conectores específica del cliente. Consulte la información general [del servicio de](../../../catalog/home.md) catálogos para obtener más información sobre el catálogo, las conexiones y los conectores.

## ¿Cuál es la latencia esperada para los datos de Audience Manager en Platform?

| Datos del Audience Manager | Latencia | Notas |
| --- | --- | --- |
| Datos en tiempo real | &lt; 35 minutos. | Tiempo desde la captura en el nodo Tiempo real hasta la aparición en Platform Data Lake. |
| Datos de entrada | &lt; 13 horas | Tiempo desde que se captura en los cubos S3 hasta que aparece en Platform Data Lake. |
| Datos de Perfil | &lt; 2 días | Tiempo desde la captura de datos en tiempo real/entrantes hasta la adición a un perfil de usuario y la aparición definitiva en Platform Data Lake. |