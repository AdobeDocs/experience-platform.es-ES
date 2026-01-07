---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos
title: Etiquetas de administración de control de acceso basado en atributos
description: Administre etiquetas a través de la interfaz Permisos en Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# Administrar etiquetas

Puede utilizar etiquetas para categorizar conjuntos de datos y campos según el uso de datos y las políticas de control de acceso basadas en atributos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas alientan el etiquetado de datos en cuanto se incorporan a Adobe Experience Platform o en cuanto los datos están disponibles para su uso. Lea este documento para aprender a administrar etiquetas en la interfaz de usuario de permisos.

Para obtener una lista completa de etiquetas y sus directivas de gobernanza correspondientes, lea la guía de [etiquetas de uso de datos principales](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Para crear o ver [atributos calculados](../../../profile/computed-attributes/overview.md){target="_blank"} con campos que contengan una etiqueta determinada, debe tener acceso a esa etiqueta.

## Explorar etiquetas {#explore-labels}

Para ver todas las etiquetas disponibles, vaya a **[!UICONTROL Permissions]** en [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Seleccione **[!UICONTROL Labels]** del panel izquierdo.

![El espacio de trabajo de etiquetas dentro de Permisos con etiquetas resaltadas en el panel izquierdo.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Las etiquetas se clasifican por tipo y pertenecen a una de las siguientes categorías:

| Tipo | Descripción |
| --- | --- |
| [Contrato](../../../data-governance/labels/reference.md#contract){target="_blank"} | Esta categoría se utiliza para categorizar los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos de su organización. |
| [Identidad](../../../data-governance/labels/reference.md#identity){target="_blank"} | Esta categoría se utiliza para categorizar los datos que pueden identificar a una persona directa o indirectamente. |
| [Sensible](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Esta categoría se utiliza para categorizar los datos que su organización considera confidenciales. |
| [Ecosistema asociado](../../../data-governance/labels/reference.md#partner){target="_blank"} | Esta categoría se utiliza para categorizar los datos obtenidos de fuentes externas a la organización. |
| Compromiso responsable | Esta categoría contiene una sola etiqueta, **[!UICONTROL Potential for Bias]**, que refleja datos que pueden introducir sesgos. |
| Personalizado | Esta categoría incluye etiquetas creadas por su organización. |

Para filtrar etiquetas, seleccione el icono de filtro (![icono de filtro](/help/images/icons/filter.png)) y luego seleccione el tipo de etiqueta que desee en la lista desplegable **[!UICONTROL Type]**.

![Área de trabajo de etiquetas con la opción de filtro expandida y la lista desplegable de tipo resaltada.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Para ver una etiqueta individual, seleccione su nombre en la lista. Aparecerá la página de detalles de la etiqueta. Las etiquetas principales de Adobe son **no** editables.

![Página de detalles de una etiqueta individual.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Crear una etiqueta personalizada {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Uso de etiquetas"
>abstract="Puede utilizar etiquetas personalizadas para aplicar a los datos configuraciones de control de acceso y de gobernanza de datos."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Crear nueva etiqueta"
>abstract="Puede crear sus propias etiquetas personalizadas para adaptarlas a las necesidades de su organización. Las etiquetas personalizadas se pueden usar para aplicar a los datos configuraciones de control de acceso y de gobernanza de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=es#manage-labels" text="Administración de etiquetas personalizadas"

>[!NOTE]
>
>Para crear una etiqueta personalizada, necesitará una función que contenga los permisos de **[!UICONTROL Manage Usage Labels]** y la zona protegida de `Prod`.

Para crear una etiqueta nueva, seleccione **[!UICONTROL Labels]** en el panel izquierdo del área de trabajo **[!UICONTROL Permissions]** y luego seleccione **[!UICONTROL Create label]**.

![Área de trabajo de etiquetas con la opción Crear etiqueta resaltada.](../../images/ui/labels/create-label.png){zoomable="yes"}

Aparece el cuadro de diálogo **[!UICONTROL Create new label]**, que le pide que escriba un **[!UICONTROL Name]**, un **[!UICONTROL Friendly name]** y **[!UICONTROL Description]**.

>[!IMPORTANT]
>
> La etiqueta [!UICONTROL Name] no se puede cambiar una vez creada la etiqueta y no se admite actualmente la eliminación de etiquetas.

Seleccione **[!UICONTROL Confirm]** para terminar de crear su etiqueta.

![Se completó el cuadro de diálogo Crear nueva etiqueta con el nombre, el nombre descriptivo y la descripción, y se resaltó la opción Confirmar.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Edición de una etiqueta personalizada {#edit-custom-label}

Aunque no puede editar **[!UICONTROL Name]** de una etiqueta personalizada, puede editar **[!UICONTROL Friendly name]** y **[!UICONTROL Description]**. Para editar una etiqueta personalizada, selecciónela en la lista del área de trabajo **[!UICONTROL Labels]**.

![Espacio de trabajo de etiquetas con la etiqueta resaltada.](../../images/ui/labels/select-label.png){zoomable="yes"}

Edite cualquiera de los campos y, a continuación, haga clic en cualquier lugar fuera del cuadro de texto para guardar los cambios. Aparecerá un mensaje de confirmación en la pantalla y cambiarán el nombre **[!UICONTROL Modified by]** y la fecha **[!UICONTROL Modified]**.

![Página de detalles de la etiqueta con un mensaje &quot;actualizado correctamente&quot;.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Próximos pasos

Ahora que tiene una comprensión más profunda de las etiquetas, puede empezar a [aplicarlas a esquemas](../../../xdm/tutorials/labels.md).
