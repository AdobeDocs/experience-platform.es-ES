---
solution: Experience Platform
title: Cómo obtener y conceder permisos de acceso para paneles de Experience Platform
type: Documentation
description: Conceda a los usuarios la capacidad de ver, editar y actualizar paneles de Experience Platform mediante Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 6%

---

# Permisos de acceso para paneles

Para conceder a los usuarios la capacidad de ver, editar y actualizar paneles, primero debe habilitar los permisos. En Adobe Experience Platform, el control de acceso se proporciona mediante [Adobe Admin Console](https://adminconsole.adobe.com/). Los usuarios están vinculados con permisos y zonas protegidas mediante perfiles de producto en [!DNL Admin Console].

Este documento proporciona un resumen de los permisos disponibles para los paneles, incluidas las funciones a las que proporcionan acceso y las funciones de usuario que habilitan. Para obtener información detallada sobre cómo obtener y asignar permisos de acceso, comience por leer la [descripción general del control de acceso](../access-control/home.md).

## Requisitos previos

Para configurar el control de acceso de [!DNL Experience Platform], debe tener privilegios de administrador en una organización que tenga una integración de producto de [!DNL Experience Platform]. Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

## Permisos de tablero disponibles {#available-permissions}

El servicio [!DNL Dashboards] proporciona tres permisos que, cuando se combinan, proporcionan acceso completo a los paneles de [!UICONTROL Perfiles], [!UICONTROL Segmentos], [!UICONTROL Destinos] y [!UICONTROL Uso de licencias] en Adobe Experience Platform. Estos permisos son:

| Permiso | Descripción |
|---|---|
| **Administrar paneles estándar** | Este permiso es de **lectura y escritura global**. Le permite [crear widgets personalizados](./customize/custom-widgets.md) y [editar el esquema del widget](./customize/edit-schema.md) a través de la [!UICONTROL biblioteca de widgets]. |
| **Ver paneles estándar** | Esto proporciona la funcionalidad de **solo lectura** para los paneles de [!UICONTROL Perfiles], [!UICONTROL Destinos] y [!UICONTROL Segmentos], y permite el acceso a ellos a través de la navegación izquierda de Platform. También agrega [!UICONTROL Paneles] a la navegación izquierda y el acceso al inventario de [!UICONTROL Paneles] y a la pestaña de integraciones. |
| **Ver tablero de uso de licencias** | Este permiso permite a los usuarios **acceso de solo lectura** a [el tablero de uso de licencias](./guides/license-usage.md) en la interfaz de usuario del Experience Platform. |

Hay cinco permisos no incluidos en la categoría [!DNL Dashboard] que son potencialmente necesarios según sus necesidades. En la tabla siguiente se describen las ubicaciones de las categorías en el Admin Console:

>[!IMPORTANT]
>
>Los permisos **de **[!DNL Manage Standard Dashboards]**y **[!DNL View Standard Dashboards]**requieren** un permiso de &quot;vista&quot; o &quot;administración&quot; de la categoría [!DNL Profile Management] o [!DNL Destinations] del Admin Console para activar las secciones relevantes en la interfaz de usuario de Platform.

| Permiso | ubicación de categoría de Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de control de acceso

La siguiente matriz de control de acceso proporciona un desglose de los permisos necesarios y qué función proporcionan con respecto al acceso a las diferentes funciones del panel. Los permisos se muestran en la fila horizontal superior y el espacio de trabajo de la IU de Platform a lo largo de la columna izquierda.

|   | [!UICONTROL Ver panel estándar] O [!UICONTROL Administrar panel estándar] | [!UICONTROL Ver perfiles],<br/>[!UICONTROL Ver segmentos],<br/> [!UICONTROL Ver destinos] | [!UICONTROL Administrar consultas] y [!UICONTROL Administrar zonas protegidas] | [!UICONTROL Ver tablero de uso de licencias] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] en el panel de navegación izquierdo. | N/A | **Se REQUIERE un permiso de &quot;Ver&quot; o &quot;Administrar&quot;** para cada tablero respectivo. | N/A | N/A |
| [!DNL Dashboards] en el panel de navegación izquierdo. | HABILITADO | **Se requiere al menos un**. | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/> (la ficha examinar) | HABILITADO | N/A | N/A | N/A |
| [!DNL Dashboards] [!DNL Integrations] ficha <br/> (utilizada para instalar Power BI) | HABILITADO | **Se requiere al menos uno** | N/A | N/A |
| Botón Instalar y flujo de trabajo de Power BI | HABILITADO | N/A | **REQUERIDO** | N/A |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] paneles.<br/>Capacidad para editar esquemas de widgets y agregar nuevos atributos para la personalización de widgets | **Se requiere administrar tablero estándar** | **REQUERIDO (para cada tablero respectivo)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | HABILITADO |

{style="table-layout:auto"}

## Adición de permisos al perfil del producto

Utilice la información proporcionada anteriormente para agregar los permisos adecuados al perfil del producto. Consulte la documentación para obtener instrucciones completas sobre [cómo agregar permisos a través de la IU de control de acceso](../access-control/ui/permissions.md).

Para obtener descripciones de los permisos, consulte la sección [permisos disponibles](#available-permissions) anterior en este documento.

>[!NOTE]
>
>No tiene que habilitar todos los permisos para todos los usuarios. Según la estructura de su organización, es posible que desee crear perfiles de producto independientes para determinados usuarios y conceder acceso limitado (como solo lectura). Consulte la documentación sobre la administración de usuarios para un perfil de producto para obtener información sobre [cómo asignar permisos a usuarios específicos](../access-control/ui/users.md).

Una vez añadidos los permisos de acceso necesarios, los usuarios de su organización pueden empezar a ver los paneles en la interfaz de usuario de Experience Platform y realizar otras acciones en función de los permisos asignados.
