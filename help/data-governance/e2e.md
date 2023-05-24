---
title: Guía completa de administración de datos
description: Siga el proceso completo para aplicar restricciones de uso de datos para campos y conjuntos de datos en Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: dca5c9df82434d75238a0a80f15e5562cf2fa412
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 0%

---

# Guía completa de administración de datos

Para controlar qué acciones de marketing se pueden realizar en determinados conjuntos de datos y campos en Adobe Experience Platform, debe configurar lo siguiente:

1. [Aplicar etiquetas](#labels) a los campos de esquemas o conjuntos de datos completos, cuyo uso desea restringir.
1. [Configurar y habilitar directivas de gobernanza de datos](#policy) que determinan qué tipos de datos etiquetados se pueden utilizar para determinadas acciones de marketing.
1. [Aplicación de acciones de marketing a sus destinos](#destinations) para indicar qué políticas se aplican a los datos enviados a esos destinos.

Una vez que haya terminado de configurar las etiquetas, las políticas de gobernanza y las acciones de marketing, puede [probar la aplicación de directivas](#test) para asegurarse de que funciona según lo esperado.

Esta guía muestra el proceso completo de configuración y aplicación de una política de gobernanza de datos en la interfaz de usuario de Platform. Para obtener información más detallada sobre las funciones utilizadas en esta guía, consulte la documentación de información general sobre los siguientes temas:

* [Gobernanza de datos de Adobe Experience Platform](./home.md)
* [Etiquetas de uso de datos](./labels/overview.md)
* [Políticas de uso de datos](./policies/overview.md)
* [Aplicación de políticas](./enforcement/overview.md)

>[!NOTE]
>
>Esta guía se centra en cómo configurar y aplicar directivas sobre cómo se utilizan o activan los datos en Experience Platform. Si está intentando restringir **access** para ver los datos en sí para determinados usuarios de Platform de su organización, consulte la guía completa sobre [control de acceso basado en atributos](../access-control/abac/end-to-end-guide.md) en su lugar. El control de acceso basado en atributos también utiliza etiquetas y directivas, pero para un caso de uso diferente al de la gobernanza de datos.

## Aplicar etiquetas {#labels}

>[!IMPORTANT]
>
>Las etiquetas ya no se pueden aplicar a campos individuales en el nivel de conjunto de datos. Este flujo de trabajo ha quedado obsoleto y favorece la aplicación de etiquetas en el nivel de esquema. Sin embargo, aún puede etiquetar un conjunto de datos completo. Cualquier etiqueta aplicada anteriormente a campos de conjuntos de datos individuales seguirá siendo compatible mediante la IU de Platform hasta el 31 de mayo de 2024. Para garantizar que las etiquetas sean coherentes en todos los esquemas, cualquier etiqueta adjunta anteriormente a campos de nivel de conjunto de datos debe migrarse al nivel de esquema durante el próximo año. Consulte la sección sobre [migración de etiquetas aplicadas anteriormente](#migrate-labels) para obtener instrucciones sobre cómo hacerlo.

Puede [aplicación de etiquetas a un esquema](#schema-labels) para que todos los conjuntos de datos basados en ese esquema hereden las mismas etiquetas. Esto le permite administrar las etiquetas de control de datos, consentimiento y control de acceso en un solo lugar. Al aplicar restricciones de uso de datos en el nivel de esquema, el efecto se propaga de forma descendente a todos los conjuntos de datos basados en ese esquema. Las etiquetas aplicadas en el nivel de campo de esquema admiten casos de uso de gobernanza de datos y se pueden detectar en el espacio de trabajo Conjuntos de datos [!UICONTROL Gobernanza de datos] debajo de la pestaña [!UICONTROL Nombre de campo] como etiquetas de solo lectura.

Si hay un conjunto de datos específico en el que desea aplicar restricciones de uso de datos, puede [aplicar etiquetas directamente a ese conjunto de datos](#dataset-labels) o campos específicos dentro de ese conjunto de datos.

Como alternativa, puede [aplicación de etiquetas a un esquema](#schema-labels) para que todos los conjuntos de datos basados en ese esquema hereden las mismas etiquetas.

>[!NOTE]
>
>Para obtener más información sobre las distintas etiquetas de uso de datos y su uso previsto, consulte la [referencia de etiquetas de uso de datos](./labels/reference.md). Si las etiquetas principales disponibles no abarcan todos los casos de uso deseados, puede [definir sus propias etiquetas personalizadas](./labels/user-guide.md#manage-custom-labels) y también.

### Aplicar etiquetas a todo un conjunto de datos {#dataset-labels}

Seleccionar **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo, seleccione el nombre del conjunto de datos al que desee aplicar las etiquetas. Si lo desea, puede utilizar el campo de búsqueda para reducir la lista de conjuntos de datos mostrados.

![La pestaña Examinar del espacio de trabajo de conjuntos de datos con Conjuntos de datos y una fila de conjunto de datos resaltada.](./images/e2e/select-dataset.png)

Aparecerá la vista de detalles del conjunto de datos. Seleccione el **[!UICONTROL Gobernanza de datos]** para ver una lista de los campos del conjunto de datos y las etiquetas que ya se les han aplicado. Seleccione el icono de lápiz para editar las etiquetas de los conjuntos de datos.

![La pestaña Control de datos para el conjunto de datos de miembros socio con el icono de lápiz resaltado.](./images/e2e/edit-dataset-labels.png)

El [!UICONTROL Editar etiquetas de gobernanza] aparece el cuadro de diálogo. Seleccione la etiqueta de gobernanza adecuada y seleccione **[!UICONTROL Guardar]**.

![El cuadro de diálogo Editar etiquetas de gobernanza con la casilla de verificación de etiqueta y Guardar resaltados.](./images/e2e/edit-dataset-governance-labels.png)

### Aplicación de etiquetas a un esquema {#schema-labels}

Seleccionar **[!UICONTROL Esquemas]** en el panel de navegación izquierdo, seleccione el esquema al que desee añadir etiquetas desde la lista.

>[!TIP]
>
>Si no está seguro de qué esquema se aplica a un conjunto de datos concreto, seleccione **[!UICONTROL Conjuntos de datos]** en el menú de navegación de la izquierda, seleccione el enlace debajo de la barra de herramientas **[!UICONTROL Esquema]** para el conjunto de datos deseado. Seleccione el nombre del esquema en la ventana emergente que aparece para abrirlo en el Editor de esquemas.
>
>![Imagen que muestra un vínculo al esquema de un conjunto de datos](./images/e2e/schema-from-dataset.png)

La estructura del esquema aparece en el Editor de esquemas. Aquí, seleccione la **[!UICONTROL Etiquetas]** para mostrar una vista de lista de los campos del esquema y las etiquetas que ya se han aplicado a ellos. Seleccione las casillas de verificación situadas junto a los campos a los que desee agregar etiquetas y, a continuación, seleccione **[!UICONTROL Aplicación de etiquetas de acceso y de gobernanza de datos]** en el carril derecho.

![La pestaña Etiquetas del espacio de trabajo de esquema con un solo campo de esquema seleccionado y Aplicar etiquetas de acceso y control de datos resaltadas.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Si desea agregar etiquetas a todos los campos del esquema, seleccione el icono de lápiz en la fila superior.
>
>![Imagen que muestra el icono de lápiz seleccionado en la vista de etiquetas de esquema](./images/e2e/label-whole-schema.png)

El [!UICONTROL Aplicación de etiquetas de acceso y de gobernanza de datos] aparece el cuadro de diálogo. Seleccione las etiquetas que desee aplicar al campo de esquema elegido. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![El cuadro de diálogo Aplicar etiquetas de acceso y control de datos muestra varias etiquetas que se agregan a un campo de esquema.](./images/e2e/save-schema-labels.png)

Siga los pasos anteriores para aplicar etiquetas a diferentes campos (o esquemas) según sea necesario. Cuando termine, puede continuar con el siguiente paso de [habilitar directivas de gobernanza de datos](#policy).

### Migrar etiquetas aplicadas anteriormente en el nivel de conjunto de datos {#migrate-labels}

Seleccionar **[!UICONTROL Conjunto de datos]** en el panel de navegación izquierdo, seleccione el nombre del conjunto de datos desde el que desea migrar las etiquetas. Si lo desea, puede utilizar el campo de búsqueda para reducir la lista de conjuntos de datos mostrados.

![La pestaña Examinar del área de trabajo Conjuntos de datos con el conjunto de datos de miembros de fidelidad resaltado.](./images/e2e/select-dataset.png)

Aparecerá la vista de detalles del conjunto de datos. Seleccione el **[!UICONTROL Gobernanza de datos]** para ver una lista de los campos del conjunto de datos y las etiquetas que ya se les han aplicado. Seleccione el icono Cancelar junto a cualquier etiqueta que desee eliminar de un campo. Aparecerá un cuadro de diálogo de confirmación, seleccione [!UICONTROL Quitar etiqueta] para confirmar sus opciones.

![La pestaña Control de datos del espacio de trabajo Conjuntos de datos con una etiqueta para un campo resaltado para su eliminación.](./images/e2e/remove-label.png)

Una vez eliminada la etiqueta del campo del conjunto de datos, vaya al Editor de esquemas para agregar la etiqueta al esquema. Las instrucciones para hacerlo se encuentran en la sección [sección sobre aplicación de etiquetas a un esquema](#schema-labels).

>[!TIP]
>
>Puede seleccionar el nombre del esquema en el carril derecho, seguido del vínculo en el cuadro de diálogo que aparece para desplazarse al esquema adecuado.
>![La pestaña Control de datos del espacio de trabajo Conjuntos de datos con el nombre del esquema en la barra lateral y el vínculo de diálogo resaltado.](./images/e2e/navigate-to-schema.png)

Después de migrar las etiquetas necesarias, asegúrese de que dispone de las etiquetas correctas [políticas de gobernanza de datos habilitadas](#policy).

## Habilitar políticas de gobernanza de datos {#policy}

Después de aplicar etiquetas a los esquemas o conjuntos de datos, puede crear políticas de gobernanza de datos que restrinjan las acciones de marketing para las que se pueden utilizar determinadas etiquetas.

Seleccionar **[!UICONTROL Políticas]** en el panel de navegación izquierdo para ver una lista de las directivas principales definidas por Adobe, así como las directivas personalizadas creadas anteriormente por su organización.

Cada etiqueta principal tiene asociada una directiva principal que, cuando está habilitada, aplica las restricciones de activación adecuadas a cualquier dato que contenga esa etiqueta. Para habilitar una directiva principal, selecciónela en la lista y, a continuación, seleccione la **[!UICONTROL Estado de política]** cambiar a **[!UICONTROL Habilitado]**.

![Imagen que muestra una política principal habilitada en la IU](./images/e2e/enable-core-policy.png)

Si las políticas principales disponibles no cubren todos los casos de uso (como cuando utiliza etiquetas personalizadas que ha definido en su organización), puede definir una política personalizada en su lugar. Desde el **[!UICONTROL Políticas]** workspace, seleccione **[!UICONTROL Crear política]**.

![Imagen que muestra el [!UICONTROL Crear política] botón seleccionado en la interfaz de usuario](./images/e2e/create-policy.png)

Aparece una ventana emergente que le solicita que seleccione el tipo de directiva que desea crear. Seleccionar **[!UICONTROL Política de gobernanza de datos]**, luego seleccione **[!UICONTROL Continuar]**.

![Imagen que muestra el [!UICONTROL Política de gobernanza de datos] opción seleccionada](./images/e2e/governance-policy.png)

En la pantalla siguiente, proporcione un **[!UICONTROL Nombre]** y opcional **[!UICONTROL Descripción]** para la directiva. En la tabla siguiente, seleccione las etiquetas que desea que compruebe esta directiva. En otras palabras, estas son las etiquetas que la directiva evitará que se utilicen para las acciones de marketing especificadas en el siguiente paso.

Si selecciona varias etiquetas, puede utilizar las opciones del carril derecho para determinar si todas las etiquetas deben estar presentes para que la directiva aplique las restricciones de uso o si solo debe estar presente una de las etiquetas. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Imagen que muestra la configuración básica de la directiva completada en la IU](./images/e2e/configure-policy.png)

En la pantalla siguiente, seleccione las acciones de marketing para las que esta directiva restringirá el uso de las etiquetas seleccionadas anteriormente. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![Imagen que muestra una acción de marketing asignada a una directiva en la interfaz de usuario](./images/e2e/select-marketing-action.png)

La pantalla final muestra un resumen de los detalles de la política y las acciones que restringirá para qué etiquetas. Seleccionar **[!UICONTROL Finalizar]** para crear la directiva.

![Imagen que muestra la configuración de la directiva que se confirma en la interfaz de usuario](./images/e2e/confirm-policy.png)

La directiva se crea, pero se establece en [!UICONTROL Desactivado] de forma predeterminada. Seleccione la directiva en la lista y establezca **[!UICONTROL Estado de política]** cambiar a **[!UICONTROL Habilitado]** para habilitar la directiva.

![Imagen que muestra la política creada que se habilita en la interfaz de usuario](./images/e2e/enable-created-policy.png)

Siga los pasos anteriores para crear y habilitar las directivas que necesita antes de pasar al siguiente paso.

## Administrar acciones de marketing para destinos {#destinations}

Para que las directivas habilitadas determinen con precisión qué datos se pueden activar en un destino, debe asignar acciones de marketing específicas a ese destino.

Por ejemplo, considere una directiva habilitada que impida cualquier dato que contenga un `C2` etiqueta de ser utilizada para la acción de marketing &quot;[!UICONTROL Exportar a terceros]&quot;. Al activar datos en un destino, la directiva comprueba qué acciones de marketing están presentes en el destino. Si &quot;[!UICONTROL Exportar a terceros]&quot; está presente, intentando activar datos con un `C2` La etiqueta provoca una infracción de directiva. Si &quot;[!UICONTROL Exportar a terceros]&quot; no está presente, la directiva no se aplica para el destino y los datos con `C2` las etiquetas se pueden activar libremente.

Cuándo [conexión de un destino en la IU](../destinations/ui/connect-destination.md), el **[!UICONTROL Gobernanza]** Este paso en el flujo de trabajo le permite seleccionar las acciones de marketing que se aplican a este destino, las cuales determinan finalmente qué políticas de gobernanza de datos se aplican al destino.

![Imagen que muestra las acciones de marketing seleccionadas para un destino](./images/e2e/destination-marketing-actions.png)

## Probar la aplicación de directivas {#test}

Una vez que haya etiquetado los datos, haya habilitado las políticas de control de datos y haya asignado acciones de marketing a sus destinos, puede probar si las políticas se aplican según lo esperado.

Si configura las cosas correctamente, al intentar activar datos que están restringidos por las directivas, la activación se deniega automáticamente y aparece un mensaje de infracción de directiva, en el que se describe información detallada del linaje de datos sobre la causa de la infracción.

Consulte el documento sobre [aplicación automática de políticas](./enforcement/auto-enforcement.md) para obtener más información sobre cómo interpretar los mensajes de infracción de directivas.

## Pasos siguientes

Esta guía abarcaba los pasos necesarios para configurar y aplicar directivas de gobernanza de datos en los flujos de trabajo de activación. Para obtener información más detallada sobre los componentes de control de datos implicados en esta guía, consulte la siguiente documentación:

* [Etiquetas de uso de datos](./labels/overview.md)
* [Políticas de uso de datos](./policies/overview.md)
* [Aplicación de políticas](./enforcement/overview.md)
