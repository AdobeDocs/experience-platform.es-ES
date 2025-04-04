---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;ABAC
title: Etiquetas de administración de control de acceso basado en atributos
description: Este documento proporciona información sobre la administración de etiquetas a través de la interfaz Permisos en Adobe Experience Cloud
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 24%

---

# Administrar etiquetas

>[!NOTE]
>
>Para crear o ver atributos calculados con campos que contengan una etiqueta determinada, debe tener acceso a esa etiqueta.

Las etiquetas permiten categorizar conjuntos de datos y campos según las políticas de uso y acceso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de los datos en cuanto se incorporan a Experience Platform o en cuanto los datos están disponibles para su uso en Experience Platform.

## Creación de una nueva etiqueta {#create-new-label}

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
>Hay una sola lista de etiquetas para toda una organización. Para crear una etiqueta personalizada, necesitará los permisos de **[!UICONTROL Administrar etiquetas de uso]** en la zona protegida de producción. En este momento no se admite la eliminación de etiquetas.

Para crear una etiqueta nueva, selecciona la pestaña **[!UICONTROL Etiquetas]** en la barra lateral y selecciona **[!UICONTROL Crear etiqueta]**.

![flac-new-label](../../images/flac-ui/create-label.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear una nueva etiqueta]**, que le solicita que escriba un nombre, un nombre descriptivo opcional y una descripción opcional.

![información-etiqueta-nueva](../../images/flac-ui/new-label-info.png)

Cuando termine, seleccione **[!UICONTROL Confirmar]**.
