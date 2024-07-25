---
solution: Experience Platform
title: Guía de IU del servicio de segmentación
description: Obtenga información sobre cómo crear y administrar audiencias y definiciones de segmentos en la interfaz de usuario de Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Guía de IU del servicio de segmentación

[!DNL Adobe Experience Platform Segmentation Service] proporciona una interfaz de usuario para crear y administrar audiencias y definiciones de segmentos.

## Introducción

El trabajo con audiencias y definiciones de segmentos requiere una comprensión de los distintos servicios de [!DNL Experience Platform] involucrados con la segmentación. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] le permite segmentar en grupos más pequeños los datos almacenados en [!DNL Experience Platform] relacionados con personas (como clientes, clientes potenciales, usuarios u organizaciones).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): habilita la creación de perfiles de clientes al unir identidades de distintos orígenes de datos que se están introduciendo en [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar la segmentación de la mejor manera posible, asegúrate de que tus datos se incorporen como perfiles y eventos según las [prácticas recomendadas para el modelado de datos](../../xdm/schema/best-practices.md).

También debe comprender los siguientes términos clave que se utilizan en este documento y la diferencia entre ellos:

- **Audiencia**: Una colección de personas que comparten comportamientos o características similares. Adobe Experience Platform puede generar esta colección de personas mediante definiciones de segmento (audiencia generada por Platform), composición de audiencia o a partir de fuentes externas como cargas personalizadas (audiencia generada externamente).
- **Definición del segmento**: Las reglas que Adobe Experience Platform usa para describir las características clave o el comportamiento de una audiencia de destino.
- **Segmento**: Acto de separar Perfiles en audiencias.

## Información general

En la interfaz de usuario del Experience Platform, seleccione **[!UICONTROL Audiencias]** en el panel de navegación izquierdo para abrir la pestaña **[!UICONTROL Información general]** que muestra el panel [!UICONTROL Audiencias].

>[!NOTE]
>
>Si su organización es nueva en Platform y aún no ha creado conjuntos de datos de perfil o políticas de combinación activos, el panel [!UICONTROL Audiencias] no estará visible. En su lugar, la pestaña [!UICONTROL Información general] muestra vínculos y documentación para ayudarle a empezar a usar las audiencias.

### Panel [!UICONTROL Audiencias] {#segments-dashboard}

El panel **[!UICONTROL Audiencias]** describe las métricas clave relacionadas con los datos de audiencia de su organización.

Para obtener más información, visita la [guía de panel de audiencias](../../dashboards/guides/audiences.md).

![Se muestra el tablero de audiencias. Muestra varios widgets, incluido el tamaño de la audiencia, los perfiles por identidad, la superposición de identidades y la tendencia de cambio de tamaño de la audiencia.](../../dashboards/images/segments/dashboard-overview.png)

## Examinar {#browse}

Seleccione la ficha **[!UICONTROL Examinar]** para ver Audience Portal. Audience Portal proporciona una lista de todas las audiencias que pertenecen a su organización y a la zona protegida e incluye detalles como el recuento de perfiles, el origen, la fecha de creación, la última modificación, las etiquetas y el desglose.

Además, Audience Portal permite crear nuevas audiencias con el Generador de segmentos o la Composición de audiencias, así como importar audiencias generadas externamente en Platform.

Para obtener más información sobre Audience Portal, lea la [descripción general de Audience Portal](./audience-portal.md).

## Composiciones {#compositions}

Seleccione la pestaña **[!UICONTROL Composiciones]** para ver una lista de todas las audiencias generadas a través de Composición de audiencias para su organización.

![Lista de audiencias creadas en Composición de audiencias para su organización.](../images/ui/overview/compositions.png)

De forma predeterminada, esta vista muestra información sobre las audiencias, incluido el nombre, el estado, la fecha de creación, la fecha de creación, la fecha de última actualización y la fecha de última actualización.

Junto a cada audiencia hay un icono de puntos suspensivos. Al seleccionar esta opción, se muestra una lista de las acciones rápidas disponibles para la audiencia.

| Acción | Descripción |
| ------ | ----------- |
| Duplicar | Copia la audiencia seleccionada. |
| Administrar acceso | Administra las etiquetas de acceso que pertenecen a la audiencia. Para obtener más información sobre las etiquetas de acceso, lea la documentación sobre [administración de etiquetas](../../access-control/abac/ui/labels.md). |
| Eliminar | Elimina la audiencia seleccionada. Las audiencias que se usan en destinos de flujo descendente o que dependen de otras audiencias **no se pueden** eliminar. Para obtener más información sobre la eliminación de audiencias, lea las [preguntas frecuentes sobre la segmentación](../faq.md#lifecycle-states). |

Puede seleccionar el icono ![Personalizar tabla](/help/images/icons/column-settings.png) para cambiar los campos que se muestran.

![El botón Personalizar tabla está resaltado. Si selecciona este botón, podrá personalizar los campos que se muestran en la página Composiciones de audiencias.](../images/ui/overview/compositions-select-customize-table.png)

Aparece una ventana emergente que enumera todos los campos que se pueden mostrar en la tabla.

![Atributos que se pueden mostrar para la sección Composición.](../images/ui/overview/compositions-customize-table.png)

| Campo | Descripción |
| ----- | ----------- | 
| [!UICONTROL Nombre] | Nombre de la audiencia. |
| [!UICONTROL Estado] | El estado de la audiencia. Los valores posibles de este campo incluyen `Draft`, `Inactive` y `Published`. |
| [!UICONTROL Creado] | La hora y la fecha de creación de la audiencia. |
| [!UICONTROL Creado por] | El nombre de la persona que creó la audiencia. |
| [!UICONTROL Actualizado] | Fecha y hora en la que se actualizó la audiencia por última vez. |
| [!UICONTROL Actualizado por] | El nombre de la persona que actualizó la audiencia por última vez. |

Para ver la composición de la audiencia, seleccione el nombre de una audiencia en la ficha [!UICONTROL Audiencias].

La página Composición de audiencia aparece con los componentes básicos que componen la audiencia. Para obtener más información acerca de cómo usar la Composición de audiencia, lea la [guía de la interfaz de usuario de la Composición de audiencia](./audience-composition.md).

## Segmentación de streaming {#streaming-segmentation}

La segmentación por transmisión es la capacidad de segmentar [!DNL Platform] en tiempo casi real, al tiempo que se centra en la riqueza de datos. Con la segmentación por streaming, la calificación para la segmentación ahora se produce cuando los datos llegan a [!DNL Platform], lo que alivia la necesidad de programar y ejecutar trabajos de segmentación.

Encontrará más información sobre la segmentación de transmisión en la [guía del usuario de segmentación de transmisión](./streaming-segmentation.md).

>[!NOTE]
>
>Para que la segmentación de streaming funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la sección segmentación de streaming en esta guía del usuario](#scheduled-segmentation).

## Segmentación de Edge {#edge-segmentation}

La segmentación de Edge es la capacidad de evaluar audiencias en Platform de forma instantánea en Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente.

Encontrará más información sobre la segmentación de Edge en la [guía de la interfaz de usuario de segmentación de Edge](./edge-segmentation.md)

## Infracciones de directiva

>[!NOTE]
>
>Las infracciones de directivas solo se aplican si se crea una audiencia que se ha asignado a un destino.

Una vez que haya terminado de crear su audiencia, el control de datos de Adobe Experience Platform analizará la audiencia para asegurarse de que no haya infracciones de directivas dentro de la audiencia. Consulte la [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

![Se muestran las infracciones de directivas para la audiencia.](../images/ui/overview/audience-dule-policy-violations.png)

## Pasos siguientes y recursos adicionales {#next-steps}

La interfaz de usuario [!DNL Segmentation Service] proporciona un flujo de trabajo enriquecido que le permite crear audiencias comercializables a partir de los datos de [!DNL Real-Time Customer Profile].

Para obtener más información acerca de [!DNL Segmentation Service], siga leyendo la documentación. Para aprender a usar la API [!DNL Segmentation Service], lea la [[!DNL Segmentation Service] guía para desarrolladores](../api/overview.md).
