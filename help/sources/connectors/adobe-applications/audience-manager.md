---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector del Administrador de Audiencias
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Conector del Administrador de Audiencias

El conector de datos de Adobe Audiencia Manager transmite datos de origen recopilados en Adobe Audiencia Manager a Adobe Experience Platform. El conector Administrador de Audiencias ingesta tres categorías de datos en la plataforma:

- **Datos en tiempo real:** Datos capturados en tiempo real en el servidor de recopilación de datos del Administrador de Audiencias. Estos datos se utilizan en el Administrador de Audiencias para rellenar características basadas en reglas y aparecerán en la plataforma en el tiempo de latencia más corto.
- **Datos incorporados (de entrada):** Estos son los archivos cargados por un usuario en una ubicación de Amazon S3 alojada por el Administrador de Audiencias. El Administrador de Audiencias utiliza estos datos para rellenar las características integradas con el método de archivo de entrada y tendrá cierta latencia.
- **Datos de Perfil:** Audiencia Manager utiliza datos en tiempo real y datos incorporados para obtener perfiles de clientes. Estos perfiles se utilizan para rellenar los gráficos de identidad y las características en la realización de segmentos.

El conector del Administrador de Audiencias asigna estas categorías de datos al esquema del Modelo de datos de experiencia (XDM) y las envía a la Plataforma. Los datos en tiempo real y los datos incorporados se envían como datos de ExperienceEvent XDM, mientras que los datos de Perfil se envían como Perfiles individuales XDM.

Para obtener instrucciones sobre cómo crear una conexión con Adobe Audiencia Manager mediante la interfaz de usuario de la plataforma, consulte el tutorial [del conector del Administrador de](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)Audiencias.

## ¿Qué es el modelo de datos de experiencia (XDM)?

XDM es una especificación documentada públicamente que proporciona un marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

El cumplimiento de los estándares XDM permite incorporar de manera uniforme los datos de experiencia del cliente, facilitando la entrega de datos y la recopilación de información.

Para obtener más información sobre cómo se utiliza XDM en la plataforma de experiencia, consulte la descripción general [del sistema](../../../xdm/home.md)XDM. Para obtener más información sobre la estructura de Esquemas XDM como Perfil y ExperienceEvent, consulte los [conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquema.

## Ejemplos de esquemas XDM

A continuación se muestran ejemplos de la estructura del Administrador de Audiencias asignada a XDM ExperienceEvent y al Perfil individual XDM en la plataforma.

### ExperienceEvent: para datos en tiempo real y datos integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM: para datos de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## ¿Cómo se asignan los campos de Adobe Audiencia Manager a XDM?

Consulte la documentación de los campos [de asignación del Administrador de][audience-manager-mapping-fields] Audiencias para obtener más información.

## Gestión de datos en la plataforma

### Conjuntos de datos

Los conjuntos de datos son una construcción de almacenamiento y administración para una colección de datos, generalmente una tabla, que contiene esquemas (columnas) y campos (filas) y que está disponible mediante una conexión de datos. Los datos del Administrador de Audiencias constan de datos en tiempo real, datos de entrada y datos de Perfil. Para ubicar los conjuntos de datos del Administrador de Audiencias, utilice la función de búsqueda en la interfaz de usuario con las convenciones de nombres proporcionadas para cada tipo de datos.

Aunque los usuarios tienen la capacidad de deshabilitar conjuntos de datos, no se recomienda deshabilitar los conjuntos de datos que se utilizarán para la pertenencia a segmentos en Perfil.

| Nombre del conjunto de datos | Descripción |
| ------------ | ----------- |
| Tiempo real del administrador de Audiencias | Este conjunto de datos contiene datos recopilados por visitas directas en los extremos DCS del Administrador de Audiencias y mapas de identidad para Perfiles del Administrador de Audiencias. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. |
| Actualizaciones del Perfil en tiempo real del Administrador de Audiencias | Este conjunto de datos permite la segmentación en tiempo real de características y segmentos del Administrador de Audiencias. Incluye información sobre el enrutamiento regional, la característica y la pertenencia a segmentos de Edge. Mantenga este conjunto de datos habilitado para la ingestión de Perfiles. |
| Datos de dispositivos del Administrador de Audiencias | Datos del dispositivo con ECID y realizaciones de segmentos correspondientes agregadas en el Administrador de Audiencias. |
| Datos de Perfil de dispositivos del Administrador de Audiencias | Se utiliza para diagnósticos de conector del Administrador de Audiencias. |
| Perfiles autenticados del Administrador de Audiencias | Este conjunto de datos contiene perfiles autenticados del Administrador de Audiencias. |
| Metadatos de Perfiles autenticados del Administrador de Audiencias | Se utiliza para diagnósticos del conector del Administrador de Audiencias. |
| {Id. de origen de datos} de entrada del Administrador de Audiencias **(obsoleto)** | Este conjunto de datos representa los registros incorporados en el Administrador de Audiencias a través del método de archivo de entrada. Este flujo de datos está obsoleto y se eliminará en una versión posterior. |
| Metadatos de entrada del Administrador de Audiencias **(obsoleto)** | Se utiliza para diagnósticos de conector del Administrador de Audiencias. Este flujo de datos está obsoleto y se eliminará en una versión posterior. |

### Conexiones

Adobe Audiencia Manager crea una conexión en el catálogo: Conexión **del Administrador de** Audiencias. Catalog es el sistema de registros para la ubicación y linaje de datos dentro de Adobe Experience Platform. Una conexión es un objeto Catalog que es una instancia de Conectores específica del cliente. Consulte la información general [del servicio de](../../../catalog/home.md) catálogos para obtener más información sobre el catálogo, las conexiones y los conectores.

## ¿Cuál es la latencia esperada para los datos del Administrador de Audiencias en la plataforma?

| Datos del Administrador de Audiencias | Latencia | Notas |
| --- | --- | --- |
| Datos en tiempo real | &lt; 35 minutos. | Tiempo desde que se captura en el nodo Tiempo real hasta que aparece en el Lago de datos de plataforma. |
| Datos de entrada | &lt; 13 horas | Tiempo desde que se captura en los bloques S3 hasta que aparece en el lago de datos de plataforma. |
| Datos de Perfil | &lt; 2 días | Tiempo desde la captura de datos en tiempo real/entrantes hasta la adición a un perfil de usuario y la aparición definitiva en Platform Data Lake. |