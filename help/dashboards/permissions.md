---
solution: Experience Platform
title: Cómo obtener y conceder permisos de acceso para paneles de Experience Platform
type: Documentation
description: Conceda a los usuarios la capacidad de ver, editar y actualizar paneles de Experience Platform mediante Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 6%

---

# Permisos de acceso para tableros

Para conceder a los usuarios la capacidad de ver, editar y actualizar paneles, primero debe habilitar los permisos. En Adobe Experience Platform, el control de acceso se proporciona mediante [Adobe Admin Console](https://adminconsole.adobe.com/). Los usuarios están vinculados con permisos y zonas protegidas mediante perfiles de producto en [!DNL Admin Console].

Este documento proporciona un resumen de los permisos disponibles para los paneles, incluidas las funciones a las que proporcionan acceso y las funciones de usuario que habilitan. Para obtener información detallada sobre cómo obtener y asignar permisos de acceso, comience por leer la [descripción general del control de acceso](../access-control/home.md).

## Requisitos previos

Para configurar el control de acceso de [!DNL Experience Platform], debe tener privilegios de administrador en una organización que tenga una integración de producto de [!DNL Experience Platform]. Consulte el artículo de Adobe Centro de Ayuda sobre [funciones](https://helpx.adobe.com/es/enterprise/using/admin-roles.html) administrativas para obtener más información.

## Permisos de panel disponibles {#available-permissions}

El servicio [!DNL Dashboards] proporciona tres permisos que, cuando se combinan, proporcionan acceso completo a los paneles de [!UICONTROL Perfiles], [!UICONTROL Segmentos], [!UICONTROL Destinos] y [!UICONTROL Uso de licencias] en Adobe Experience Platform. Estos permisos son:

| Permiso | Descripción |
|---|---|
| **Administrar tableros estándar** | Este permiso es un **permiso** global de lectura y escritura. Le permite [crear widgets](./customize/custom-widgets.md) personalizados y [editar el widget esquema](./customize/edit-schema.md) través del [!UICONTROL biblioteca de Widget]. |
| **Ver Tableros estándar** | Esto proporciona **funcionalidad de solo** lectura para los [!UICONTROL tableros Perfiles], Destinos y [!UICONTROL Segmentos y permite acceder a ellos a través del navegación izquierdo de Experience Platform. También agrega [!UICONTROL Dashboards] al navegación izquierdo y acceso a los inventario Dashboards] y a las integraciones pestaña. |
| **Ver Panel de uso de licencias** | Este permiso permite a los usuarios **acceso de solo lectura** a [el tablero de uso de licencias](./guides/license-usage.md) en la interfaz de usuario de Experience Platform. |

Hay cinco permisos no incluidos en la categoría [!DNL Dashboard] que son potencialmente necesarios según sus necesidades. En la tabla siguiente se describen las ubicaciones de las categorías en Admin Console:

>[!IMPORTANT]
>
>Tanto el **[!DNL Manage Standard Dashboards]** como los **[!DNL View Standard Dashboards]** permisos **requieren** un permiso &quot;vista&quot; o &quot;administrar&quot; del categoría o [!DNL Destinations] del Admin Console para activar las secciones relevantes dentro del [!DNL Profile Management] IU Experience Platform.

| Permiso | Admin Console ubicación categoría |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de control de acceso

La siguiente matriz de control de acceso proporciona un desglose de los permisos necesarios y qué función proporcionan con respecto al acceso a las diferentes funciones del panel. Los permisos se muestran en la fila horizontal superior y el espacio de trabajo de la interfaz de usuario de Experience Platform en la columna izquierda.

|   | [!UICONTROL Ver panel estándar] O [!UICONTROL Administrar panel estándar] | [!UICONTROL Ver perfiles],<br/>[!UICONTROL Ver segmentos],<br/> [!UICONTROL Ver destinos] | [!UICONTROL Administre consultas] y [!UICONTROL administre entornos aislados] | [!UICONTROL Ver Panel de uso de licencias] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] en el panel de navegación izquierdo. | N/A | **Se REQUIERE un permiso de &quot;Ver&quot; o &quot;Administrar&quot;** para cada tablero respectivo. | N/A | N/A |
| [!DNL Dashboards] en el navegación izquierdo. | HABILITADO | **Se requiere al menos uno.** | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/> (la ficha examinar) | HABILITADO | N/A | N/A | N/A |
| [!DNL Dashboards][!DNL Integrations] <br/>pestaña (usado para instalar Power BI) | HABILITADO | **Se requiere al menos uno** | N/A | N/A |
| Power BI Install botón &amp; flujo de trabajo | HABILITADO | N/A | **OBLIGATORIO** | N/A |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] paneles.<br/>Capacidad para editar esquemas de widgets y agregar nuevos atributos para la personalización de widgets | **Se requiere administrar tablero estándar** | **REQUERIDO (para cada tablero respectivo)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | HABILITADO |

{style="table-layout:auto"}

## Adición de permisos al perfil del producto

Utilice la información proporcionada anteriormente para agregar los permisos adecuados al perfil del producto. Consulte la documentación para obtener instrucciones completas sobre [cómo agregar permisos a través del IU control de acceso](../access-control/ui/permissions.md).

Para obtener descripciones de los permisos, consulte la [sección de permisos](#available-permissions) disponibles anteriormente en este documento.

>[!NOTE]
>
>No tiene que habilitar todos los permisos para todos los usuarios. Según la estructura de su organización, es posible que desee crear perfiles de producto independientes para determinados usuarios y conceder acceso limitado (como solo lectura). Consulte la documentación sobre la administración de usuarios para un perfil de producto para obtener información sobre [cómo asignar permisos a usuarios específicos](../access-control/ui/users.md).

Una vez añadidos los permisos de acceso necesarios, los usuarios de su organización pueden empezar a ver los paneles en la interfaz de usuario de Experience Platform y realizar otras acciones en función de los permisos asignados.
