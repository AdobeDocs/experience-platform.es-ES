---
title: Notas de la versión de Adobe Experience Platform, agosto de 2022
description: Notas de la versión de agosto de 2022 para Adobe Experience Platform.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 24 de agosto de 2022**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Preparación de datos](#data-prep)
- [Fuentes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Funciones actualizadas**

| Función | Descripción |
| --- | --- |
| Compatibilidad con la ingesta de registros con advertencias | La preparación de datos ahora localizará las advertencias (errores no críticos) en los campos y permitirá que se ingrese el resto de la fila. Todos los errores de transformación del asignador ahora se notifican como advertencias y las filas parcialmente ingeridas se consideran correctas, con una advertencia.  La supervisión también se admite en registros con advertencias y detalles de diagnóstico. Actualmente, la ingesta parcial de registros con advertencias solo está disponible para la transmisión de datos. Consulte la documentación de [ingesta de registros con advertencias](../../sources/tutorials/ui/monitor-streaming.md) para obtener más información. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre [!DNL Data Prep], consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad entre regiones para el origen de Adobe Analytics | Ahora puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur). Los grupos de informes deben asignarse a la misma organización que la instancia de espacio aislado del Experience Platform en la que se está creando la conexión de origen. Para obtener más información, consulte la guía de [creación de una conexión de origen de Adobe Analytics en la interfaz de usuario](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
