---
title: Administre la puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B
type: Documentation
description: Este documento proporciona información sobre la administración de la función de puntuación de cuenta y posible cliente predictivo en Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Administre la puntuación predictiva de clientes potenciales y cuentas en Adobe Real-time Customer Data Platform, edición B2B

>[!NOTE]
>
>Solo los usuarios con permiso Administrar IA B2B pueden crear, cambiar y eliminar objetivos de puntuación.

Este tutorial le guiará por los pasos para administrar los objetivos de puntuación del servicio de puntuación de cuenta y posible cliente predictivo. Los objetivos de puntuación pueden ser para un perfil de persona o de cuenta

## Crear una nueva puntuación

Para crear una nueva puntuación, seleccione la **[!UICONTROL Servicios]** en la barra lateral y seleccione **[!UICONTROL Crear puntuación]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

El **[!UICONTROL Información básica]** aparece una pantalla en la que se le solicita que seleccione un tipo de perfil, introduzca un nombre y una descripción opcional. Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

El **[!UICONTROL Defina su objetivo]** aparece la pantalla. Seleccione la flecha desplegable y, a continuación, seleccione un tipo de objetivo en la ventana desplegable que aparece.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

El **[!UICONTROL Detalles del objetivo]** se abre. Seleccione la flecha desplegable y, a continuación, seleccione el nombre del campo de objetivo en la ventana desplegable que aparece.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

El **[!UICONTROL Condiciones del objetivo]** aparece la selección. Seleccione la flecha desplegable y, a continuación, seleccione condición en la ventana desplegable que aparece.

![plas-goal-specific-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

El **[!UICONTROL Valor de meta]** aparece el campo. A continuación, configure su [!UICONTROL Detalles del objetivo]. Seleccione el [!UICONTROL Introducir valor de campo] y escriba el valor de la meta.

>[!NOTE]
>
>Se pueden añadir varios valores de objetivo.

![plas-goal-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Para añadir campos adicionales, seleccione **[!UICONTROL Añadir campo]**.

![plas-goal-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Para configurar el periodo de tiempo de predicción, seleccione la flecha desplegable y, a continuación, el periodo de tiempo que desee.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

La política de combinación seleccionada determina cómo se seleccionan los valores de campo de un perfil de persona. En la flecha desplegable, seleccione la política de combinación que desee y, a continuación, seleccione **[!UICONTROL Finalizar]**.

El **[!UICONTROL Configuración de puntuación finalizada]** aparece un cuadro de diálogo que confirma que se ha creado la nueva puntuación. Seleccionar **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Cada proceso de puntuación puede tardar hasta 24 horas en completarse.

Se le devolverá a la **[!UICONTROL Servicios]** pestaña donde puede ver la nueva puntuación creada en la lista de puntuaciones.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Seleccione la puntuación para ver detalles e información adicional sobre los detalles de la última ejecución.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Para obtener información más detallada sobre los códigos de error que se pueden ver en los detalles de la última ejecución, consulte la sección sobre [conduce códigos de error de canalización de IA](#leads-ai-pipeline-error-codes) en este documento.

## Editar una puntuación

Para editar una puntuación, selecciónela en el **[!UICONTROL Servicios]** y seleccione **[!UICONTROL Editar]** en el panel de detalles adicionales, en el lado derecho de la pantalla.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

El **[!UICONTROL Editar instancia]** aparece un cuadro de diálogo en el que puede editar la descripción de la puntuación. Realice los cambios y seleccione **[!UICONTROL Guardar]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>La configuración de puntuación no se puede cambiar, ya que esto generará un déclencheur en el reciclaje y la nueva puntuación del modelo. Equivale a eliminar la puntuación y crear una nueva puntuación. Para editar la configuración de la puntuación, deberá clonar esta puntuación o crear una nueva puntuación.

Se le devolverá a la **[!UICONTROL Servicios]** pestaña. Seleccione la puntuación para ver los detalles de la descripción actualizada en el panel de detalles adicionales situado en la parte derecha de la pantalla.

## Clonar una puntuación

Para clonar una puntuación, seleccione una puntuación en la **[!UICONTROL Servicios]** y seleccione **[!UICONTROL Clonar]** en el panel de detalles adicionales, en el lado derecho de la pantalla.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

El **[!UICONTROL Información básica]** aparece la pantalla. El tipo, el nombre y la descripción del perfil se clonan a partir de la puntuación original. Modifique estos detalles y seleccione **[!UICONTROL Siguiente]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

El **[!UICONTROL Defina su objetivo]** aparece la pantalla. Complete la sección de metas como lo haría al crear una nueva puntuación y seleccione **[!UICONTROL Finalizar]**.

Se le devolverá a la **[!UICONTROL Servicios]** pestaña donde puede ver la puntuación recién clonada en la lista.

>[!NOTE]
>
>El **[!UICONTROL Defina su objetivo]** La sección no se clona desde la puntuación original.

## Eliminar una puntuación

Para eliminar una puntuación, selecciónela en el **[!UICONTROL Servicios]** y seleccione **[!UICONTROL Eliminar]** en el panel de detalles adicionales, en el lado derecho de la pantalla.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

El **[!UICONTROL Eliminar documentación]** Aparecerá el cuadro de diálogo de confirmación. Seleccione **[!UICONTROL Eliminar]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Si se elimina la definición de puntuación, también se eliminarán todas las puntuaciones previstas en el perfil de la persona o el perfil de cuenta, pero no el grupo de campos creado para la definición de puntuación. El grupo de campos quedará &quot;huérfano&quot; en el modelo de datos.

Se le devolverá a la **[!UICONTROL Servicios]** donde ya no puede ver la puntuación en la lista.

## Códigos de error de canalización de IA de posibles clientes

| Código de error | Mensaje de error |
| --- | --- |
| 401 | ERROR 401. Canalización de IA de posibles clientes detenida: no hay suficientes cuentas válidas para la puntuación de cuentas. Recuento de cuentas: {}. |
| 402 | ERROR 402. Canalización de IA de posibles clientes detenida: no hay suficientes contactos válidos para la puntuación de contactos. Recuento de contactos: {}. |
| 403 | ERROR 403. Canalización de IA de posibles clientes detenida: no hay suficiente volumen de actividad para la formación de modelos. Recuento de eventos: {}. |
| 404 | ERROR 404. Canalización de IA de posibles clientes detenida: no hay suficientes conversiones para la formación de modelos. Recuento de conversiones: {}. |
| 405 | ERROR 405. Canalización de IA de posibles clientes detenida: actividad demasiado dispersa para una formación de modelo válida. Solo {} el porcentaje de cuentas tiene actividad. |
| 406 | ERROR 406. Canalización de IA de posibles clientes detenida: actividad demasiado dispersa para una formación de modelo válida. Solo {} el porcentaje de contactos tiene actividad. |
| 407 | ERROR 407. Canalización de IA de posibles clientes detenida: los tipos de actividad de datos de puntuación no coinciden con los datos de formación. |
| 408 | ERROR 408. Canalización de IA de posibles clientes detenida: la tasa de falta es demasiado alta para las funciones de actividad. Tasa faltante: {}. |
| 409 | ERROR 409. Canalización de IA de posibles clientes detenida: el auc de prueba es demasiado bajo. Probar auc: {}. |
| 410 | ERROR 410. Canalización de IA de posibles clientes detenida: el auc de prueba es demasiado bajo después de ajustar los parámetros. Probar auc: {}. |
| 411 | ERROR 411. Canalización de IA de posibles clientes detenida: los datos de formación no tienen suficientes conversiones para producir un modelo fiable. Conversiones: {}. |
| 412 | ERROR 412. Canalización de IA de posibles clientes detenida: los datos de prueba no tienen ninguna conversión para calcular el AUC-ROC. |

| Código de información/advertencia | Mensaje |
| --- | --- |
| 100 | INFORMACIÓN 100. Comprobación de calidad de AI de posibles clientes: el recuento de cuentas es: {}. |
| 101 | INFORMACIÓN 101. Comprobación de calidad de AI de posibles clientes: el recuento de contactos es: {}. |
| 102 | INFORMACIÓN 102. Comprobación de calidad de IA de posibles clientes: el recuento de oportunidades es: {}. |
| 103 | INFORMACIÓN 103. Comprobación de calidad de IA de posibles clientes: el auc de prueba es bajo. Iniciar ajuste de parámetros. Probando auc: {}. |
| 200 | AVISO 200. Comprobación de calidad de la IA de posibles clientes: la tasa de ausencia de funciones firmográficas es: {}. |
| 201 | AVISO 201. Comprobación de calidad de IA de posibles clientes: la tasa de ausencia de funciones de actividad es: {}. |

## Pasos siguientes

Al seguir este tutorial, ahora puede crear y administrar correctamente las puntuaciones. Consulte los siguientes documentos para obtener más información:

* [Puntuación predictiva de posibles clientes y cuentas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorización de trabajos predictivos de puntuación de clientes potenciales y cuentas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
