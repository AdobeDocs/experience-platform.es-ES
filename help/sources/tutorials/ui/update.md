---
keywords: Experience Platform;inicio;temas populares;actualizar cuentas
description: En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El área de trabajo Fuentes permite agregar, editar y eliminar detalles de una conexión de flujo continuo o por lotes existente, incluidos el nombre, la descripción y las credenciales.
solution: Experience Platform
title: Actualización de los detalles de la cuenta de Source Connection en la IU
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Actualización de los detalles de la cuenta en la IU

En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El área de trabajo [!UICONTROL Sources] le permite agregar, editar y eliminar detalles de una conexión de flujo continuo o por lotes existente, incluidos el nombre, la descripción y las credenciales.

Este tutorial proporciona los pasos para actualizar los detalles y las credenciales de una cuenta existente del área de trabajo [!UICONTROL Sources].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
- [Zonas protegidas](../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Actualización de cuentas

Inicie sesión en la [interfaz de usuario del Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo de [!UICONTROL Fuentes]. Seleccione **[!UICONTROL Cuentas]** del encabezado superior para ver las cuentas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

Aparecerá la página **[!UICONTROL Cuentas]**. En esta página hay una lista de cuentas visibles, que incluye información sobre su fuente, nombre de usuario, número de flujos de datos y fecha de creación.

Seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para iniciar el panel de ordenación.

![lista de cuentas](../../images/tutorials/update/accounts-list.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de un origen en la lista para acceder a una selección filtrada de cuentas asociadas con diferentes orígenes.

Seleccione el origen con el que desea trabajar para ver una lista de sus cuentas existentes. Una vez identificada la cuenta que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta.

![cuentas-ordenar](../../images/tutorials/update/accounts-sort.png)

Aparece un menú desplegable que le proporciona opciones para **[!UICONTROL Agregar datos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]**. Seleccione **[!UICONTROL Editar detalles]** del menú para actualizar su cuenta.

![actualización del estado](../../images/tutorials/update/update.png)

El cuadro de diálogo **[!UICONTROL Editar detalles de la cuenta]** le permite actualizar el nombre, la descripción y las credenciales de autenticación de una cuenta. Una vez que hayas actualizado la información deseada, selecciona **[!UICONTROL Guardar]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la actualización se ha realizado correctamente.

![actualización confirmada](../../images/tutorials/update/update-confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el área de trabajo [!UICONTROL Sources] para actualizar la información de una cuenta de origen existente.

Para obtener información sobre cómo realizar estas operaciones mediante programación usando la API [!DNL Flow Service], consulte el tutorial sobre [actualización de información de conexión mediante la API de Flow Service](../../tutorials/api/update.md).
