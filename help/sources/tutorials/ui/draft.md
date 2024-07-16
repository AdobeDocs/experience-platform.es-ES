---
title: Borradores de flujos de datos en la IU
description: Obtenga información sobre cómo guardar los flujos de datos como borrador y publicarlos más adelante, al utilizar el espacio de trabajo de fuentes.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Borradores de flujos de datos en la IU

Guarde el progreso del flujo de trabajo de ingesta de datos sin finalizar estableciendo el flujo de datos en un estado de borrador. Puede reanudar y completar los flujos de datos esbozados más adelante.

Este documento proporciona pasos sobre cómo guardar los flujos de datos al utilizar el área de trabajo de fuentes en la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este documento requiere un entendimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.

## Guardar un flujo de datos como borrador

Puede pausar el progreso de creación del flujo de datos en cualquier momento después de seleccionar los datos que va a introducir en Platform.

Por ejemplo, si desea guardar el progreso durante el paso de detalles del flujo de datos, seleccione **[!UICONTROL Guardar como borrador]**.

![Paso de detalle del flujo de datos del flujo de trabajo de orígenes con la opción Guardar como borrador seleccionada.](../../images/tutorials/draft/save-as-draft.png)

Una vez guardado el borrador, se le redirigirá a la página de su cuenta, donde podrá ver una lista de los flujos de datos existentes, incluidos los borradores.

![Una lista de flujos de datos para una cuenta determinada.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Los flujos de datos borrador no se habilitarán y su estado se establecerá en `draft`.

Para continuar con el borrador, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione **[!UICONTROL Actualizar flujo de datos]**.

>[!NOTE]
>
>Si el borrador incluye información de programación, la ventana desplegable también te dará la opción de **[!UICONTROL Editar programación]**.

![Ventana desplegable con flujo de datos de actualización seleccionado.](../../images/tutorials/draft/update-dataflow.png)

### Acceder a los borradores desde el catálogo de origen

También puede acceder a sus flujos de datos de borrador a través del catálogo de flujos de datos. Seleccione **[!UICONTROL Flujos de datos]** del encabezado superior para acceder al catálogo de flujos de datos. Aquí, busque el borrador en la lista de flujos de datos existentes en su organización, seleccione los puntos suspensivos (`...`) junto a su nombre y, a continuación, seleccione **[!UICONTROL Actualizar flujo de datos]**.

![Una lista de flujos de datos para una organización determinada.](../../images/tutorials/draft/catalog-access.png)

## Publish el flujo de datos de borrador

Volverá al paso [!UICONTROL Agregar datos] del flujo de trabajo de orígenes, donde podrá volver a confirmar el formato de los datos y continuar progresando en el flujo de datos.

Una vez que confirme el formato, el delimitador y el tipo de compresión de los datos, seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso para agregar datos del flujo de trabajo de orígenes.](../../images/tutorials/draft/select-data.png)

A continuación, confirme los detalles del flujo de datos. Utilice la interfaz de detalles del flujo de datos para actualizar las configuraciones relacionadas con el nombre, la descripción, la ingesta parcial, la configuración de diagnóstico de errores y las preferencias de alerta del flujo de datos.

Una vez que haya finalizado las configuraciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso de detalle del flujo de datos del flujo de trabajo de origen.](../../images/tutorials/draft/dataflow-detail.png)

Aparecerá el paso [!UICONTROL Mapping]. Durante este paso, puede volver a configurar las configuraciones de asignación del flujo de datos. Para obtener una guía completa sobre las funciones de preparación de datos utilizadas para la asignación, visite la [guía de IU de preparación de datos](../../../data-prep/ui/mapping.md).

Una vez que haya completado la reconfiguración de la asignación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso de asignación del flujo de trabajo de orígenes.](../../images/tutorials/draft/mapping.png)

Use el paso [!UICONTROL Programación] para establecer un horario de ingesta para su flujo de datos. Puede establecer la frecuencia de ingesta en `once`, `minute`, `hour`, `day` o `week`. Cuando termine, seleccione **[!UICONTROL Siguiente]** para continuar.

![Paso de programación del flujo de trabajo de orígenes.](../../images/tutorials/draft/scheduling.png)

Finalmente, revise los detalles de su flujo de datos y luego seleccione **[!UICONTROL Finalizar]** para publicar su borrador.

![Paso de revisión del flujo de trabajo de orígenes.](../../images/tutorials/draft/review.png)

Después de guardar y publicar un borrador, el flujo de datos se habilitará y ya no podrá restablecerlo como borrador.

## Pasos siguientes

Al seguir este tutorial, ha aprendido a guardar el progreso y establecer un flujo de datos como borrador. Para obtener más información sobre las fuentes, visite [descripción general de las fuentes](../../home.md).
