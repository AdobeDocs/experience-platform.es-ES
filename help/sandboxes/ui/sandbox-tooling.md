---
title: Herramientas de zonas protegidas
description: Exporte e importe sin problemas configuraciones de espacio aislado entre espacios aislados.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: fea62a2aa3c7d175afbfa808f392c3a93a0d31a0
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 7%

---

# Herramientas de zona protegida

>[!NOTE]
>
>Las herramientas de espacio aislado son una capacidad fundamental que admite [!DNL Real-Time Customer Data Platform] y [!DNL Journey Optimizer] para mejorar la eficiencia del ciclo de desarrollo y la precisión de la configuración.<br><br>Debe tener los dos permisos de control de acceso basados en roles siguientes para usar la característica de herramientas de zona protegida: <br>- `manage-sandbox` o `view-sandbox`<br>- `manage-package`

Mejore la precisión de la configuración en todos los entornos limitados y exporte e importe sin problemas las configuraciones de los entornos limitados con la función de herramientas para entornos limitados. Utilice las herramientas de zona protegida para reducir el tiempo de respuesta al valor del proceso de implementación y mover las configuraciones correctas a través de las zonas protegidas.

Puede utilizar la función de herramientas de zona protegida para seleccionar diferentes objetos y exportarlos a un paquete. Un paquete puede constar de un único objeto o de varios objetos. <!--or an entire sandbox.-->Todos los objetos incluidos en un paquete deben pertenecer a la misma zona protegida.

## Objetos admitidos para las herramientas de zona protegida {#supported-objects}

La característica de herramientas de zona protegida permite exportar objetos [!DNL Adobe Real-Time Customer Data Platform] y [!DNL Adobe Journey Optimizer] a un paquete.

### Objetos Real-time Customer Data Platform {#real-time-cdp-objects}

En la tabla siguiente se enumeran [!DNL Adobe Real-Time Customer Data Platform] objetos que actualmente se admiten en las herramientas de zona protegida:

| Plataforma | Objeto | Detalles |
| --- | --- | --- |
| Plataforma de datos del cliente | Fuentes | Las credenciales de la cuenta de origen no se replican en la zona protegida de destino por motivos de seguridad y deberán actualizarse manualmente. El flujo de datos de origen se copia en estado de borrador de forma predeterminada. |
| Plataforma de datos del cliente | Públicos | Solo se admite el tipo de **[!UICONTROL servicio de segmentación]** de la **[!UICONTROL Audiencia del cliente]**. Las etiquetas existentes para consentimiento y control se copiarán en el mismo trabajo de importación. El sistema seleccionará automáticamente la política de combinación predeterminada en la zona protegida de destino con la misma clase XDM al comprobar las dependencias de la política de combinación. |
| Plataforma de datos del cliente | Identidades | El sistema deduplicará automáticamente las áreas de nombres de identidad estándar de Adobe al crear en la zona protegida de destino. Las audiencias solo se pueden copiar cuando todos los atributos de las reglas de audiencia están habilitados en el esquema de unión. Los esquemas necesarios deben moverse y habilitarse primero para el perfil unificado. |
| Plataforma de datos del cliente | Esquemas | Las etiquetas existentes para consentimiento y control se copiarán en el mismo trabajo de importación. El usuario tiene la flexibilidad de importar esquemas sin la opción de perfil unificado habilitada. Las mayúsculas y minúsculas perimetrales de las relaciones de esquema no se incluyen en el paquete. |
| Plataforma de datos del cliente | Conjuntos de datos | Los conjuntos de datos se copian con la configuración del perfil unificado deshabilitada de forma predeterminada. |
| Plataforma de datos del cliente | Políticas de consentimiento y gobernanza | Añada directivas personalizadas creadas por un usuario a un paquete y muévalas a zonas protegidas. |

Los objetos siguientes se importan, pero están en estado de borrador o desactivado:

| Función | Objeto | Estado |
| --- | --- | --- |
| Estado de importación | Flujo de datos de Source | Borrador |
| Estado de importación |  Recorrido  | Borrador |
| Perfil unificado | Conjunto de datos | Perfil unificado desactivado |
| Políticas | Políticas de gobernanza de datos | Desactivado |

### Objetos Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

La tabla siguiente enumera [!DNL Adobe Journey Optimizer] objetos que actualmente son compatibles con las herramientas y limitaciones de la zona protegida:

| Plataforma | Objeto | Detalles |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Público | Una audiencia se puede copiar como un objeto dependiente del objeto de recorrido. Puede seleccionar crear una audiencia nueva o reutilizar una existente en la zona protegida de destino. |
| [!DNL Adobe Journey Optimizer] | Esquema | Los esquemas utilizados en el recorrido se pueden copiar como objetos dependientes. Puede seleccionar crear un nuevo esquema o reutilizar uno existente en la zona protegida de destino. |
| [!DNL Adobe Journey Optimizer] | Política de combinación | Las políticas de combinación utilizadas en el recorrido se pueden copiar como objetos dependientes. En la zona protegida de Target, **no puede** crear una nueva política de combinación, solo puede utilizar una ya existente. |
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

Seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Examinar]**, que enumera los esquemas disponibles. A continuación, seleccione los puntos suspensivos (`...`) junto al esquema seleccionado y aparecerá un menú desplegable con los controles. Seleccione **[!UICONTROL Agregar al paquete]** en la lista desplegable.

![Lista de esquemas que muestra el menú desplegable que resalta el control [!UICONTROL Agregar al paquete].](../images/ui/sandbox-tooling/add-to-package.png)

En el cuadro de diálogo **[!UICONTROL Agregar al paquete]**, seleccione la opción **[!UICONTROL Crear nuevo paquete]**. Proporcione un [!UICONTROL Nombre] para el paquete y una [!UICONTROL Descripción] opcional y, a continuación, seleccione **[!UICONTROL Agregar]**.

![Cuadro de diálogo [!UICONTROL Agregar al paquete] con [!UICONTROL Crear nuevo paquete] seleccionado y resaltando [!UICONTROL Agregar].](../images/ui/sandbox-tooling/create-new-package.png)

Ha vuelto al entorno **[!UICONTROL Schemas]**. Ahora puede añadir objetos adicionales al paquete que ha creado siguiendo los pasos que se indican a continuación.

### Añadir un objeto a un paquete existente y publicarlo {#add-object-to-existing-package}

Para ver una lista de los esquemas disponibles, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Examinar]**. A continuación, seleccione los puntos suspensivos (`...`) junto al esquema seleccionado para ver las opciones de control en un menú desplegable. Seleccione **[!UICONTROL Agregar al paquete]** en la lista desplegable.

![Lista de esquemas que muestra el menú desplegable que resalta el control [!UICONTROL Agregar al paquete].](../images/ui/sandbox-tooling/add-to-package.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Agregar al paquete]**. Seleccione la opción **[!UICONTROL Paquete existente]**, luego seleccione la lista desplegable **[!UICONTROL Nombre del paquete]** y seleccione el paquete requerido. Finalmente, selecciona **[!UICONTROL Agregar]** para confirmar tus opciones.

Cuadro de diálogo ![[!UICONTROL Agregar al paquete], que muestra un paquete seleccionado del menú desplegable.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Se muestra la lista de objetos añadidos al paquete. Para publicar el paquete y hacer que esté disponible para su importación en entornos limitados, seleccione **[!UICONTROL Publish]**.

![Una lista de objetos en el paquete que resalta la opción [!UICONTROL Publish].](../images/ui/sandbox-tooling/publish-package.png)

Seleccione **[!UICONTROL Publish]** para confirmar la publicación del paquete.

![Cuadro de diálogo de confirmación de paquete de Publish, en el que se resalta la opción [!UICONTROL Publish].](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Una vez publicado, el contenido del paquete no se puede cambiar. Para evitar problemas de compatibilidad, asegúrese de que se han seleccionado todos los recursos necesarios. Si es necesario realizar cambios, debe crear un nuevo paquete.

Ha vuelto a la ficha **[!UICONTROL Paquetes]** del entorno [!UICONTROL Zonas protegidas], donde puede ver el nuevo paquete publicado.

![Lista de paquetes de espacio aislado que resalta el nuevo paquete publicado.](../images/ui/sandbox-tooling/published-packages.png)

## Importación de un paquete en una zona protegida de destino {#import-package-to-target-sandbox}

>[!NOTE]
>
>Todas las acciones de importación se registran en los registros de auditoría.

Para importar el paquete en una zona protegida de destino, vaya a la pestaña Zonas protegidas **[!UICONTROL Examinar]** y seleccione la opción más (+) junto al nombre de la zona protegida.

![La pestaña **[!UICONTROL Examinar]** de las zonas protegidas resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/browse-sandboxes.png)

En el menú desplegable, seleccione el **[!UICONTROL nombre del paquete]** que desee importar a la zona protegida de destino. Agregue un **[!UICONTROL nombre de trabajo]**, que se usará para la supervisión futura. De forma predeterminada, el perfil unificado se desactiva cuando se importan los esquemas del paquete. Cambie **Habilitar esquemas para el perfil** para habilitar esto y luego seleccione **[!UICONTROL Siguiente]**.

![La página de detalles de importación que muestra la selección desplegable [!UICONTROL Nombre del paquete]](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

La página [!UICONTROL Objeto de paquete y dependencias] proporciona una lista de todos los recursos incluidos en este paquete. El sistema detecta automáticamente los objetos dependientes necesarios para importar correctamente los objetos padre seleccionados. Los atributos que faltan se muestran en la parte superior de la página. Seleccione **[!UICONTROL Ver detalles]** para obtener un desglose más detallado.

![La página [!UICONTROL Objeto de paquete y dependencias] muestra los atributos que faltan.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Los objetos dependientes se pueden reemplazar por objetos existentes en la zona protegida de destino, lo que permite reutilizar objetos existentes en lugar de crear una nueva versión. Por ejemplo, al importar un paquete que incluye esquemas, puede reutilizar el grupo de campos personalizados existente y las áreas de nombres de identidad en la zona protegida de destino. Alternativamente, al importar un paquete que incluya Recorridos, puede reutilizar segmentos existentes en la zona protegida de Target.

Para utilizar un objeto existente, seleccione el icono de lápiz situado junto al objeto dependiente.

![La página [!UICONTROL Objeto de paquete y dependencias] muestra una lista de recursos incluidos en el paquete.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Se muestran las opciones para crear nuevos o utilizar los existentes. Seleccionar **[!UICONTROL Usar]** existente.

![La página [!UICONTROL Objeto de paquete y dependencias] que muestra las opciones de objeto dependiente [!UICONTROL Crear nuevo] y [!UICONTROL Usar existente].](../images/ui/sandbox-tooling/use-existing-object.png)

El diálogo **[!UICONTROL Grupo de campos]** muestra una lista de grupos de campos disponibles para el objeto. Seleccione los grupos de campos requeridos y luego seleccione **[!UICONTROL Guardar]**.

![Una lista de campos mostrados en el cuadro de diálogo [!UICONTROL Grupo de campos], que resalta la selección [!UICONTROL Guardar]. ](../images/ui/sandbox-tooling/field-group-list.png)

Ha vuelto a la página [!UICONTROL Objeto Package y dependencias]. Aquí, seleccione **[!UICONTROL Finalizar]** para completar la importación del paquete.

![La página [!UICONTROL Objeto de paquete y dependencias] muestra una lista de los recursos incluidos en el paquete, destacando [!UICONTROL Finalizar].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportar e importar una zona protegida completa

>[!NOTE]
>
>Actualmente, solo se admiten objetos de Real-time Customer Data Platform al exportar o importar una zona protegida completa. Los objetos de Adobe Journey Optimizer, como los recorridos, no son compatibles en este momento.

Puede exportar todos los tipos de objetos admitidos en un paquete de zona protegida completo y, a continuación, importar el paquete en varios entornos limitados para replicar las configuraciones de objetos. Por ejemplo, esta funcionalidad le permite:

- Vuelva a importar una zona protegida para reproducir todas las configuraciones del objeto si necesita restablecer la zona protegida
- Importe el paquete en otros entornos limitados y utilícelo como entorno limitado de modelo para acelerar el proceso de desarrollo.

### Exportar toda una zona protegida {#export-entire-sandbox}

Para exportar una zona protegida completa, ve a la pestaña [!UICONTROL Zonas protegidas] **[!UICONTROL Paquetes]** y selecciona **[!UICONTROL Crear paquete]**.

![La ficha [!UICONTROL Zonas protegidas] **[!UICONTROL Paquetes]** que resalta [!UICONTROL Crear paquete].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Seleccione **[!UICONTROL Zona protegida completa]** para el [!UICONTROL Tipo de paquete] en el cuadro de diálogo [!UICONTROL Crear paquete]. Proporcione un [!UICONTROL nombre de paquete] para su nuevo paquete y seleccione la **[!UICONTROL zona protegida]** en la lista desplegable. Finalmente, selecciona **[!UICONTROL Crear]** para confirmar tus entradas.

![El cuadro de diálogo [!UICONTROL Crear paquete] muestra los campos completados y resalta [!UICONTROL Crear].](../images/ui/sandbox-tooling/create-package-dialog.png)

El paquete se ha creado correctamente, seleccione **[!UICONTROL Publish]** para publicar el paquete.

![Lista de paquetes de espacio aislado que resalta el nuevo paquete publicado.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Ha vuelto a la ficha **[!UICONTROL Paquetes]** del entorno [!UICONTROL Zonas protegidas], donde puede ver el nuevo paquete publicado.

### Importar todo el paquete de zona protegida {#import-entire-sandbox-package}

>[!NOTE]
>
>Todos los objetos se importarán en la zona protegida de destino como objetos nuevos. Se recomienda importar un paquete de zona protegida completo en una zona protegida vacía.

Para importar el paquete en una zona protegida de destino, vaya a la pestaña [!UICONTROL Zonas protegidas] **[!UICONTROL Examinar]** y seleccione la opción más (+) junto al nombre de la zona protegida.

![La pestaña **[!UICONTROL Examinar]** de las zonas protegidas resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

En el menú desplegable, seleccione la zona protegida completa usando la lista desplegable **[!UICONTROL Nombre del paquete]**. Agregue un **[!UICONTROL nombre de trabajo]**, que se usará para la supervisión futura y una **[!UICONTROL descripción de trabajo]** opcional; a continuación, seleccione **[!UICONTROL Siguiente]**.

![La página de detalles de importación que muestra la selección desplegable [!UICONTROL Nombre del paquete]](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Debe tener permisos completos para todos los objetos incluidos en el paquete. Si no tiene permisos, la operación de importación fallará y aparecerán mensajes de error.

Se le dirigirá a la página [!UICONTROL Objeto del paquete y dependencias], donde podrá ver el número de objetos y dependencias que se importan y excluyen. Aquí, seleccione **[!UICONTROL Importar]** para completar la importación del paquete.

![La página [!UICONTROL Objeto de paquete y dependencias] muestra el mensaje en línea de los tipos de objeto no admitidos, destacando [!UICONTROL Importar].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Espere un poco para que se complete la importación. El tiempo para finalizar puede variar según el número de objetos del paquete. Puede supervisar el trabajo de importación desde la ficha [!UICONTROL Zonas protegidas] **[!UICONTROL Trabajos]**.

## Monitorización de detalles de importación {#view-import-details}

Para ver los detalles importados, vaya a la pestaña [!UICONTROL Zonas protegidas] **[!UICONTROL Trabajos]** y seleccione el paquete en la lista. También puede utilizar la barra de búsqueda para buscar el paquete.

![La pestaña [!UICONTROL Trabajos] de las zonas protegidas resalta la selección del paquete de importación.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Seleccione **[!UICONTROL Ver resumen de importación]** en el panel de detalles derecho de la ficha **[!UICONTROL Trabajos]** del entorno de zonas protegidas.

![La pestaña [!UICONTROL Importaciones] de las zonas protegidas resalta la selección [!UICONTROL Ver detalles de importación] en el panel derecho.](../images/ui/sandbox-tooling/view-import-details.png)

El cuadro de diálogo **[!UICONTROL Resumen de importación]** muestra un desglose de las importaciones con el progreso como porcentaje.

>[!NOTE]
>
>Puede ver una lista de objetos navegando a páginas de inventario específicas.

![El cuadro de diálogo [!UICONTROL Importar detalles] muestra un desglose detallado de las importaciones.](../images/ui/sandbox-tooling/import-details.png)

Cuando se completa la importación, se recibe una notificación en la interfaz de usuario de Platform. Puede acceder a estas notificaciones desde el icono de alertas. Puede navegar a la resolución de problemas desde aquí si un trabajo no se ha realizado correctamente.

## Tutorial de vídeo

El siguiente vídeo tiene como objetivo ayudarle a comprender las herramientas de la zona protegida, y describe cómo crear un nuevo paquete, publicarlo e importarlo.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Pasos siguientes

Este documento muestra cómo utilizar la función de herramientas de zona protegida en la interfaz de usuario de Experience Platform. Para obtener información sobre las zonas protegidas, consulte la [guía de usuario sobre zonas protegidas](../ui/user-guide.md).

Para ver los pasos de realización de distintas operaciones mediante la API de espacio aislado, consulte la [guía para desarrolladores de espacios aislados](../api/getting-started.md). Para obtener información general de alto nivel sobre las zonas protegidas en Experience Platform, consulte la [documentación general](../home.md).
