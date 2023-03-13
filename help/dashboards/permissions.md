---
solution: Experience Platform
title: Cómo obtener y conceder permisos de acceso para paneles de Experience Platform
type: Documentation
description: Conceda a los usuarios la capacidad de ver, editar y actualizar paneles de Experience Platform mediante Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 7%

---

# Permisos de acceso para paneles

Para conceder a los usuarios la capacidad de ver, editar y actualizar paneles, primero debe habilitar los permisos. En Adobe Experience Platform, el control de acceso se proporciona a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com/). Los usuarios están vinculados con permisos y zonas protegidas a través de perfiles de producto en [!DNL Admin Console].

Este documento proporciona un resumen de los permisos disponibles para los paneles, incluidas las funciones a las que proporcionan acceso y las funciones de usuario que habilitan. Para obtener información detallada sobre cómo obtener y asignar permisos de acceso, comience por leer el [información general de control de acceso](../access-control/home.md).

## Requisitos previos

Para configurar el control de acceso de [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga un [!DNL Experience Platform] integración del producto. Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

## Permisos de tablero disponibles {#available-permissions}

El [!DNL Dashboards] proporciona tres permisos que, combinados, proporcionan acceso completo al [!UICONTROL Perfiles], [!UICONTROL Segmentos], [!UICONTROL Destinos], y [!UICONTROL Uso de licencias] paneles dentro de Adobe Experience Platform. Estos permisos son:

| Permiso | Descripción |
|---|---|
| **Administrar paneles estándar** | Este permiso es un **permiso global de lectura y escritura**. Le permite hacer lo siguiente [crear widgets personalizados](./customize/custom-widgets.md) y [editar el esquema del widget](./customize/edit-schema.md) a través de [!UICONTROL Biblioteca de widgets]. |
| **Ver paneles estándar** | Esto proporciona lo siguiente **de solo lectura** funcionalidad para [!UICONTROL Perfiles], [!UICONTROL Destinos], y [!UICONTROL Segmentos] paneles y permite acceder a ellos a través de la navegación izquierda de Platform. También agrega [!UICONTROL Paneles] a la navegación izquierda y acceso a la [!UICONTROL Paneles] pestaña inventario e integraciones. |
| **Ver tablero de uso de licencias** | Permite a los usuarios **de solo lectura** acceso a [el tablero de uso de licencias](./guides/license-usage.md) en la interfaz de usuario de Experience Platform. |

Hay cinco permisos que no se incluyen en la [!DNL Dashboard] categorías que pueden ser necesarias según sus necesidades. En la tabla siguiente se describen las ubicaciones de las categorías en el Admin Console:

>[!IMPORTANT]
>
>Tanto la **[!DNL Manage Standard Dashboards]** y el **[!DNL View Standard Dashboards]** permissions **requerir** un permiso de &quot;vista&quot; o &quot;administración&quot; del [!DNL Profile Management] o [!DNL Destinations] en el Admin Console para activar las secciones relevantes dentro de la interfaz de usuario de Platform.

| Permiso | ubicación de categoría de Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de control de acceso

La siguiente matriz de control de acceso proporciona un desglose de los permisos necesarios y qué función proporcionan con respecto al acceso a las diferentes funciones del panel. Los permisos se muestran en la fila horizontal superior y el espacio de trabajo de la IU de Platform a lo largo de la columna izquierda.

|  | [!UICONTROL Ver tablero estándar] O [!UICONTROL Administrar tablero estándar] | [!UICONTROL Ver perfiles],<br/>[!UICONTROL Ver segmentos],<br/> [!UICONTROL Ver destinos] | [!UICONTROL Administrar consultas] &amp; [!UICONTROL Administrar zonas protegidas] | [!UICONTROL Ver tablero de uso de licencias] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] en el panel de navegación izquierdo. | N/A | **Se REQUIERE un permiso de &quot;Ver&quot; o &quot;Administrar&quot;** para cada tablero respectivo. | N/A | N/A |
| [!DNL Dashboards] en el panel de navegación izquierdo. | HABILITADO | **Al menos uno REQUERIDO**. | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/>(la pestaña examinar) | HABILITADO | N/A | N/A | N/A |
| [!DNL Dashboards] [!DNL Integrations] pestaña <br/>(se usa para instalar Power BI) | HABILITADO | **Al menos uno REQUERIDO** | N/A | N/A |
| Botón Instalar y flujo de trabajo de Power BI | HABILITADO | N/A | **OBLIGATORIO** | N/A |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] paneles.<br/>La capacidad de editar esquemas de widgets y añadir nuevos atributos para la personalización de widgets | **Manage-standard-dashboard REQUERIDO** | **OBLIGATORIO (para cada tablero respectivo)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | HABILITADO |

{style="table-layout:auto"}

## Adición de permisos al perfil del producto

Utilice la información proporcionada anteriormente para agregar los permisos adecuados al perfil del producto. Consulte la documentación para obtener instrucciones completas sobre [Cómo añadir permisos a través de la IU de control de acceso](../access-control/ui/permissions.md).

Para obtener descripciones de los permisos, consulte la [permisos disponibles](#available-permissions) anteriormente en este documento.

>[!NOTE]
>
>No tiene que habilitar todos los permisos para todos los usuarios. Según la estructura de su organización, es posible que desee crear perfiles de producto independientes para determinados usuarios y conceder acceso limitado (como solo lectura). Consulte la documentación sobre la administración de usuarios para ver un perfil de producto para obtener más información [cómo asignar permisos a usuarios específicos](../access-control/ui/users.md).

Una vez añadidos los permisos de acceso necesarios, los usuarios de su organización pueden empezar a ver los paneles en la interfaz de usuario de Experience Platform y realizar otras acciones en función de los permisos asignados.
