---
solution: Experience Platform
title: Cómo obtener y conceder permisos de acceso para tableros de Experience Platform
type: Documentation
description: Conceder a los usuarios la capacidad de ver, editar y actualizar tableros de Experience Platform mediante Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f138bb0f1b8d289cc872afc065d31c5e55d4b05c
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 7%

---

# Permisos de acceso para tableros

Para que los usuarios puedan ver, editar y actualizar los tableros, primero debe habilitar los permisos. En Adobe Experience Platform, el control de acceso se proporciona a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com/). Los usuarios están vinculados con permisos y entornos limitados a través de perfiles de producto en la variable [!DNL Admin Console].

Este documento proporciona un resumen de los permisos disponibles para los tableros, incluidas las funciones a las que proporcionan acceso y las funciones de usuario que habilitan. Para obtener información detallada sobre cómo obtener y asignar permisos de acceso, lea la [información general sobre el control de acceso](../access-control/home.md).

## Requisitos previos

Para configurar el control de acceso para [!DNL Experience Platform], debe tener privilegios de administrador para una organización que tenga una [!DNL Experience Platform] integración de productos. Consulte el artículo de Adobe Help Center sobre [funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obtener más información.

## Permisos de tablero disponibles {#available-permissions}

La variable [!DNL Dashboards] proporciona tres permisos que, cuando se combinan, proporcionan acceso completo al [!UICONTROL Perfiles], [!UICONTROL Segmentos], [!UICONTROL Destinos]y [!UICONTROL Uso de licencias] tableros dentro de Adobe Experience Platform. Estos permisos son:

| Permiso | Descripción |
|---|---|
| **Administrar tableros estándar** | Este permiso es un **permiso global de lectura y escritura**. Le permite [crear widgets personalizados](./customize/custom-widgets.md) y [editar el esquema del widget](./customize/edit-schema.md) a través de [!UICONTROL Biblioteca de utilidades]. |
| **Ver tableros estándar** | Esto proporciona **solo lectura** para la función [!UICONTROL Perfiles], [!UICONTROL Destinos]y [!UICONTROL Segmentos] tableros y permite acceder a ellos a través de la navegación izquierda de Platform. También agrega [!UICONTROL Tableros] a la navegación izquierda y acceso al [!UICONTROL Tableros] ficha inventario e integraciones . |
| **Ver panel de uso de licencias** | Este permiso permite a los usuarios **solo lectura** acceso a [el panel de uso de licencias](./guides/license-usage.md) en la interfaz de usuario del Experience Platform. |

Hay cinco permisos que no se incluyen en la variable [!DNL Dashboard] que pueden ser necesarias según sus necesidades. La siguiente tabla describe sus ubicaciones de categorías en el Admin Console:

>[!IMPORTANT]
>
>Ambas **[!DNL Manage Standard Dashboards]** y **[!DNL View Standard Dashboards]** permissions **requerir** un permiso &quot;ver&quot; o &quot;administrar&quot; de la variable [!DNL Profile Management] o [!DNL Destinations] en el Admin Console para activar las secciones relevantes dentro de la interfaz de usuario de Platform.

| Permiso | Ubicación de categoría del Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de control de acceso

La siguiente matriz de control de acceso proporciona un desglose de qué permisos se requieren y qué función proporcionan con respecto al acceso a las diferentes funciones del tablero. Los permisos se enumeran en la fila horizontal superior y el espacio de trabajo de la interfaz de usuario de Platform se muestra en la columna izquierda.

|  | [!UICONTROL Ver tablero estándar] O [!UICONTROL Administrar tablero estándar] | [!UICONTROL Ver perfiles],<br/>[!UICONTROL Ver segmentos],<br/> [!UICONTROL Ver destinos] | [!UICONTROL Administrar consultas] &amp; [!UICONTROL Administrar entornos limitados] | [!UICONTROL Ver panel de uso de licencias] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] en el panel de navegación izquierdo. | N/A | **Se REQUIERE un permiso &quot;Ver&quot; o &quot;Administrar&quot;** para cada tablero respectivo. | N/D | N/D |
| [!DNL Dashboards] en el panel de navegación izquierdo. | HABILITADO | **Al menos una**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(la pestaña examinar ) | HABILITADO | N/D | N/D | N/D |
| [!DNL Dashboards] [!DNL Integrations] ficha <br/>(utilizado para instalar Power BI) | HABILITADO | **Al menos una** | N/D | N/D |
| Botón de instalación de Power BI y flujo de trabajo | HABILITADO | N/D | **REQUERIDO** | N/D |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] tableros.<br/>La capacidad de editar esquemas de utilidades y agregar nuevos atributos para la personalización de utilidades | **Se requiere la administración de tableros estándar** | **REQUERIDO (para cada tablero respectivo)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | HABILITADO |

{style=&quot;table-layout:auto&quot;}

## Añadir permisos al perfil del producto

Utilice la información proporcionada anteriormente para añadir los permisos adecuados a su perfil de producto. Consulte la documentación para obtener instrucciones completas sobre [cómo añadir permisos a través de la interfaz de usuario de control de acceso](../access-control/ui/permissions.md).

Para obtener descripciones de los permisos, consulte la [permisos disponibles](#available-permissions) en este documento.

>[!NOTE]
>
>No es necesario habilitar todos los permisos para todos los usuarios. Según la estructura de su organización, puede que desee crear perfiles de producto independientes para determinados usuarios y conceder acceso limitado (como solo lectura). Consulte la documentación sobre la administración de usuarios para obtener un perfil de producto para obtener más información [cómo asignar permisos para usuarios específicos](../access-control/ui/users.md).

Una vez que haya añadido los permisos de acceso necesarios, los usuarios de su organización pueden empezar a ver los tableros en la interfaz de usuario del Experience Platform y a realizar otras acciones en función de los permisos que haya asignado.
