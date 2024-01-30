---
solution: Experience Platform
title: Información general sobre la concienciación en materia de datos en los manuales de casos de uso
description: Aprenda a acelerar el tiempo de respuesta al valor copiando los recursos generados en la zona protegida inspiradora final en otras zonas protegidas.
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Información general sobre la concienciación en materia de datos en los manuales de casos de uso

Los libros de reproducción de casos de uso son plantillas de marketing diseñadas para generar recursos como audiencias, esquemas o recorridos para casos de uso de marketing comunes. Puede probar los recursos creados por los libros de reproducción en la zona protegida inspiradora y, cuando esté listo, puede importar los recursos en otras zonas protegidas de desarrollo para realizar más pruebas con los datos que tiene disponibles en esas zonas protegidas. Cuando esté satisfecho con las pruebas, puede mover los recursos de los entornos limitados de desarrollo a los de producción.

Sin embargo, en algunos casos, es posible que ya haya configurado sus propios esquemas, campos y grupos de campos en otros entornos limitados de desarrollo. Esto podría hacer que algunos de los recursos generados por las plantillas de casos de uso, como los recorridos, sean incompatibles con los datos. Para comprender cómo utilizar la funcionalidad de reconocimiento de datos para alinear y complementar mejor los recursos generados con los recursos existentes, lea este tutorial.

## Requisitos previos {#prerequisites}

Antes de leer este tutorial, examine la [plantillas de manual de casos de uso disponibles](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) y [creación de una instancia](/help/use-case-playbooks/playbooks/create-share-reuse.md) de un manual de estrategias preferido.

La creación de una instancia de genera un conjunto de recursos, como recorridos, segmentos, esquemas y mensajes, en la zona protegida inspiracional. Siga leyendo para aprender a copiar estos recursos en otros entornos limitados.

### Creación y publicación de un paquete {#create-publish-package}

>[!NOTE]
>
> Solo puede importar paquetes en otros entornos limitados de desarrollo. Una vez que haya realizado todos los cambios o actualizaciones necesarios, podrá importar los recursos o paquetes de esos entornos limitados de desarrollo a producción. No puede importar directamente desde las zonas protegidas de los libros de reproducción de casos de uso a la producción.

1. Para importar objetos de la zona protegida inspiracional a otra zona protegida, busque la instancia que desee en un manual de casos de uso y seleccione **[!UICONTROL Publicar en una zona protegida diferente]** para exportar los artefactos como un paquete.

   ![GIF que muestra las diferentes instancias de caso de uso](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Una vez seleccionada la variable **[!UICONTROL Publicar en una zona protegida diferente]** botón, aparece un modal. Rellene el nombre y la descripción opcional y seleccione **[!UICONTROL Crear]**. Este paso agrupa los recursos generados en un paquete que se puede importar en una zona protegida diferente.

   ![Un modal para crear un paquete](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Vaya a **Zonas protegidas** página en la barra de navegación del lado izquierdo y seleccione la **Paquetes** , busque el paquete y publíquelo. Para publicar un paquete que esté en estado de borrador, siga los pasos de la sección [herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) documento.

   ![Paquete en estado de borrador o sin publicar](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publicación del paquete](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Una vez publicada correctamente, en la página de exploración de paquetes debería ver un **+** botón habilitado junto al nombre.

   ![Paquetes en la página Zonas protegidas](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > El paquete no se puede importar mientras esté en modo de borrador, por lo que debe abrir la página de detalles del paquete y publicarlo.

5. Seleccione el **+** controle e inicie el flujo de trabajo para importar los recursos generados por el manual de casos de uso en **[!UICONTROL Zona protegida de Target]**. Seleccione una zona protegida de destino y confirme el nombre del paquete que desea importar mediante la lista desplegable. Añada los detalles del trabajo, como el nombre y la descripción del trabajo, antes de continuar con el siguiente paso.

   ![Inicie el flujo de trabajo de importación, seleccione un destino, confirme el paquete y añada detalles del trabajo.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. En el **[!UICONTROL Ver dependencias]** paso a paso, puede asignar esquemas y copiar otros recursos de la zona protegida de inspiración en la de destino. El **[!UICONTROL Finalizar]** El botón está desactivado hasta que asigne cada esquema.

   ![Asigne esquemas en el paso &quot;Ver dependencias&quot;, habilitando el botón Finalizar.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Asignación de esquemas {#map-schemas}

1. Asigne el primer esquema. El cuadro de diálogo de asignación de esquemas muestra una lista desplegable para seleccionar el esquema de destino. Si el esquema de origen es un esquema de perfil, no hay otras opciones de esquema de destino aparte de la variable [esquema de perfil de unión individual](/help/xdm/classes/individual-profile.md). Puede ver las recomendaciones de asignación generadas automáticamente entre los datos de origen y los campos de destino cuando se muestra la página por primera vez. Puede editar las asignaciones seleccionando el campo de destino y, a continuación, un nuevo campo. Si modifica las asignaciones sugeridas, utilice el **Validate** para validar las nuevas asignaciones y mostrar cualquier error que pueda estar vinculado a las nuevas asignaciones. Seleccionar **Guardar** una vez finalizada la asignación.

   ![Cuadro de diálogo Asignación de esquemas con un menú desplegable para seleccionar un esquema de destino.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Continúe asignando todos los campos de los esquemas. Si el esquema es un [esquema de eventos](/help/xdm/classes/experienceevent.md), el cuadro de diálogo muestra una lista desplegable en la que puede ver todos los esquemas de evento de la zona protegida de destino.

   ![Seleccione un esquema de destino de la lista desplegable](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Seleccione un esquema de los esquemas disponibles en la **Zona protegida de Target**.

   ![Seleccionar un esquema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Complete la asignación y seleccione **Guardar**.

   ![Guardar asignación](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Una vez que haya terminado de asignar todos los campos de los esquemas, seleccione **Finalizar** para completar el flujo de trabajo de importación.

   ![Finalizar el flujo](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > No puede modificar ningún recurso excepto para los esquemas, ya que es una zona protegida inspiradora, pero se muestran como dependencias del paquete.

### Estado de importación {#import-status}

1. Se le redirigirá automáticamente a [**Importaciones**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) página donde puede ver el progreso de la importación.

   ![Página que muestra el progreso de importación](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Mientras se importa el paquete, los recursos del paquete se crean en la zona protegida de destino. Una vez finalizados, hacen referencia a los campos asignados durante el proceso de importación. El proceso se ha completado y los recursos de la zona protegida inspiracional ahora también están presentes en la zona protegida de Target para que los pruebe.

   ![Recursos generados en la zona protegida de destinatario](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Pasos siguientes

Después de leer esta guía, ahora comprende mejor cómo aprovechar los libros de reproducción de casos de uso junto con [herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) para crear recorridos ejecutables que hagan referencia a los esquemas. Obtenga más información sobre los [Casos de uso de Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).

### Más ayuda sobre este tema

[Herramientas de zona protegida](/help/sandboxes/ui/sandbox-tooling.md)
