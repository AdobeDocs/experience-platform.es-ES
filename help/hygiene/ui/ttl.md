---
title: Administrar TTL de conjuntos de datos
description: Aprenda a programar un tiempo de vida (TTL) para un conjunto de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Administrar TTL de conjuntos de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido Escudo de Adobe para la atención médica.

La variable [[!UICONTROL Higiene de los datos] workspace](./overview.md) en la interfaz de usuario de Adobe Experience Platform le permite programar un tiempo de vida (TTL) para un conjunto de datos.

Este documento explica cómo programar y administrar los TTL de conjuntos de datos en la interfaz de usuario de Platform.

## Programar un TTL

Para crear una solicitud nueva, seleccione **[!UICONTROL Crear solicitud]** desde la página principal del espacio de trabajo.

![Imagen que muestra la variable [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/ttl/create-request-button.png)

Aparecerá el cuadro de diálogo de creación de solicitudes. En el **[!UICONTROL Acción]** , seleccione **[!UICONTROL Conjunto de datos]** para actualizar los controles disponibles para la programación TTL.

![Imagen que muestra la variable [!UICONTROL Conjunto de datos] opción seleccionada](../images/ui/ttl/create-request-button.png)

### Seleccionar una fecha y un conjunto de datos

En el **[!UICONTROL Acción]** , seleccione una fecha para la que desee eliminar el conjunto de datos. Puede introducir la fecha manualmente (con el formato `mm/dd/yyyy`) o seleccione el icono de calendario (![Imagen del icono del calendario](../images/ui/ttl/calendar-icon.png)) para seleccionar la fecha en un cuadro de diálogo.

![Imagen que muestra una fecha de caducidad establecida para el TTL](../images/ui/ttl/select-date.png)

A continuación, en **[!UICONTROL Detalles del conjunto de datos]**, seleccione el icono de base de datos (![Imagen del icono de la base de datos](../images/ui/ttl/database-icon.png)) para abrir un cuadro de diálogo de selección de conjuntos de datos. Elija un conjunto de datos de la lista a la que aplicar el TTL y, a continuación, seleccione **[!UICONTROL Listo]**.

![Imagen que muestra un conjunto de datos seleccionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Solo se muestran los conjuntos de datos que pertenecen al entorno limitado actual.

### Enviar la solicitud

Una vez que haya seleccionado un conjunto de datos y una fecha TTL, seleccione **[!UICONTROL Submit]**.

![Imagen que muestra la variable [!UICONTROL Submit] botón seleccionado](../images/ui/ttl/select-dataset.png)

Se le pedirá que confirme la fecha en la que eliminará el conjunto de datos. Select **[!UICONTROL Submit]** para continuar.

Una vez enviada la solicitud, se crea una orden de trabajo que aparece en la [!UICONTROL Consumidor] de la pestaña [!UICONTROL Higiene de los datos] espacio de trabajo. Desde aquí, puede controlar el estado de la orden de trabajo a medida que procesa la solicitud.

## Editar o cancelar un TTL

Para editar o cancelar un TTL, seleccione **[!UICONTROL Conjunto de datos]** en la página principal del espacio de trabajo y seleccione el TTL en la lista.

En la página de detalles del TTL, el carril derecho muestra los controles para editar o cancelar la eliminación programada.

## Pasos siguientes

Este documento trataba sobre cómo programar TTL de conjuntos de datos en la interfaz de usuario del Experience Platform. Para obtener información sobre cómo realizar otras tareas de higiene de datos en la interfaz de usuario, consulte [información general sobre la interfaz de usuario de higiene de datos](./overview.md).

Para aprender a programar TTL de conjuntos de datos mediante la API de higiene de datos, consulte la [guía de extremo de TTL del conjunto de datos](../api/ttl.md).
