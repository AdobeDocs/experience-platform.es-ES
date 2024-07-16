---
solution: Experience Platform
title: Información general sobre la concienciación en materia de datos en los manuales de casos de uso
description: Aprenda a acelerar el tiempo de respuesta al valor copiando los recursos generados en la zona protegida inspiradora final en otras zonas protegidas.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Recursos generados por el manual de Publish a otras zonas protegidas {#publish-to-other-sandboxes}

Los libros de reproducción de casos de uso son plantillas de marketing diseñadas para generar recursos como audiencias, esquemas o recorridos para casos de uso de marketing comunes. Puede probar los recursos creados por los libros de reproducción en la zona protegida inspiradora y, cuando esté listo, puede importar los recursos en otras zonas protegidas de desarrollo para realizar más pruebas con los datos que tiene disponibles en esas zonas protegidas. Cuando esté satisfecho con las pruebas, puede mover los recursos de los entornos limitados de desarrollo a los de producción.

Sin embargo, en algunos casos, es posible que ya haya configurado sus propios esquemas, campos y grupos de campos en otros entornos limitados de desarrollo. Esto podría hacer que algunos de los recursos generados por las plantillas de casos de uso, como los recorridos, sean incompatibles con los datos. Para comprender cómo utilizar la funcionalidad de reconocimiento de datos para alinear y complementar mejor los recursos generados con los recursos existentes, lea este tutorial.

## Requisitos previos {#prerequisites}

Antes de leer este tutorial, examine las [plantillas disponibles del manual de casos de uso](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) y [cree una instancia](/help/use-case-playbooks/playbooks/create-share-reuse.md) de un manual de uso preferido.

La creación de una instancia de genera un conjunto de recursos, como recorridos, segmentos, esquemas y mensajes, en la zona protegida inspiracional. Siga leyendo para aprender a copiar estos recursos en otros entornos limitados.

### Creación y publicación de un paquete {#create-publish-package}

>[!NOTE]
>
> Solo puede importar paquetes en otros entornos limitados de desarrollo. Una vez que haya realizado todos los cambios o actualizaciones necesarios, podrá importar los recursos o paquetes de esos entornos limitados de desarrollo a producción. No puede importar directamente desde las zonas protegidas de los libros de reproducción de casos de uso a la producción.

1. Para importar objetos de una zona protegida inspiradora a otra, busca la instancia que desees de un manual de casos de uso y selecciona **[!UICONTROL Publish a una zona protegida diferente]** para exportar los artefactos como paquete.

   ![GIF que muestra las diferentes instancias de caso de uso](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Una vez que seleccione el botón **[!UICONTROL Publish a una zona protegida diferente]**, aparecerá un modal. Rellene el nombre y la descripción opcional y seleccione **[!UICONTROL Crear]**. Este paso agrupa los recursos generados en un paquete que se puede importar en una zona protegida diferente.

   ![Un modal para crear un paquete](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Vaya a la página **Zonas protegidas** en el panel de navegación izquierdo y seleccione la pestaña **Paquetes**, busque su paquete y publíquelo. Para publicar un paquete en estado de borrador, siga los pasos del documento [herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish).

   ![Paquete en estado de borrador o sin publicar](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publicando el paquete](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Una vez publicada correctamente, en la página de exploración de paquetes debería ver un botón **+** habilitado junto al nombre.

   ![Paquetes en la página Zonas protegidas](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > El paquete no se puede importar mientras esté en modo de borrador, por lo que debe abrir la página de detalles del paquete y publicarlo.

5. Seleccione el control **+** e inicie el flujo de trabajo para importar los recursos generados por el manual de casos de uso en la **[!UICONTROL zona protegida de Target]**. Seleccione una zona protegida de destino y confirme el nombre del paquete que desea importar mediante la lista desplegable. Añada los detalles del trabajo, como el nombre y la descripción del trabajo, antes de continuar con el siguiente paso.

   ![Iniciar flujo de trabajo de importación, seleccionar destino, confirmar paquete, agregar detalles del trabajo.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. En el paso **[!UICONTROL Ver dependencias]**, puede asignar esquemas y copiar otros recursos de la zona protegida de inspiración en la de destino. El botón **[!UICONTROL Finalizar]** está deshabilitado hasta que asigne cada esquema.

   ![Asignar esquemas en el paso &#39;Ver dependencias&#39;, habilitando el botón Finalizar.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Asignación de esquemas {#map-schemas}

1. Asigne el primer esquema. El cuadro de diálogo de asignación de esquemas muestra una lista desplegable para seleccionar el esquema de destino. Si el esquema de origen es un esquema de perfil, no hay otras opciones de esquema de destino aparte del [esquema de perfil de unión individual](/help/xdm/classes/individual-profile.md). Puede ver las recomendaciones de asignación generadas automáticamente entre los campos Datos de Source y Destino cuando se muestra la página por primera vez. Puede editar las asignaciones seleccionando el campo de destino y, a continuación, un nuevo campo. Si modifica las asignaciones sugeridas, use el botón **Validar** para validar las nuevas asignaciones y mostrar los errores que puedan estar vinculados a las nuevas asignaciones. Seleccione **Guardar** una vez que se haya completado la asignación.

   ![Cuadro de diálogo de asignación de esquemas con un menú desplegable para seleccionar un esquema de destino.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Continúe asignando todos los campos de los esquemas. Si el esquema es un [esquema de evento](/help/xdm/classes/experienceevent.md), el cuadro de diálogo muestra un menú desplegable donde puede ver todos los esquemas de evento de la zona protegida de destino.

   ![Seleccionar un esquema de destino del menú desplegable](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Seleccione un esquema de los esquemas disponibles en la **zona protegida de destino**.

   ![Seleccionar un esquema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Complete la asignación y seleccione **Guardar**.

   ![Guardar asignación](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Una vez que haya completado la asignación de todos los campos de los esquemas, seleccione **Finalizar** para completar el flujo de trabajo de importación.

   ![Finalizar el flujo](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > No puede modificar ningún recurso excepto para los esquemas, ya que es una zona protegida inspiradora, pero se muestran como dependencias del paquete.

### Estado de importación {#import-status}

1. Se le redirigirá automáticamente a la página [**Importaciones**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details), donde podrá ver el progreso de la importación.

   ![Página que muestra el progreso de la importación](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Mientras se importa el paquete, los recursos del paquete se crean en la zona protegida de destino. Una vez finalizados, hacen referencia a los campos asignados durante el proceso de importación. El proceso se ha completado y los recursos de la zona protegida inspiracional ahora también están presentes en la zona protegida de Target para que los pruebe.

   ![Recursos generados en la zona protegida de destino](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Pasos siguientes

Después de leer esta guía, ahora comprende mejor cómo aprovechar los libros de reproducción de casos de uso junto con [herramientas de espacio aislado](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) para crear recorridos ejecutables que hagan referencia a sus esquemas. Obtenga más información sobre los [casos de uso comunes de Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
