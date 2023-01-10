---
keywords: Experience Platform;inicio;temas populares;actualizar cuentas
description: En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El espacio de trabajo Orígenes permite agregar, editar y eliminar detalles de un lote o conexión de flujo continuo existente, como su nombre, descripción y credenciales.
solution: Experience Platform
title: Actualizar los detalles de la cuenta de conexión de origen en la interfaz de usuario
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Actualizar los detalles de la cuenta en la interfaz de usuario

En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. La variable [!UICONTROL Fuentes] workspace le permite agregar, editar y eliminar detalles de un lote o conexión de flujo continuo existente, como su nombre, descripción y credenciales.

Este tutorial proporciona pasos para actualizar los detalles y las credenciales de una cuenta existente desde la [!UICONTROL Fuentes] espacio de trabajo.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
- [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Actualizar cuentas

Inicie sesión en la [IU de Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. Select **[!UICONTROL Cuentas]** en el encabezado superior para ver las cuentas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

La variable **[!UICONTROL Cuentas]** se abre. En esta página hay una lista de cuentas visibles que incluye información sobre su origen, nombre de usuario, número de flujos de datos y fecha de creación.

Seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para iniciar el panel de ordenación.

![lista de cuentas](../../images/tutorials/update/accounts-list.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de cuentas asociadas a diferentes fuentes.

Seleccione la fuente con la que desee trabajar para ver una lista de sus cuentas existentes. Una vez identificada la cuenta que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Aparece un menú desplegable que le proporciona las opciones para **[!UICONTROL Añadir datos]**, **[!UICONTROL Editar detalles]** y **[!UICONTROL Eliminar]**. Select **[!UICONTROL Editar detalles]** en el menú para actualizar su cuenta.

![actualizar](../../images/tutorials/update/update.png)

La variable **[!UICONTROL Editar detalles de la cuenta]** permite actualizar el nombre, la descripción y las credenciales de autenticación de una cuenta. Una vez que haya actualizado la información deseada, seleccione **[!UICONTROL Guardar]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la actualización se ha realizado correctamente.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Pasos siguientes

Al seguir este tutorial, ha utilizado correctamente la variable [!UICONTROL Fuentes] espacio de trabajo para actualizar la información de una cuenta de origen existente.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación usando la variable [!DNL Flow Service] API, consulte el tutorial sobre [actualización de la información de conexión mediante la API de servicio de flujo](../../tutorials/api/update.md).
