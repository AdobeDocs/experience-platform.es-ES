---
keywords: Experience Platform;inicio;temas populares;actualizar cuentas
description: En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El espacio de trabajo Orígenes permite agregar, editar y eliminar detalles de un lote o conexión de flujo continuo existente, como su nombre, descripción y credenciales.
solution: Experience Platform
title: Actualizar los detalles de la cuenta de conexión de origen en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Actualizar los detalles de la cuenta en la interfaz de usuario

En algunas circunstancias, puede ser necesario actualizar los detalles de una cuenta de fuentes existente. El espacio de trabajo [!UICONTROL Sources] permite agregar, editar y eliminar detalles de una conexión de flujo continuo o por lotes existente, como su nombre, descripción y credenciales.

Este tutorial proporciona pasos para actualizar los detalles y las credenciales de una cuenta existente desde el espacio de trabajo [!UICONTROL Sources].

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
- [Simuladores para pruebas](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Actualizar cuentas

Inicie sesión en la [IU del Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. Seleccione **[!UICONTROL Accounts]** en el encabezado superior para ver las cuentas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

Aparece la página **[!UICONTROL Accounts]**. En esta página hay una lista de cuentas visibles que incluye información sobre su origen, nombre de usuario, número de flujos de datos y fecha de creación.

Seleccione el icono de filtro ![filter](../../images/tutorials/update/filter.png) en la parte superior izquierda para iniciar el panel de ordenación.

![lista de cuentas](../../images/tutorials/update/accounts-list.png)

El panel de ordenación proporciona una lista de todas las fuentes. Puede seleccionar más de una fuente de la lista para acceder a una selección filtrada de cuentas asociadas a diferentes fuentes.

Seleccione la fuente con la que desee trabajar para ver una lista de sus cuentas existentes. Una vez identificada la cuenta que desea actualizar, seleccione los puntos suspensivos (`...`) junto al nombre de la cuenta.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Aparece un menú desplegable que proporciona las opciones **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** y **[!UICONTROL Delete]**. Seleccione **[!UICONTROL Edit details]** en el menú para actualizar su cuenta.

![actualizar](../../images/tutorials/update/update.png)

El cuadro de diálogo **[!UICONTROL Edit account details]** permite actualizar el nombre, la descripción y las credenciales de autenticación de una cuenta. Una vez que haya actualizado la información deseada, seleccione **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Después de unos momentos, aparece un cuadro de confirmación en la parte inferior de la pantalla para confirmar que la actualización se ha realizado correctamente.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Pasos siguientes

Siguiendo este tutorial, ha utilizado correctamente el espacio de trabajo [!UICONTROL Sources] para actualizar la información de una cuenta de origen existente.

Para ver los pasos sobre cómo realizar estas operaciones mediante programación utilizando la API [!DNL Flow Service], consulte el tutorial sobre la [actualización de la información de conexión mediante la API de servicio de flujo](../../tutorials/api/update.md).
