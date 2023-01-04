---
title: Plantillas de informe de Power BI para tableros de plataforma
description: Utilice las plantillas de informe para explorar los datos de Experience Platform mediante el uso de Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Power BI de plantillas de informes para tableros

La función de plantilla de informe de Power BI le permite crear informes convincentes rellenados con datos de Adobe Experience Platform. El proceso de instalación optimizado instala automáticamente utilidades estándar para el perfil del cliente en tiempo real, la segmentación y los destinos. La instalación también conecta la Power BI con los modelos de datos para que pueda personalizar y ampliar fácilmente las plantillas de informes. Estos informes se pueden compartir en toda la organización sin que los destinatarios necesiten credenciales para la organización IMS en Platform.

Este documento proporciona instrucciones sobre cómo conectar Adobe Experience Platform con la aplicación de Power BI y cómo usar las plantillas de informe para compartir perspectivas de datos de Platform clave con usuarios externos.

## Primeros pasos

Antes de continuar con este tutorial, se recomienda tener una buena comprensión de [composición de esquema](../../xdm/schema/composition.md) en Experience Platform, y cómo se incluyen los atributos en el perfil del cliente en tiempo real a través del [esquema de unión](../../xdm/schema/composition.md#union).

Para instalar la integración de la aplicación de Power BI, los usuarios deben haber adquirido primero los siguientes permisos de Platform:

- Administrar consultas
- Administrar entornos limitados

Para obtener información sobre cómo asignar estos permisos, lea la [control de acceso](../../access-control/home.md) documentación.

También debe tener una cuenta de Power BI para seguir este tutorial. Para crear una cuenta, vaya a la [Página de inicio de Power BI](https://powerbi.microsoft.com/en-us/) y siga el proceso de registro. Los usuarios de esta cuenta de Power BI también deben habilitar la variable **Crear espacio de trabajo** en su configuración de Power BI. Esta configuración se encuentra dentro de la configuración de inquilino del portal de administración de Power BI. Si su inquilino o empleador proporciona su cuenta, póngase en contacto con su administrador respectivo para habilitar esta configuración.

![El portal de administración de Power BI crea la configuración del espacio de trabajo.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Para que la ficha Tableros aparezca en el panel de navegación izquierdo de la interfaz de usuario de Platform y que la vista Inventario de tableros esté visible, debe tener acceso a cualquiera de los tableros de perfil, segmentación o destino como parte de la licencia de Platform.

## Instalación de la integración de la aplicación de Power BI

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Tableros]** en el panel de navegación izquierdo para abrir [!UICONTROL Tableros] espacio de trabajo. La variable [!UICONTROL Examinar] muestra una lista de las vistas de tablero disponibles actualmente. Para obtener más información sobre la visualización de paneles disponibles, consulte la [documentación de inventario](../inventory.md).

A continuación, seleccione la **[!UICONTROL Integraciones]** pestaña . Aparece la página de integración de la aplicación de Power BI. Desde aquí, seleccione **[!UICONTROL Instalar]** para iniciar la instalación.

>[!NOTE]
>
>La variable [!UICONTROL Instalar] está desactivado a menos que tenga los permisos Administrar y Administrar entornos limitados del servicio de consultas.

![Pantalla de detalles de Power BI con el botón Instalar resaltado.](../images/power-bi/details-screen.png)

### Proporcionar credenciales

El primer paso en el proceso de instalación es proporcionar credenciales que no caduquen para la integración de la aplicación de Power BI. Hay dos opciones disponibles para proporcionar estas opciones: [[!UICONTROL Crear nuevas credenciales]](#create-new-credentials) o [[!UICONTROL Usar credenciales existentes]](#use-existing-credentials). Seleccione la opción adecuada para continuar.

#### Crear nuevas credenciales {#create-new-credentials}

Existen dos campos obligatorios al generar nuevas credenciales: [!UICONTROL Nombre] y [!UICONTROL Asignado a]. La variable [!UICONTROL Asignado a] está relacionado con la dirección de correo electrónico asociada a su cuenta de Power BI.

![Power BI generar nueva pantalla de credenciales.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>La creación de credenciales que no caduquen requiere que tenga asignados ciertos permisos y funciones. Los permisos necesarios son Administrar entornos limitados y Administrar integración del servicio de consulta. Las funciones necesarias son las funciones de administrador y desarrollador de Adobe Experience Platform. Para obtener información sobre cómo asignar estos permisos, lea la [control de acceso](../../access-control/home.md) documentación.

Para obtener más información sobre la generación de credenciales del servicio de consulta que no caducan, consulte la [guía de credenciales que no caducan](../../query-service/ui/credentials.md#non-expiring-credentials).

Después de generar credenciales que no caducan por primera vez, se descarga un archivo JSON en ese equipo. Este archivo JSON se puede compartir con otros usuarios como credenciales para completar el proceso de instalación.

#### Usar credenciales existentes {#use-existing-credentials}

También se puede cargar un archivo de credenciales JSON para pasar la validación. Estos archivos JSON que contienen valores de credenciales que no caducan se descargan en el equipo local que se utiliza cuando se crea una credencial que no caduca.

>[!IMPORTANT]
>
>Para utilizar una credencial existente que no caduque, al usuario ya se le debe haber asignado una credencial. Si el usuario no tiene una credencial asignada y no puede crear una nueva mediante Adobe Admin Console, no podrá continuar con el proceso de instalación.

Select **[!UICONTROL Cargar archivo de credenciales]** y, a continuación, seleccione el archivo JSON adecuado para cargarlo en el cuadro de diálogo que aparece.

![Pantalla de credenciales de Power BI con el botón Cargar archivo de credenciales resaltado.](../images/power-bi/upload-credential-file.png)

Después de proporcionar las credenciales que no caducan, Platform las valida automáticamente. Cuando la validación se haya realizado correctamente, aparece un mensaje de confirmación. Select **[!UICONTROL Siguiente]** para revisar el acuerdo de consentimiento para la solicitud de Power BI.

![Las credenciales que no caducan se validaron correctamente en la pantalla con el botón Siguiente resaltado.](../images/power-bi/successfully-uploaded-credential-file.png)

### Proporcionar consentimiento

Aparecerá la visualización del consentimiento. Select **[!UICONTROL Revisar consentimiento]** para abrir una nueva ventana que detalle los permisos necesarios para que Power BI acceda a sus datos y los utilice según sus condiciones de servicio y declaración de privacidad.

![La visualización de consentimiento proporcionado con el botón Revisar consentimiento resaltado.](../images/power-bi/provide-consent-display.png)

Select **[!UICONTROL Accept]** para conceder permiso de Power BI para acceder y utilizar sus datos de Platform.

![Solicitud de permisos para la aplicación de Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Si sale del proceso de instalación en cualquier momento antes de dar su consentimiento, la integración de la aplicación de Power BI no se instalará en el inventario de paneles.

Después de dar su consentimiento, la plantilla de informe se instala automáticamente en el entorno de Power BI como parte del proceso de instalación. A continuación, Power BI utiliza las credenciales que no caducan para acceder a Platform, ejecuta secuencialmente todas las consultas SQL y rellena la plantilla de informe con los datos devueltos.

Select **[!UICONTROL Finalizar]** para volver al inventario del tablero.

![La pantalla Proporcionar consentimiento con el botón Finalizar resaltado.](../images/power-bi/finish-consent-review.png)

Ahora que la plantilla de informe de Power BI está instalada, aparece en la lista de paneles disponibles en la sección [!UICONTROL Examinar] pestaña . Select **[!UICONTROL Power BI]** de la lista para navegar al entorno de Power BI.

![Power BI enumerado en el inventario de paneles.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Los administradores de Power BI deben asegurarse de que los usuarios tengan los permisos de acceso adecuados para ver estos tableros en el entorno de Power BI.

## espacio de trabajo de Power BI

Tras iniciar sesión [el espacio de trabajo de Power BI](https://dxt.powerbi.com), las plantillas de informe están disponibles para cada uno de los servicios a los que tiene acceso. Las plantillas de informe incluyen tableros de perfiles, segmentos y destinos **only** si tienen los permisos de vista correspondientes.

Los widgets estándar de perfiles, segmentos y destinos están disponibles en los informes de plantilla de Power BI de forma predeterminada.

>[!NOTE]
>
>Debe tener permisos de edición habilitados para un tablero determinado para permitir que ese tablero se instale en el entorno de Power BI.

![Informe de plantilla de perfil de Power BI con widgets de perfil de plataforma estándar.](../images/power-bi/profile-report-template.png)

Una vez instalado un tablero en Power BI, las plantillas de informe se muestran a todos los usuarios de forma predeterminada. Si desea restringir el acceso a cualquier plantilla de informe, asegúrese de deshabilitar el acceso de los usuarios en cuestión desde el entorno de Power BI.

## Personalización de la plantilla del informe de Power BI

Mediante el uso de utilidades personalizadas, puede agregar atributos personalizados al modelo de datos para enriquecer las plantillas de informe proporcionadas por Power BI.

>[!NOTE]
>
>Los atributos que se pueden usar para las utilidades personalizadas dependen de lo que esté disponible en el esquema de unión. Para obtener información sobre cómo ver y explorar esquemas de unión en beneficio de los widgets personalizados, consulte la [guía de la interfaz de usuario del esquema de unión](../../profile/ui/union-schema.md).

### Creación de un widget personalizado

Los widgets personalizados se crean mediante la biblioteca de utilidades. Consulte la [Información general de la biblioteca de utilidades](../customize/widget-library.md) para ver una introducción a la función y a la [tutorial para crear un widget personalizado](../customize/custom-widgets.md) para instrucciones específicas.

>[!IMPORTANT]
>
>Los widgets personalizados recién creados son **not** se sincroniza automáticamente entre los tableros de Adobe Experience Platform y las plantillas de informe de Power BI. Los widgets personalizados creados en la interfaz de usuario de Platform deben volver a crearse manualmente dentro del entorno de Power BI.

### Vuelva a crear la utilidad personalizada en el entorno de Power BI

Una vez que el tablero tenga las métricas y los atributos adecuados incluidos en los widgets personalizados, podrá modificar la plantilla de informe que se muestra desde el entorno de Power BI. Consulte la [documentación de Power BI](https://docs.microsoft.com/es-ES/power-bi/) para obtener información sobre cómo editar un informe a través de su interfaz de usuario.

## Eliminar la integración de la aplicación de Power BI

Para eliminar el tablero, vaya al inventario del tablero y seleccione el icono Eliminar (![](../images/power-bi/delete-icon.png)) junto al nombre del tablero.

>[!NOTE]
>
>Solo el usuario que instaló el tablero de Power BI puede eliminar la integración de la interfaz de usuario de Platform.

![La ficha Examinar de la pantalla de inventario de los paneles se muestra con el botón Examinar y el icono Eliminar resaltados.](../images/power-bi/delete-power-bi-dashboard.png)

Aparece una ventana emergente de confirmación. Select **[!UICONTROL Eliminar]** para confirmar el proceso.

>[!IMPORTANT]
>
>Al eliminar el tablero de Power BI de la interfaz de usuario de Platform, **not** elimine las plantillas de informe disponibles en su entorno de Power BI. Si desea eliminar por completo la información contenida en las plantillas de informe de Power BI, debe iniciar sesión en la cuenta de Power BI y eliminar las plantillas de informe de ese entorno. Una vez eliminado, un usuario puede volver a instalar el panel de Power BI siguiendo las mismas instrucciones de instalación que se describen arriba.

## Pasos siguientes

Al leer este documento, tendrá una mejor comprensión de cómo se pueden integrar las plantillas de informes de Power BI en Platform para compartir datos convincentes de sus paneles de perfiles, segmentos o destinos. Consulte la [información general sobre la personalización de tableros](../customize/overview.md) para obtener más información sobre la personalización de los tableros.
