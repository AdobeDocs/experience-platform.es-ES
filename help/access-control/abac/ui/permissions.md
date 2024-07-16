---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Control de acceso basado en atributos Administrar permisos de funciones
description: Este documento proporciona información sobre la configuración de permisos para una función a través de la interfaz Permisos en Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c1c7a851315214e2362085d3283d144066d4dd8a
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# Administración de permisos de una función

>[!IMPORTANT]
>
>El control de acceso utiliza un ID de usuario (un ID único interno asignado a un usuario) para conceder permisos. Cuando se migra una organización de Adobe ID a un ID empresarial, se perderán todos los permisos establecidos para sus usuarios, ya que el ID de usuario cambia y el control de acceso utiliza el ID de usuario recién generado. Si su organización se migra a un ID empresarial, póngase en contacto con su representante de Adobe para migrar su ID de usuario de Adobe ID a un ID empresarial.

Permisos es el área del Experience Cloud donde los administradores pueden definir funciones de usuario y directivas de acceso para administrar permisos de acceso para funciones y objetos dentro de una aplicación de producto.

Mediante Permisos, puede crear y administrar funciones, así como asignar los permisos de recursos deseados para estas. Los permisos también le permiten administrar las etiquetas, las zonas protegidas y los usuarios asociados a una función específica.

Inmediatamente después de que [cree un nuevo rol](#create-a-new-role), volverá a la ficha **[!UICONTROL Roles]**. Si está editando permisos para una función existente, seleccione la función en la ficha **[!UICONTROL Funciones]**. También puede utilizar la opción de filtro para filtrar los resultados y encontrar un rol.

## Filtrar funciones

Seleccione el icono de canal (![Icono de filtro](../../images/icon.png)) para mostrar una lista de controles de filtro y ayudar a reducir los resultados.

![flac-filters](../../images/flac-ui/flac-filters.png)

Los siguientes filtros están disponibles para las funciones en la interfaz de usuario:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Creado entre] | Seleccione una fecha de inicio o de finalización para definir un intervalo de fechas en el que filtrar los resultados. |
| [!UICONTROL Creado por] | Filtre por creador de funciones seleccionando un usuario en la lista desplegable. |
| [!UICONTROL Modificado entre] | Seleccione una fecha de inicio o de finalización para definir un intervalo de fechas en el que filtrar los resultados. |
| [!UICONTROL Modificado por] | Filtre por modificador de función seleccionando un usuario en la lista desplegable. |

Para quitar un filtro, selecciona la &quot;X&quot; en el icono de la píldora para el filtro en cuestión o selecciona **[!UICONTROL Borrar todo]** para eliminar todos los filtros.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Detalles del rol

Seleccione el rol en la ficha **[!UICONTROL Roles]**, la cual abrirá la página de detalles del rol.

![flac-details](../../images/flac-ui/flac-details.png)

La pestaña de detalles proporciona una descripción general de la función. La descripción general muestra el nombre de la función, la descripción de la función, el nombre del usuario que creó y modificó la función, cuándo se creó y modificó la función y los permisos asociados a la función. Si es necesario, se pueden modificar el nombre y la descripción de la función.

## Administrar etiquetas de un rol

Seleccione la ficha **[!UICONTROL Etiquetas]** para abrir la página de etiquetas de roles y, a continuación, seleccione **[!UICONTROL Agregar etiquetas]** para asignar etiquetas al rol.

![etiquetas flac](../../images/flac-ui/flac-labels.png)

Las etiquetas se muestran en esta página. La lista muestra el nombre de la etiqueta, el nombre descriptivo, la categoría y su descripción.

Seleccione las etiquetas de la lista que desee agregar al rol y después seleccione **[!UICONTROL Guardar]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

Las etiquetas agregadas aparecen en la ficha **[!UICONTROL Etiquetas]**.

![flac-added-labels](../../images/flac-ui/flac-added-labels.png)

Para quitar una etiqueta de un rol, seleccione el icono **X** junto al nombre de las etiquetas.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Administración de zonas protegidas para la función

Seleccione la ficha **[!UICONTROL Zonas protegidas]** para abrir la página de zonas protegidas de funciones. Aquí puede ver una lista de las zonas protegidas que se agregaron a la función.

![zonas protegidas flac](../../images/flac-ui/flac-sandboxes.png)

Para agregar más zonas protegidas a un rol, seleccione **[!UICONTROL Editar]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

La siguiente pantalla le solicita que elija qué permisos de recursos que existen en los entornos limitados se incluirán en la función con la lista desplegable. Cuando termine, seleccione **[!UICONTROL Guardar y salir]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Administrar usuarios para la función

Seleccione la ficha **[!UICONTROL Usuarios]** para abrir la página de roles de usuarios y, a continuación, seleccione **[!UICONTROL Agregar usuarios]** para asignar usuarios al rol.

![flac-users](../../images/flac-ui/flac-users.png)

Seleccione los usuarios de la lista que desee agregar al rol. También puede usar la barra de búsqueda para buscar al usuario al escribir su nombre o dirección de correo electrónico y, a continuación, seleccionar **[!UICONTROL Guardar]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

Los usuarios agregados aparecen en la ficha **[!UICONTROL Usuarios]**.

![flac-added-users](../../images/flac-ui/flac-added-users.png)

Para quitar un usuario de un rol, seleccione el icono **X** junto al nombre del usuario.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

El siguiente vídeo tiene como objetivo ayudarle a comprender la creación de una función nueva y a administrar usuarios para esa función.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Administrar credenciales de API para la función {#manage-api-credentials-for-role}

Seleccione la ficha **[!UICONTROL Credenciales de API]** para abrir la página de credenciales de API de roles y, a continuación, seleccione **[!UICONTROL Agregar credenciales de API]** para asignar credenciales de API al rol.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Seleccione las credenciales de la API de la lista que desee agregar al rol y, a continuación, seleccione **[!UICONTROL Guardar]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Las credenciales de API agregadas aparecen en la ficha **[!UICONTROL Credenciales de API]**.

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Para quitar credenciales de API de un rol, seleccione el icono **X** junto al nombre de la credencial de API.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

Aparece el cuadro de diálogo **[!UICONTROL Quitar credenciales de API]**, que le solicita que confirme la eliminación.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Se le devolverá a la ficha **[!UICONTROL Credenciales de API]**.

## Administración de grupos de usuarios para funciones

Los grupos de usuarios son varios usuarios que se han agrupado y tienen acceso para ejecutar las mismas funciones.

Seleccione la ficha **[!UICONTROL Grupos de usuarios]** para abrir la página de roles, grupos de usuarios y, a continuación, seleccione **[!UICONTROL Agregar grupos]** para asignar grupos de usuarios al rol.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

Seleccione los grupos de usuarios de la lista que desee agregar a la función. También puede usar la barra de búsqueda para buscar el grupo de usuarios al escribir el nombre del grupo y seleccionar **[!UICONTROL Guardar]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

El grupo de usuarios agregados aparece en la ficha **[!UICONTROL Grupos de usuarios]**.

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Para quitar un grupo de usuarios de un rol, seleccione el icono **X** junto al nombre del grupo de usuarios.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

Aparece el cuadro de diálogo **[!UICONTROL Quitar grupo de usuarios]**, que le solicita que confirme la eliminación.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Volverá a la ficha **[!UICONTROL Grupos de usuarios]**.

## Adición de usuarios al Experience Platform mediante una función

Para agregar un usuario a un rol, inicia sesión en el Admin Console y selecciona **[!UICONTROL Agregar usuarios]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Agregar usuarios a su equipo]**. Introduzca la dirección de correo electrónico del usuario, el nombre (opcional) y los apellidos (opcional).

Seleccione el icono de lápiz para seleccionar productos y grupos de usuarios, seleccione **[!UICONTROL Adobe Experience Platform]**, a continuación, seleccione **[!UICONTROL AEP-Default-All-Users]** y después seleccione **[!UICONTROL Guardar]**.

![perfil de producto](../../images/flac-ui/product-profile.png)

## Pasos siguientes

Con los permisos establecidos, puede continuar con el siguiente paso para [administrar usuarios](users.md).
