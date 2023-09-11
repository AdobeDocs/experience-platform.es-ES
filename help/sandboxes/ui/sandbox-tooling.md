---
title: Herramientas de zonas protegidas
description: Exporte e importe sin problemas configuraciones de espacio aislado entre espacios aislados.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 8%

---


# [!BADGE Beta] Herramientas de espacio aislado

>[!IMPORTANT]
>
>El **Herramientas de espacio aislado** La función que se describe a continuación solo está disponible para clientes beta seleccionados.

>[!NOTE]
>
>Las herramientas de espacio aislado son una capacidad fundamental que admite [!DNL Real-Time Customer Data Platform] y [!DNL Journey Optimizer] para mejorar la eficiencia del ciclo de desarrollo y la precisión de la configuración.<br><br>Debe tener los dos permisos de control de acceso basados en funciones siguientes para utilizar la función de herramientas de zona protegida:<br>- `manage-sandbox` o `view-sandbox`<br>- `manage-package`

Mejore la precisión de la configuración en todos los entornos limitados y exporte e importe sin problemas las configuraciones de los entornos limitados con la función de herramientas para entornos limitados. Utilice las herramientas de zona protegida para reducir el tiempo de respuesta al valor del proceso de implementación y mover las configuraciones correctas a través de las zonas protegidas.

Puede utilizar la función de herramientas de zona protegida para seleccionar diferentes objetos y exportarlos a un paquete. Un paquete puede constar de un solo objeto, varios objetos o una zona protegida completa. Los objetos incluidos en un paquete deben pertenecer a la misma zona protegida.

## Objetos admitidos para las herramientas de zona protegida {#supported-objects}

En la tabla siguiente se enumeran los objetos actualmente compatibles con las herramientas de zona protegida:

| Plataforma | Objeto |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Recorridos |
| Plataforma de datos del cliente | Fuentes |
| Plataforma de datos del cliente | Segmentos |
| Plataforma de datos del cliente | Identidades |
| Plataforma de datos del cliente | Políticas |
| Plataforma de datos del cliente | Esquemas |
| Plataforma de datos del cliente | Conjuntos de datos |

Los objetos siguientes se importan, pero están en estado de borrador o desactivado:

| Función | Objeto | Estado |
| --- | --- | --- |
| Estado de importación | Flujo de datos de origen | Borrador |
| Estado de importación |  Recorrido  | Borrador |
| Perfil unificado | Esquema | Desactivado |
| Perfil unificado | Conjunto de datos | Desactivado |
| Políticas | Políticas de consentimiento | Desactivado |
| Políticas | Políticas de gobernanza de datos | Desactivado |

Los casos extremos que se enumeran a continuación no están incluidos en el paquete:

* Relaciones de esquemas

## Exportación de objetos a un paquete {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Guardar y salir del paquete"
>abstract="Los usuarios solo puede utilizar la opción Atrás para guardar y salir del paquete."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Quitar un objeto"
>abstract="El usuario debe seleccionar la fila y, a continuación, utilizar la opción Eliminar (disponible tras la selección) para quitar la fila."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Configuración de caducidad del paquete"
>abstract="La fecha está fijada para 90 días a partir de hoy. Esta fecha seguirá cambiando hasta que se haya publicado el paquete. Si un usuario visita mañana el paquete en estado de borrador, la fecha se mueve a un día más (a menos que la establezca el usuario)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Estado del paquete"
>abstract="El estado se establece como borrador de manera predeterminada. El estado cambia a publicado una vez que se haya publicado el paquete. No se pueden realizar cambios después de publicar el paquete."

>[!NOTE]
>
>Solo puede importar un paquete si tiene permiso para acceder a los objetos.

Este ejemplo documenta el proceso de exportación de un esquema y su adición a un paquete. Puede utilizar el mismo proceso para exportar otros objetos, por ejemplo, conjuntos de datos, recorridos y mucho más.

### Agregar un objeto a un nuevo paquete {#add-object-to-new-package}

Seleccionar **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Examinar]** , que enumera los esquemas disponibles. A continuación, seleccione los puntos suspensivos (`...`) junto al esquema seleccionado, y una lista desplegable muestra los controles. Seleccionar **[!UICONTROL Añadir a paquete]** en el menú desplegable.

![Lista de esquemas que muestran el menú desplegable resaltando la variable [!UICONTROL Añadir a paquete] control.](../images/ui/sandbox-tooling/add-to-package.png)

Desde el **[!UICONTROL Añadir a paquete]** , seleccione la **[!UICONTROL Crear nuevo paquete]** opción. Proporcione un [!UICONTROL Nombre] para su paquete y un [!UICONTROL Descripción], luego seleccione **[!UICONTROL Añadir]**.

![El [!UICONTROL Añadir a paquete] diálogo con [!UICONTROL Crear nuevo paquete] seleccionado y resaltado [!UICONTROL Añadir].](../images/ui/sandbox-tooling/create-new-package.png)

Se le devolverá a la **[!UICONTROL Esquemas]** entorno. Ahora puede añadir objetos adicionales al paquete que ha creado siguiendo los pasos que se indican a continuación.

### Añadir un objeto a un paquete existente y publicarlo {#add-object-to-existing-package}

Para ver una lista de los esquemas disponibles, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Examinar]** pestaña. A continuación, seleccione los puntos suspensivos (`...`) junto al esquema seleccionado para ver las opciones de control en un menú desplegable. Seleccionar **[!UICONTROL Añadir a paquete]** en el menú desplegable.

![Lista de esquemas que muestran el menú desplegable resaltando la variable [!UICONTROL Añadir a paquete] control.](../images/ui/sandbox-tooling/add-to-package.png)

El **[!UICONTROL Añadir a paquete]** aparece el cuadro de diálogo. Seleccione el **[!UICONTROL Paquete existente]** , luego seleccione la opción **[!UICONTROL Nombre del paquete]** y seleccione el paquete requerido. Finalmente, seleccione **[!UICONTROL Añadir]** para confirmar sus opciones.

![[!UICONTROL Añadir a paquete] , mostrando un paquete seleccionado de la lista desplegable.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Se muestra la lista de objetos añadidos al paquete. Para publicar el paquete y hacer que esté disponible para su importación en entornos limitados, seleccione **[!UICONTROL Publish]**.

![Una lista de objetos del paquete, que resalta el [!UICONTROL Publish] opción.](../images/ui/sandbox-tooling/publish-package.png)

Seleccionar **[!UICONTROL Publish]** para confirmar la publicación del paquete.

![Cuadro de diálogo de confirmación de paquete de publicación, destacando el [!UICONTROL Publish] opción.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Una vez publicado, el contenido del paquete no se puede cambiar. Para evitar problemas de compatibilidad, asegúrese de que se han seleccionado todos los recursos necesarios. Si es necesario realizar cambios, debe crear un nuevo paquete.

Se le devolverá a la **[!UICONTROL Paquetes]** en la pestaña [!UICONTROL Zonas protegidas] entorno, donde puede ver el nuevo paquete publicado.

![Lista de paquetes de zona protegida que resaltan el nuevo paquete publicado.](../images/ui/sandbox-tooling/published-packages.png)

## Importación de un paquete en una zona protegida de destino {#import-package-to-target-sandbox}

Para importar el paquete en una zona protegida de Target, vaya a las zonas protegidas **[!UICONTROL Examinar]** y seleccione la opción más (+) junto al nombre de la zona protegida.

![Las zonas protegidas **[!UICONTROL Examinar]** pestaña que resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/browse-sandboxes.png)

En el menú desplegable, seleccione la **[!UICONTROL Nombre del paquete]** desea importar a la zona protegida de destino. Añada un opcional **[!UICONTROL Nombre de trabajo]**, que se utilizará para una monitorización futura, y seleccione **[!UICONTROL Siguiente]**.

![La página de detalles de importación que muestra [!UICONTROL Nombre del paquete] selección desplegable](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

El [!UICONTROL Objeto de paquete y dependencias] proporciona una lista de todos los recursos incluidos en este paquete. El sistema detecta automáticamente los objetos dependientes necesarios para importar correctamente los objetos padre seleccionados.

![El [!UICONTROL Objeto de paquete y dependencias] Esta página muestra una lista de los recursos incluidos en el paquete.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Los objetos dependientes se pueden reemplazar por objetos existentes en la zona protegida de destino, lo que permite reutilizar objetos existentes en lugar de crear una nueva versión. Por ejemplo, al importar un paquete que incluye esquemas, puede reutilizar el grupo de campos personalizados existente y las áreas de nombres de identidad en la zona protegida de destino. Alternativamente, al importar un paquete que incluya Recorridos, puede reutilizar segmentos existentes en la zona protegida de Target.

Para utilizar un objeto existente, seleccione el icono de lápiz situado junto al objeto dependiente. Se muestran las opciones para crear nuevos o utilizar los existentes. Seleccionar **[!UICONTROL Usar los existentes]**.

![El [!UICONTROL Objeto de paquete y dependencias] página que muestra las opciones de objeto dependientes [!UICONTROL Crear nuevo] y [!UICONTROL Usar los existentes].](../images/ui/sandbox-tooling/use-existing-object.png)

El **[!UICONTROL Grupo de campos]** El cuadro de diálogo muestra una lista de grupos de campos disponibles para el objeto. Seleccione los grupos de campos necesarios y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Una lista de campos que se muestran en la [!UICONTROL Grupo de campos] diálogo, resaltando el [!UICONTROL Guardar] selección. ](../images/ui/sandbox-tooling/field-group-list.png)

Se le devolverá a la [!UICONTROL Objeto de paquete y dependencias] página. Desde aquí, seleccione **[!UICONTROL Finalizar]** para completar la importación del paquete.

![El [!UICONTROL Objeto de paquete y dependencias] Esta página muestra una lista de los recursos incluidos en el paquete, resaltando [!UICONTROL Finalizar].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportar e importar una zona protegida completa

### Exportar toda una zona protegida {#export-entire-sandbox}

Para exportar una zona protegida completa, vaya a [!UICONTROL Zonas protegidas] **[!UICONTROL Paquetes]** y seleccione **[!UICONTROL Crear paquete]**.

![El [!UICONTROL Zonas protegidas] **[!UICONTROL Paquetes]** resaltado de tabulaciones [!UICONTROL Crear paquete].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Seleccionar **[!UICONTROL Toda la zona protegida]** para el Tipo de paquete en el [!UICONTROL Crear paquete] diálogo. Proporcione un [!UICONTROL Nombre del paquete] para el paquete y seleccione la **[!UICONTROL Sandbox]** en el menú desplegable. Finalmente, seleccione **[!UICONTROL Crear]** para confirmar las entradas.

![El [!UICONTROL Crear paquete] diálogo que muestra los campos completados y el resaltado [!UICONTROL Crear].](../images/ui/sandbox-tooling/create-package-dialog.png)

El paquete se ha creado correctamente, seleccione **[!UICONTROL Publish]** para publicar el paquete.

![Lista de paquetes de zona protegida que resaltan el nuevo paquete publicado.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Se le devolverá a la **[!UICONTROL Paquetes]** en la pestaña [!UICONTROL Zonas protegidas] entorno, donde puede ver el nuevo paquete publicado.

### Importar todo el paquete de zona protegida {#import-entire-sandbox-package}

Para importar el paquete en una zona protegida de Target, vaya a [!UICONTROL Zonas protegidas] **[!UICONTROL Examinar]** y seleccione la opción más (+) junto al nombre de la zona protegida.

![Las zonas protegidas **[!UICONTROL Examinar]** pestaña que resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

En el menú desplegable, seleccione la zona protegida completa con la variable **[!UICONTROL Nombre del paquete]** desplegable. Añada un opcional **[!UICONTROL Nombre de trabajo]**, que se utilizará para una monitorización futura, y seleccione **[!UICONTROL Siguiente]**.

![La página de detalles de importación que muestra [!UICONTROL Nombre del paquete] selección desplegable](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Todos los objetos se crean como nuevos desde el paquete al importar una zona protegida completa. Los objetos no aparecen en la lista [!UICONTROL Objeto de paquete y dependencias] , ya que puede haber varios. Se muestra un mensaje en línea que informa de los tipos de objeto no compatibles.

Se le redirige a la [!UICONTROL Objeto de paquete y dependencias] página en la que puede ver el número de objetos y dependencias que se importan y excluyen. Desde aquí, seleccione **[!UICONTROL Importar]** para completar la importación del paquete.

![El [!UICONTROL Objeto de paquete y dependencias] página muestra el mensaje en línea de los tipos de objeto no admitidos, resaltando [!UICONTROL Importar].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## Supervisión de trabajos de importación y visualización de detalles de objetos de importación

Para ver los objetos importados y los detalles importados, vaya a [!UICONTROL Zonas protegidas] **[!UICONTROL Importaciones]** y seleccione el paquete en la lista. También puede utilizar la barra de búsqueda para buscar el paquete.

![Las zonas protegidas [!UICONTROL Importaciones] La pestaña resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/imports-tab.png)

### Ver objetos importados {#view-imported-objects}

En el **[!UICONTROL Importaciones]** en la pestaña [!UICONTROL Zonas protegidas] entorno, seleccione **[!UICONTROL Ver objetos importados]** en el panel de detalles derecho.

Seleccionar **[!UICONTROL Ver objetos importados]** en el panel de detalles derecho de la **[!UICONTROL Importaciones]** en la pestaña [!UICONTROL Zonas protegidas] entorno.

![Las zonas protegidas [!UICONTROL Importaciones] La pestaña resalta el [!UICONTROL Ver objetos importados] selección en el panel derecho.](../images/ui/sandbox-tooling/view-imported-objects.png)

Utilice las flechas para expandir los objetos y ver la lista completa de campos que se han importado al paquete.

![Las zonas protegidas [!UICONTROL Objetos importados] mostrar una lista de objetos importados en el paquete.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Ver detalles de importación {#view-import-details}

Seleccionar **[!UICONTROL Ver detalles de importación]** en el panel de detalles derecho del **[!UICONTROL Importaciones]** en el entorno Zonas protegidas.

![Las zonas protegidas [!UICONTROL Importaciones] La pestaña resalta el [!UICONTROL Ver detalles de importación] selección en el panel derecho.](../images/ui/sandbox-tooling/view-import-details.png)

El **[!UICONTROL Importar detalles]** El cuadro de diálogo muestra un desglose detallado de las importaciones.

![El [!UICONTROL Importar detalles] que muestra un desglose detallado de las importaciones.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Cuando se complete una importación, recibirá notificaciones en la interfaz de usuario de Platform. Puede acceder a estas notificaciones desde el icono de alertas. Puede navegar a la resolución de problemas desde aquí si un trabajo no se ha realizado correctamente.

## Pasos siguientes

Este documento muestra cómo utilizar la función de herramientas de zona protegida en la interfaz de usuario de Experience Platform. Para obtener información sobre los entornos limitados, consulte [guía del usuario de sandbox](../ui/user-guide.md).

Para ver los pasos sobre cómo realizar diferentes operaciones con la API de zona protegida, consulte la [guía para desarrolladores de sandbox](../api/getting-started.md). Para obtener una descripción general de alto nivel de los entornos limitados de Experience Platform, consulte la [documentación general](../home.md).
