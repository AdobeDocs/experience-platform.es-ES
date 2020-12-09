---
keywords: Experience Platform;home;popular topics;update accounts
description: En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El espacio de trabajo Fuentes le permite agregar, editar y eliminar detalles de un lote o una conexión de flujo existente, incluido su nombre, descripción y credenciales.
solution: Experience Platform
title: Actualizar los detalles de la cuenta en la interfaz de usuario
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 9b48bc1426e6259ea0b2cf9b420b55b92712f7c2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Actualizar los detalles de la cuenta en la interfaz de usuario

En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El espacio de trabajo [!UICONTROL Fuentes] le permite agregar, editar y eliminar detalles de una conexión de flujo o lote existente, incluido su nombre, descripción y credenciales.

Este tutorial proporciona pasos para actualizar los detalles y las credenciales de una cuenta existente desde el espacio de trabajo [!UICONTROL Fuentes] .

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): El Experience Platform DNL permite la ingesta de datos desde diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
- [Simuladores](../../../sandboxes/home.md): DNL Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Actualizar cuentas

Inicie sesión en la interfaz de usuario [del](https://platform.adobe.com) Experience Platform y, a continuación, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Fuentes] . Seleccione **[!UICONTROL Cuentas]** del encabezado superior para vista de cuentas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

Aparece la página **[!UICONTROL Cuentas]** . En esta página hay una lista de cuentas visualizables, que incluye información sobre su origen, nombre de usuario, número de flujos de datos y fecha de creación.

Seleccione el ![filtro](../../images/tutorials/update/filter.png) de icono de filtro en la parte superior izquierda para iniciar el panel de ordenación.

![cuentas-lista](../../images/tutorials/update/accounts-list.png)

El panel Ordenar proporciona una lista de todas las fuentes. Puede seleccionar más de un origen de la lista para acceder a una selección filtrada de cuentas asociadas con diferentes orígenes.

Seleccione el origen con el que desea trabajar para ver una lista de sus cuentas existentes. Una vez identificada la cuenta que desea actualizar, seleccione las elipses (`...`) al lado del nombre de la cuenta.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Aparece un menú desplegable con opciones para **[!UICONTROL Añadir datos]**, **[!UICONTROL editar detalles]** y **[!UICONTROL eliminar]**. Seleccione **[!UICONTROL Editar detalles]** en el menú para actualizar la cuenta.

![update](../../images/tutorials/update/update.png)

El cuadro de diálogo **[!UICONTROL Editar detalles]** de la cuenta le permite actualizar el nombre, la descripción y las credenciales de autenticación de una cuenta. Una vez que haya actualizado la información deseada, seleccione **[!UICONTROL Guardar]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Al cabo de unos minutos, aparece un cuadro de confirmación verde en la parte inferior de la pantalla para confirmar que la actualización se ha realizado correctamente.

![actualización confirmada](../../images/tutorials/update/update-confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Fuentes] para actualizar la información de la cuenta.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación mediante la [!DNL Flow Service] API, consulte el tutorial sobre la [actualización de la información de conexión mediante la API](../../tutorials/api/update.md)de servicio de flujo.