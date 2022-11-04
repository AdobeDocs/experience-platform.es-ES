---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Permisos de la función Administración de controles de acceso basados en atributos
description: Este documento proporciona información sobre la configuración de permisos para una función a través de la interfaz Permisos en Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: a94cf02a57bd91d2342b53ced7da98836343aa2b
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 4%

---

# Administrar permisos para una función

>[!IMPORTANT]
>
>El control de acceso utiliza el ID de usuario (un identificador único interno asignado a un usuario) para conceder permisos. Cuando se migra una organización de Adobe ID a un ID empresarial, todos los permisos establecidos para sus usuarios se pierden porque el ID de usuario cambia y el control de acceso utilizará el ID de usuario recién generado. Si su organización se migra a Business ID, póngase en contacto con su representante de Adobe para migrar su ID de usuario de Adobe ID a Business ID.

Los permisos son el área del Experience Cloud en la que los administradores pueden definir funciones de usuario y políticas de acceso para administrar los permisos de acceso a funciones y objetos dentro de una aplicación de producto.

Mediante Permisos de , , puede crear y administrar funciones, así como asignar los permisos de recursos deseados para estas. Los permisos también le permiten administrar las etiquetas, las zonas protegidas y los usuarios asociados a una función específica.

Inmediatamente después de [creación de una función nueva](#create-a-new-role), volverá a la **[!UICONTROL Funciones]** pestaña . Si está editando permisos para una función existente, seleccione la función en la **[!UICONTROL Funciones]** pestaña . Como alternativa, utilice la opción de filtro para filtrar los resultados y encontrar una función.

## Filtrar funciones

Seleccione el icono de canal (![Icono de filtro](../../images/icon.png)) para mostrar una lista de controles de filtro para ayudar a reducir los resultados.

![flac-filters](../../images/flac-ui/flac-filters.png)

Los siguientes filtros están disponibles para las funciones en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Creado entre] | Seleccione una fecha de inicio o una fecha de finalización para definir un intervalo de fechas por el que filtrar los resultados. |
| [!UICONTROL Creado por] | Filtre por creador de funciones seleccionando un usuario en la lista desplegable. |
| [!UICONTROL Modificado entre] | Seleccione una fecha de inicio o una fecha de finalización para definir un intervalo de fechas por el que filtrar los resultados. |
| [!UICONTROL Modificado por] | Filtre por modificador de funciones seleccionando un usuario en la lista desplegable. |

Para quitar un filtro, seleccione la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o seleccione **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Detalles de la función

Seleccione la función de la variable **[!UICONTROL Funciones]** , que abrirá la página de detalles de la función.

![flac-details](../../images/flac-ui/flac-details.png)

La pestaña de detalles proporciona una descripción general de la función. La descripción general muestra el nombre del rol, la descripción del rol, el nombre del usuario que creó y modificó el rol, cuándo se creó y modificó, y los permisos adjuntos al rol. Si es necesario, se pueden modificar el nombre de la función y la descripción de la función.

## Administrar etiquetas para una función

Seleccione el **[!UICONTROL Etiquetas]** para abrir la página de etiquetas de funciones y, a continuación, seleccione **[!UICONTROL Agregar etiquetas]** para asignar etiquetas a la función.

![flac-label](../../images/flac-ui/flac-labels.png)

Las etiquetas se muestran en esta página. La lista muestra el nombre de la etiqueta, el nombre descriptivo, la categoría y su descripción.

Seleccione las etiquetas de la lista que desee agregar a la función y, a continuación, seleccione **[!UICONTROL Guardar]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

Las etiquetas agregadas aparecen en **[!UICONTROL Etiquetas]** pestaña .

![flac-added-labels](../../images/flac-ui/flac-added-labels.png)

Para quitar una etiqueta de una función, seleccione **X** junto al nombre de las etiquetas.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Administración de entornos limitados para la función

Seleccione el **[!UICONTROL Sandboxes]** para abrir la página de entornos limitados de roles. Aquí puede ver una lista de entornos limitados que se agregaron al rol.

![flac-sandboxes](../../images/flac-ui/flac-sandboxes.png)

Para agregar más entornos limitados a una función, seleccione **[!UICONTROL Editar]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

La siguiente pantalla le pedirá que elija qué permisos de recursos existen en los entornos limitados para incluir en la función mediante la lista desplegable. Cuando termine, seleccione **[!UICONTROL Guardar y salir]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Administración de usuarios para la función

Seleccione el **[!UICONTROL Usuarios]** pestaña para abrir la página usuarios de roles y, a continuación, seleccione **[!UICONTROL Agregar usuarios]** para asignar usuarios a la función.

![flac-users](../../images/flac-ui/flac-users.png)

Seleccione a los usuarios de la lista que desee agregar a la función. También puede utilizar la barra de búsqueda para buscar al usuario introduciendo su nombre o dirección de correo electrónico y, a continuación, seleccionar **[!UICONTROL Guardar]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

Los usuarios añadidos aparecen en **[!UICONTROL Usuarios]** pestaña .

![flac-added-users](../../images/flac-ui/flac-added-users.png)

Para quitar un usuario de una función, seleccione la opción **X** junto al nombre del usuario.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## Administración de credenciales de API para la función

Seleccione el **[!UICONTROL Credenciales de API]** para abrir la página de credenciales de la API de roles y, a continuación, seleccione **[!UICONTROL Agregar credenciales de API]** para asignar credenciales de API a la función.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Seleccione las credenciales de API de la lista que desee agregar a la función y, a continuación, seleccione **[!UICONTROL Guardar]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Las credenciales de API agregadas aparecen en **[!UICONTROL Credenciales de API]** pestaña .

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Para quitar credenciales de API de una función, seleccione la opción **X** junto al nombre de las credenciales de API.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

La variable **[!UICONTROL Eliminación de credenciales de API]** , solicitando que confirme la eliminación.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Volverá a la **[!UICONTROL Credenciales de API]** pestaña .

## Administración de grupos de usuarios para funciones

Los grupos de usuarios son varios usuarios que se han agrupado y tienen acceso para ejecutar las mismas funciones.

Seleccione el **[!UICONTROL Grupos de usuarios]** pestaña para abrir la página de grupos de usuarios de roles y, a continuación, seleccione **[!UICONTROL Agregar grupos]** para asignar grupos de usuarios a la función.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

Seleccione los grupos de usuarios de la lista que desee agregar a la función. Como alternativa, utilice la barra de búsqueda para buscar el grupo de usuarios introduciendo el nombre del grupo y, a continuación, seleccione **[!UICONTROL Guardar]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

El grupo de usuarios añadido aparece en **[!UICONTROL Grupos de usuarios]** pestaña .

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Para quitar un grupo de usuarios de una función, seleccione **X** junto al nombre del grupo de usuarios.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

La variable **[!UICONTROL Quitar grupo de usuarios]** , solicitando que confirme la eliminación.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Volverá a la **[!UICONTROL Grupos de usuarios]** pestaña .

## Añadir usuarios al Experience Platform a través de un perfil de producto

Para agregar un usuario a un perfil de producto, inicie sesión en el Admin Console y seleccione **[!UICONTROL Agregar usuarios]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

La variable **[!UICONTROL Agregar usuarios a su equipo]** se abre. Introduzca la dirección de correo electrónico, el nombre (opcional) y los apellidos del usuario (opcional).

Seleccione el icono de lápiz para seleccionar productos y grupos de usuarios, seleccione **[!UICONTROL Adobe Experience Platform]** y, a continuación, seleccione **[!UICONTROL AEP-Default-All-Users]** y, a continuación, seleccione  **[!UICONTROL Guardar]**.

![product-profile](../../images/flac-ui/product-profile.png)

## Pasos siguientes

Con los permisos establecidos, puede continuar con el paso siguiente a [administrar usuarios](users.md).
