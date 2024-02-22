---
title: Herramientas de zonas protegidas
description: Exporte e importe sin problemas configuraciones de espacio aislado entre espacios aislados.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 888608bdf3ccdfc56edd41c164640e258a4c5dd7
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 8%

---

# Herramientas de zona protegida

>[!NOTE]
>
>Las herramientas de espacio aislado son una capacidad fundamental que admite [!DNL Real-Time Customer Data Platform] y [!DNL Journey Optimizer] para mejorar la eficiencia del ciclo de desarrollo y la precisión de la configuración.<br><br>Debe tener los dos permisos de control de acceso basados en funciones siguientes para utilizar la función de herramientas de zona protegida:<br>- `manage-sandbox` o `view-sandbox`<br>- `manage-package`

Mejore la precisión de la configuración en todos los entornos limitados y exporte e importe sin problemas las configuraciones de los entornos limitados con la función de herramientas para entornos limitados. Utilice las herramientas de zona protegida para reducir el tiempo de respuesta al valor del proceso de implementación y mover las configuraciones correctas a través de las zonas protegidas.

Puede utilizar la función de herramientas de zona protegida para seleccionar diferentes objetos y exportarlos a un paquete. Un paquete puede constar de un único objeto o de varios objetos. <!--or an entire sandbox.-->Los objetos incluidos en un paquete deben pertenecer a la misma zona protegida.

## Objetos admitidos para las herramientas de zona protegida {#supported-objects}

La función de herramientas de zona protegida permite exportar [!DNL Adobe Real-Time Customer Data Platform] y [!DNL Adobe Journey Optimizer] en un paquete.

### Objetos Real-time Customer Data Platform {#real-time-cdp-objects}

La tabla siguiente enumera [!DNL Adobe Real-Time Customer Data Platform] objetos que son compatibles actualmente con las herramientas de zona protegida:

| Plataforma | Objeto | Detalles |
| --- | --- | --- |
| Plataforma de datos del cliente | Fuentes | Las credenciales de la cuenta de origen no se replican en la zona protegida de destino por motivos de seguridad y deberán actualizarse manualmente. El flujo de datos de origen se copia en estado de borrador de forma predeterminada. |
| Plataforma de datos del cliente | Públicos | Solo el **[!UICONTROL Audiencia del cliente]** type **[!UICONTROL Servicio de segmentación]** es compatible. Las etiquetas existentes para consentimiento y control se copiarán en el mismo trabajo de importación. El sistema seleccionará automáticamente la política de combinación predeterminada en la zona protegida de destino con la misma clase XDM al comprobar las dependencias de la política de combinación. |
| Plataforma de datos del cliente | Identidades | El sistema deduplicará automáticamente las áreas de nombres de identidad estándar de Adobe al crear en la zona protegida de destino. Las audiencias solo se pueden copiar cuando todos los atributos de las reglas de audiencia están habilitados en el esquema de unión. Los esquemas necesarios deben moverse y habilitarse primero para el perfil unificado. |
| Plataforma de datos del cliente | Esquemas | Las etiquetas existentes para consentimiento y control se copiarán en el mismo trabajo de importación. El usuario tiene la flexibilidad de importar esquemas sin la opción de perfil unificado habilitada. Las mayúsculas y minúsculas perimetrales de las relaciones de esquema no se incluyen en el paquete. |
| Plataforma de datos del cliente | Conjuntos de datos | Los conjuntos de datos se copian con la configuración del perfil unificado deshabilitada de forma predeterminada. |
| Plataforma de datos del cliente | Políticas de consentimiento y gobernanza | Añada directivas personalizadas creadas por un usuario a un paquete y muévalas a zonas protegidas. |

Los objetos siguientes se importan, pero están en estado de borrador o desactivado:

| Función | Objeto | Estado |
| --- | --- | --- |
| Estado de importación | Flujo de datos de origen | Borrador |
| Estado de importación |  Recorrido  | Borrador |
| Perfil unificado | Conjunto de datos | Perfil unificado desactivado |
| Políticas | Políticas de gobernanza de datos | Desactivado |

### Objetos Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

La tabla siguiente enumera [!DNL Adobe Journey Optimizer] objetos que actualmente son compatibles con las herramientas y limitaciones de la zona protegida:

| Plataforma | Objeto | Detalles |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Público | Una audiencia se puede copiar como un objeto dependiente del objeto de recorrido. Puede seleccionar crear una audiencia nueva o reutilizar una existente en la zona protegida de destino. |
| [!DNL Adobe Journey Optimizer] | Esquema | Los esquemas utilizados en el recorrido se pueden copiar como objetos dependientes. Puede seleccionar crear un nuevo esquema o reutilizar uno existente en la zona protegida de destino. |
| [!DNL Adobe Journey Optimizer] | Política de combinación | Las políticas de combinación utilizadas en el recorrido se pueden copiar como objetos dependientes. En la zona protegida de Target, puede hacer lo siguiente **no puede** Para crear una nueva política de combinación, solo puede utilizar una ya existente. |
| [!DNL Adobe Journey Optimizer] | Recorrido - detalles del lienzo | La representación del recorrido en el lienzo incluye los objetos del recorrido, como condiciones, acciones, eventos, audiencias de lectura, etc., que se copian. La actividad de salto se excluye de la copia. |
| [!DNL Adobe Journey Optimizer] | Evento | Se copian los eventos y los detalles del evento utilizados en el recorrido. Siempre se crea una nueva versión en la zona protegida de destino. |
| [!DNL Adobe Journey Optimizer] | Acción | Los mensajes push y de correo electrónico utilizados en el recorrido se pueden copiar como objetos dependientes. No se comprueba la integridad de las actividades de acción de canal utilizadas en los campos de recorrido que se utilizan para la personalización en el mensaje. Los bloques de contenido no se copian.<br><br>Se puede copiar la acción de actualización de perfil utilizada en el recorrido. Las acciones personalizadas y los detalles de acción utilizados en el recorrido también se copian. Siempre se crea una nueva versión en la zona protegida de destino. |

Las superficies (por ejemplo, los ajustes preestablecidos) no se copian. El sistema selecciona automáticamente la coincidencia más cercana posible en la zona protegida de destino en función del tipo de mensaje y el nombre de la superficie. Si no se encuentran superficies en la zona protegida de destino, la copia de superficie fallará, lo que provocará que la copia del mensaje falle porque un mensaje requiere que haya una superficie disponible para la configuración. En este caso, es necesario crear al menos una superficie para el canal derecho del mensaje para que funcione la copia.

Los tipos de identidad personalizados no se admiten como objetos dependientes al exportar un recorrido.

## Exportación de objetos a un paquete {#export-objects}

>[!NOTE]
>
>Todas las acciones de exportación se registran en los registros de auditoría.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Quitar un objeto"
>abstract="Para quitar un objeto del paquete, seleccione la fila que desea eliminar y, a continuación, utilice la opción Eliminar, que está disponible tras la selección. Tenga en cuenta que no puede quitar objetos de los paquetes publicados."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Configuración de caducidad del paquete"
>abstract="Los paquetes están configurados para que caduquen después de un período de inactividad en estado de borrador. La fecha predeterminada está fijada para 90 días a partir de hoy. Esta fecha seguirá cambiando hasta que se haya publicado el paquete. Si visita el paquete en estado de borrador, la fecha se mueve a un día más (a menos que la establezca manualmente)."

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

>[!NOTE]
>
>Todas las acciones de importación se registran en los registros de auditoría.

Para importar el paquete en una zona protegida de Target, vaya a las zonas protegidas **[!UICONTROL Examinar]** y seleccione la opción más (+) junto al nombre de la zona protegida.

![Las zonas protegidas **[!UICONTROL Examinar]** pestaña que resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/browse-sandboxes.png)

En el menú desplegable, seleccione la **[!UICONTROL Nombre del paquete]** desea importar a la zona protegida de destino. Añada un opcional **[!UICONTROL Nombre de trabajo]**, que se utilizará para futuras monitorizaciones. De forma predeterminada, el perfil unificado se desactiva cuando se importan los esquemas del paquete. Alternar **Habilitar esquemas para el perfil** para habilitar esto, seleccione **[!UICONTROL Siguiente]**.

![La página de detalles de importación que muestra [!UICONTROL Nombre del paquete] selección desplegable](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

El [!UICONTROL Objeto de paquete y dependencias] proporciona una lista de todos los recursos incluidos en este paquete. El sistema detecta automáticamente los objetos dependientes necesarios para importar correctamente los objetos padre seleccionados. Los atributos que faltan se muestran en la parte superior de la página. Seleccionar **[!UICONTROL Ver detalles]** para obtener un desglose más detallado.

![El [!UICONTROL Objeto de paquete y dependencias] La página muestra los atributos que faltan.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Los objetos dependientes se pueden reemplazar por objetos existentes en la zona protegida de destino, lo que permite reutilizar objetos existentes en lugar de crear una nueva versión. Por ejemplo, al importar un paquete que incluye esquemas, puede reutilizar el grupo de campos personalizados existente y las áreas de nombres de identidad en la zona protegida de destino. Alternativamente, al importar un paquete que incluya Recorridos, puede reutilizar segmentos existentes en la zona protegida de Target.

Para utilizar un objeto existente, seleccione el icono de lápiz situado junto al objeto dependiente.

![El [!UICONTROL Objeto de paquete y dependencias] Esta página muestra una lista de los recursos incluidos en el paquete.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Se muestran las opciones para crear nuevos o utilizar los existentes. Seleccionar **[!UICONTROL Usar los existentes]**.

![El [!UICONTROL Objeto de paquete y dependencias] página que muestra las opciones de objeto dependientes [!UICONTROL Crear nuevo] y [!UICONTROL Usar los existentes].](../images/ui/sandbox-tooling/use-existing-object.png)

El **[!UICONTROL Grupo de campos]** El cuadro de diálogo muestra una lista de grupos de campos disponibles para el objeto. Seleccione los grupos de campos necesarios y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Una lista de campos que se muestran en la [!UICONTROL Grupo de campos] diálogo, resaltando el [!UICONTROL Guardar] selección. ](../images/ui/sandbox-tooling/field-group-list.png)

Se le devolverá a la [!UICONTROL Objeto de paquete y dependencias] página. Desde aquí, seleccione **[!UICONTROL Finalizar]** para completar la importación del paquete.

![El [!UICONTROL Objeto de paquete y dependencias] Esta página muestra una lista de los recursos incluidos en el paquete, resaltando [!UICONTROL Finalizar].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

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

## Tutorial de vídeo

El siguiente vídeo tiene como objetivo ayudarle a comprender las herramientas de la zona protegida, y describe cómo crear un nuevo paquete, publicarlo e importarlo.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Pasos siguientes

Este documento muestra cómo utilizar la función de herramientas de zona protegida en la interfaz de usuario de Experience Platform. Para obtener información sobre los entornos limitados, consulte [guía del usuario de sandbox](../ui/user-guide.md).

Para ver los pasos sobre cómo realizar diferentes operaciones con la API de zona protegida, consulte la [guía para desarrolladores de sandbox](../api/getting-started.md). Para obtener una descripción general de alto nivel de los entornos limitados de Experience Platform, consulte la [documentación general](../home.md).
