---
title: Actualizar la fecha de finalización de los flujos de datos de exportación del conjunto de datos (acción necesaria el 1 de mayo de 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Obtenga información sobre cómo actualizar la fecha de finalización de los flujos de datos de exportación del conjunto de datos con una fecha de finalización actual del 1 de mayo de 2025.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Actualizar la fecha de finalización de los flujos de datos de exportación del conjunto de datos (acción necesaria el 1 de mayo de 2025)

>[!IMPORTANT]
>
>Los elementos de acción de esta página se aplican si su organización configura flujos de datos de exportación de conjuntos de datos antes de la versión de septiembre de 2024 de Experience Platform.

## ¿Qué está sucediendo?

En la versión de [septiembre de 2024 de Experience Platform](/help/release-notes/latest/latest.md#destinations) se introdujo la opción de establecer una fecha de `endTime` para exportar flujos de datos del conjunto de datos. Adobe también ha introducido una fecha de finalización predeterminada del 1 de mayo de 2025 para todos los flujos de datos de exportación de conjuntos de datos creados *antes de la versión de septiembre de 2024*. Estos flujos de datos muestran actualmente un mensaje similar al que se muestra a continuación.

![Notificación de la interfaz de usuario sobre la necesidad de actualizar la fecha de finalización del flujo de datos del conjunto de datos de exportación.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Elemento de acción**: Para cualquiera de estos flujos de datos, debe actualizar manualmente la fecha de finalización antes de que caduque; de lo contrario, se detendrán las exportaciones. Utilice la IU de Experience Platform para identificar qué flujos de datos están configurados para detenerse el 1 de mayo de 2025.

## ¿Por qué se me notifica?

Se ha identificado a su organización como si tuviera flujos de datos de exportación de conjuntos de datos activos con una fecha de finalización del 1 de mayo de 2025.

## Uso de la interfaz de usuario para actualizar la fecha de finalización

Utilice la interfaz de usuario de Experience Platform para identificar los flujos de datos con una fecha de finalización del 1 de mayo de 2025 y actualizarlos a una fecha futura.

### Buscar los flujos de datos que deben actualizarse

Vaya a **Destinos > Examinar** y busque el tipo de datos **Conjuntos de datos** en la columna **Tipo de datos**, como se muestra a continuación. Seleccione los flujos de datos deseados para inspeccionarlos.

![Flujos de datos de exportación de conjuntos de datos resaltados en la ficha Examinar.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Actualizar la fecha de finalización de los flujos de datos

Para actualizar la fecha de finalización de los flujos de datos:

1. En los flujos de datos que seleccionó para inspección en el paso anterior, seleccione **Exportar conjuntos de datos**.
   ![Control de conjuntos de datos de exportación resaltado en la ficha Examinar.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. En el flujo de trabajo, continúe con el paso **Programación** y seleccione **Editar programación**.
   ![Editar control de programación resaltado en el paso Programación.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Elija una fecha de finalización deseada después del 1 de mayo de 2025 y seleccione **Guardar**.
   ![Seleccione el control de fecha de finalización resaltado en el paso Programación.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Continúe al final del flujo de trabajo y guarde las actualizaciones.

Para obtener información detallada sobre el paso de programación, lea el tutorial de la interfaz de usuario [exportar conjuntos de datos](/help/destinations/api/export-datasets.md#scheduling).

## Utilice la API para actualizar la fecha de finalización

### Buscar los flujos de datos que deben actualizarse

### Actualizar la fecha de finalización de los flujos de datos
