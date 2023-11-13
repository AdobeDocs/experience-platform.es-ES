---
title: Plantillas de informe de Power BI para paneles de Platform
description: Utilice plantillas de informe para explorar los datos del Experience Platform mediante Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 729d218f72a8caecc90a98810b973d0754f7757b
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Power BI de plantillas de informes para paneles

La función de Power BI de informes permite crear informes atractivos rellenados con datos de Adobe Experience Platform. El proceso de instalación simplificado instala automáticamente los widgets estándar para el perfil del cliente en tiempo real, la segmentación y los destinos. La instalación también conecta Power BI con los modelos de datos para que pueda personalizar y ampliar fácilmente las plantillas de informes. Estos informes se pueden compartir en toda la organización sin que los destinatarios necesiten credenciales para su organización en Platform.

Este documento proporciona instrucciones sobre cómo conectar Adobe Experience Platform con la aplicación de Power BI y utilizar plantillas de informes para compartir perspectivas de datos clave de Platform con usuarios externos.

## Introducción

Antes de continuar con este tutorial, se recomienda comprender bien [composición de esquemas](../../xdm/schema/composition.md) en Experience Platform y cómo se incluyen los atributos en el Perfil del cliente en tiempo real a través de [esquema de unión](../../xdm/schema/composition.md#union).

Para instalar la integración de aplicaciones de Power BI, los usuarios deben haber adquirido primero los siguientes permisos de Platform:

- Administrar consultas
- Administrar zonas protegidas

Para obtener información sobre cómo asignar estos permisos, lea la [control de acceso](../../access-control/home.md) documentación.

También debe tener una cuenta de Power BI para seguir este tutorial. Para crear una cuenta de, vaya a [Power BI homepage](https://powerbi.microsoft.com/en-us/) y siga el proceso de registro. Los usuarios de esta cuenta de Power BI también deben habilitar la variable **Crear espacio de trabajo** configuración dentro de su configuración de Power BI. Esta configuración se encuentra en la configuración de inquilino del portal de administración de Power BI. Si su inquilino o empleador proporciona su cuenta, póngase en contacto con su administrador respectivo para habilitar esta configuración.

![Power BI Portal de administración: crear configuración de Workspace.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Para que la pestaña Paneles aparezca en la navegación izquierda de la interfaz de usuario de Platform y la vista Inventario de paneles sea visible, debe tener acceso a cualquiera de los paneles de Perfil, Segmentación o Destino como parte de la licencia de Platform.

## Instalación de la integración de la aplicación Power BI

En la IU de Platform, seleccione **[!UICONTROL Paneles]** en la navegación izquierda para abrir [!UICONTROL Paneles] workspace. El [!UICONTROL Examinar] La pestaña muestra una lista de las vistas de panel disponibles actualmente. Para obtener más información sobre cómo ver los paneles disponibles, consulte la [documentación de inventario](../inventory.md).

A continuación, seleccione la **[!UICONTROL Integraciones]** pestaña. Aparecerá la página Power BI de la aplicación. Desde aquí, seleccione **[!UICONTROL Instalar]** para iniciar la instalación.

>[!NOTE]
>
>El [!UICONTROL Instalar] está desactivado a menos que tenga los permisos de Administrar servicio de consulta y Administrar zonas protegidas.

![Pantalla de detalles del Power BI con el botón Instalar resaltado.](../images/power-bi/details-screen.png)

### Proporcionar credenciales

El primer paso del proceso de instalación es proporcionar credenciales que no caduquen para la integración de la aplicación de Power BI. Hay dos opciones disponibles para proporcionar estos elementos: [[!UICONTROL Crear credenciales nuevas]](#create-new-credentials) o [[!UICONTROL Usar credenciales existentes]](#use-existing-credentials). Seleccione el conmutador adecuado para continuar.

#### Crear credenciales nuevas {#create-new-credentials}

Existen dos campos obligatorios al generar nuevas credenciales: [!UICONTROL Nombre] y [!UICONTROL Asignado a]. El [!UICONTROL Asignado a] Este campo está relacionado con la dirección de correo electrónico asociada a la cuenta de Power BI.

![Pantalla de creación de nuevas credenciales de Power BI.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>La creación de credenciales que no caducan requiere que tenga asignados determinados permisos y funciones. Los permisos necesarios son Administrar zonas protegidas y Administrar integración del servicio de consultas. Las funciones requeridas son de administrador de Adobe Experience Platform y de desarrollador. Para obtener información sobre cómo asignar estos permisos, lea la [control de acceso](../../access-control/home.md) documentación.

Para obtener más información sobre la generación de credenciales de servicio de consulta que no caducan, consulte la [guía de credenciales que no caducan](../../query-service/ui/credentials.md#non-expiring-credentials).

Después de generar credenciales que no caducan por primera vez, se descarga un archivo JSON en ese equipo. Este archivo JSON se puede compartir con otros usuarios como credenciales para completar el proceso de instalación.

#### Usar credenciales existentes {#use-existing-credentials}

También se puede cargar un archivo de credenciales JSON para aprobar la validación. Estos archivos JSON que contienen los valores de credencial que no caducan se descargan en el equipo local que se utiliza cuando se crea una credencial que no caduca.

>[!IMPORTANT]
>
>Para utilizar una credencial existente que no caduque, el usuario ya debe tener asignada una credencial. Si el usuario no tiene una credencial asignada y no puede crear una nueva mediante Adobe Admin Console, no podrá continuar con el proceso de instalación.

Seleccionar **[!UICONTROL Cargar archivo de credenciales]**, luego seleccione el archivo JSON apropiado para cargar en el cuadro de diálogo que aparece.

![Pantalla de credenciales de Power BI con el botón Cargar archivo de credenciales resaltado.](../images/power-bi/upload-credential-file.png)

Después de proporcionar las credenciales que no caducan, Platform las valida automáticamente. Cuando la validación se realiza correctamente, aparece un mensaje de confirmación. Seleccionar **[!UICONTROL Siguiente]** para revisar el acuerdo de consentimiento de la aplicación de Power BI.

![Las credenciales que no caducan validaron correctamente la pantalla con el botón Siguiente resaltado.](../images/power-bi/successfully-uploaded-credential-file.png)

### Dar su consentimiento

Aparecerá la pantalla de consentimiento. Seleccionar **[!UICONTROL Revisar consentimiento]** para abrir una nueva ventana que detalle los permisos necesarios para que Power BI acceda y utilice sus datos según sus condiciones de servicio y declaración de privacidad.

![Se muestra la pantalla de consentimiento de proveedor con el botón Revisar consentimiento resaltado.](../images/power-bi/provide-consent-display.png)

Seleccionar **[!UICONTROL Aceptar]** para conceder permiso a la Power BI para acceder y utilizar los datos de Platform.

![Solicitud de permisos para la aplicación de Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Si sale del proceso de instalación en cualquier momento antes de dar su consentimiento, la integración de la aplicación de Power BI no se instalará en el inventario de paneles.

Después de dar su consentimiento, la plantilla de informe se instala automáticamente en el entorno de Power BI como parte del proceso de instalación. Power BI a continuación, utiliza las credenciales que no caducan para acceder a Platform, ejecutar secuencialmente todas las consultas SQL y rellenar la plantilla de informe con los datos devueltos.

Seleccionar **[!UICONTROL Finalizar]** para volver al inventario de tableros.

![Se muestra el consentimiento del proveedor con el botón Finalizar resaltado.](../images/power-bi/finish-consent-review.png)

Ahora que la plantilla de informe de Power BI está instalada, aparece en la lista de paneles disponibles en la [!UICONTROL Examinar] pestaña. Seleccionar **[!UICONTROL Power BI]** en la lista para desplazarse al entorno de Power BI.

![Power BI enumerados en el inventario de paneles.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Los administradores de Power BI deben asegurarse de que los usuarios tengan los permisos de acceso adecuados para ver estos paneles en el entorno de Power BI.

## Power BI Workspace

Después de iniciar sesión en [el espacio de trabajo de Power BI](https://dxt.powerbi.com), las plantillas de informes están disponibles para cada uno de los servicios a los que tiene acceso. Las plantillas de informe incluyen perfiles, segmentos y paneles de destinos **solamente** si tienen los permisos de vista correspondientes.

Los widgets estándar de perfiles, segmentos y destinos están disponibles en los informes de plantilla de Power BI de forma predeterminada.

>[!NOTE]
>
>Debe tener habilitados los permisos de edición de un tablero determinado para permitir que ese tablero se instale en el entorno de Power BI.

![Informe de plantilla de perfil de Power BI con widgets de perfil de plataforma estándar.](../images/power-bi/profile-report-template.png)

Una vez instalado un tablero en Power BI, las plantillas de informe se muestran a todos los usuarios de forma predeterminada. Si desea restringir el acceso a cualquier plantilla de informe, asegúrese de deshabilitar el acceso para los usuarios en cuestión desde el entorno de Power BI.

## Personalización de la plantilla de informe de Power BI

Mediante el uso de widgets personalizados, puede agregar atributos personalizados al modelo de datos para enriquecer las plantillas de informe que proporciona Power BI.

>[!NOTE]
>
>Los atributos que puede utilizar para los widgets personalizados dependen de lo que esté disponible en el esquema de unión. Para obtener información sobre cómo ver y explorar esquemas de unión en beneficio de los widgets personalizados, consulte la [guía de IU del esquema de unión](../../profile/ui/union-schema.md).

### Crear un widget personalizado

Los widgets personalizados se crean mediante la biblioteca de widgets. Consulte la [Resumen de biblioteca de widgets](../customize/widget-library.md) para obtener una introducción a la función y la [tutorial para crear un widget personalizado](../customize/custom-widgets.md) para obtener instrucciones específicas.

>[!IMPORTANT]
>
>Los widgets personalizados recién creados son **no** se sincroniza automáticamente entre los paneles de Adobe Experience Platform y las plantillas de informe de Power BI. Los widgets personalizados creados en la interfaz de usuario de Platform deben volver a crearse manualmente dentro del entorno de Power BI.

### Vuelva a crear el widget personalizado en el entorno de Power BI.

Una vez que el tablero tenga las métricas y los atributos adecuados incluidos en los widgets personalizados, podrá modificar la plantilla de informe que se muestra en el entorno de Power BI. Consulte la [documentación de Power BI](https://docs.microsoft.com/es-ES/power-bi/) para obtener información sobre cómo editar un informe a través de su interfaz de usuario.

## Eliminación de la integración de la aplicación Power BI

Para eliminar el tablero, vaya al inventario del tablero y seleccione el icono Eliminar (![](../images/power-bi/delete-icon.png)) junto al nombre del tablero.

>[!NOTE]
>
>Solo el usuario que instaló el panel de Power BI puede eliminar la integración de la interfaz de usuario de Platform.

![Pantalla de inventario de paneles: la pestaña de exploración se muestra con el botón Examinar y el icono de eliminación resaltado.](../images/power-bi/delete-power-bi-dashboard.png)

Aparece una ventana emergente de confirmación. Seleccionar **[!UICONTROL Eliminar]** para confirmar el proceso.

>[!IMPORTANT]
>
>Al eliminar el tablero de Power BI de la IU de Platform, se hace **no** elimine las plantillas de informe disponibles en su entorno de Power BI. Si desea eliminar por completo la información contenida en las plantillas de informes de Power BI, debe iniciar sesión en su cuenta de Power BI y eliminar las plantillas de informes de ese entorno. Una vez eliminado, un usuario puede volver a instalar el panel de Power BI siguiendo las mismas instrucciones de instalación descritas anteriormente.

## Pasos siguientes

Power BI Al leer este documento, tiene una mejor comprensión de cómo se pueden integrar las plantillas de informes en Platform para compartir perspectivas de datos atractivas de sus perfiles, segmentos o paneles de destinos. Consulte la [información general sobre personalización de tableros](../customize/overview.md) para obtener más información sobre cómo personalizar los paneles.
