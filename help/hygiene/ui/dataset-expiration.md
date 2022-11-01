---
title: Administrar caducidad del conjunto de datos
description: Obtenga información sobre cómo programar una caducidad de un conjunto de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Administrar caducidades del conjunto de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos en Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

La variable [[!UICONTROL Higiene de los datos] workspace](./overview.md) en la interfaz de usuario de Adobe Experience Platform le permite programar caducidades para conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos separados para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez que se eliminan los datos de los tres servicios, la caducidad se marca como completa.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente cualquier flujo de datos que pueda estar introduciendo datos en ese conjunto de datos para que sus flujos de trabajo descendentes no se vean afectados negativamente.

Este documento explica cómo programar y administrar las caducidades de los conjuntos de datos en la interfaz de usuario de Platform.

## Programar una caducidad del conjunto de datos

Para crear una solicitud nueva, seleccione **[!UICONTROL Crear solicitud]** desde la página principal del espacio de trabajo.

![Imagen que muestra la variable [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/ttl/create-request-button.png)

Aparecerá el cuadro de diálogo de creación de solicitudes. En el **[!UICONTROL Acción solicitada]** , seleccione **[!UICONTROL Eliminar conjunto de datos]** para actualizar los controles disponibles para la programación de caducidad del conjunto de datos.

![Imagen que muestra la variable [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/ttl/dataset-selected.png)

### Seleccionar una fecha y un conjunto de datos

Aparecerá el cuadro de diálogo de creación de solicitudes. En el **[!UICONTROL Acción solicitada]** , seleccione una fecha para la que desee eliminar el conjunto de datos. Puede introducir la fecha manualmente (con el formato `mm/dd/yyyy`) o seleccione el icono de calendario (![Imagen del icono del calendario](../images/ui/ttl/calendar-icon.png)) para seleccionar la fecha en un cuadro de diálogo.

![Imagen que muestra una fecha de caducidad establecida para el conjunto de datos](../images/ui/ttl/select-date.png)

A continuación, en **[!UICONTROL Detalles del conjunto de datos]**, seleccione el icono de base de datos (![Imagen del icono de la base de datos](../images/ui/ttl/database-icon.png)) para abrir un cuadro de diálogo de selección de conjuntos de datos. Elija un conjunto de datos de la lista a la que aplicar la caducidad y, a continuación, seleccione **[!UICONTROL Listo]**.

![Imagen que muestra un conjunto de datos seleccionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Solo se muestran los conjuntos de datos que pertenecen al entorno limitado actual.

### Enviar la solicitud

La variable [!UICONTROL Detalles del conjunto de datos] se rellena para incluir la identidad principal y el esquema para el conjunto de datos seleccionado. En **[!UICONTROL Configuración de solicitud]**, introduzca un nombre y una descripción opcional para la solicitud, seguido de **[!UICONTROL Submit]**.

![Imagen que muestra la variable [!UICONTROL Submit] botón seleccionado](../images/ui/ttl/submit.png)

Se le pedirá que confirme la fecha en la que eliminará el conjunto de datos. Select **[!UICONTROL Submit]** para continuar.

Una vez enviada la solicitud, se crea una orden de trabajo que aparece en la pestaña principal del [!UICONTROL Higiene de los datos] espacio de trabajo. Desde aquí, puede controlar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección Información general de [plazos y transparencia](../home.md#dataset-expiration-transparency) para obtener más información sobre cómo se procesan las caducidades de los conjuntos de datos una vez que se ejecutan.

## Editar o cancelar una caducidad del conjunto de datos

Para editar o cancelar una caducidad del conjunto de datos, seleccione **[!UICONTROL Conjunto de datos]** en la página principal del espacio de trabajo y seleccione la caducidad del conjunto de datos en la lista.

En la página de detalles de la caducidad del conjunto de datos, el carril derecho muestra los controles para editar o cancelar la eliminación programada.

## Pasos siguientes

Este documento trata sobre cómo programar caducidades de conjuntos de datos en la interfaz de usuario del Experience Platform. Para obtener información sobre cómo realizar otras tareas de higiene de datos en la interfaz de usuario, consulte [información general sobre la interfaz de usuario de higiene de datos](./overview.md).

Para aprender a programar caducidades del conjunto de datos mediante la API de higiene de datos, consulte la [guía de extremo de caducidad del conjunto de datos](../api/dataset-expiration.md).
