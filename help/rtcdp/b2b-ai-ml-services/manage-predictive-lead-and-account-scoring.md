---
title: Administre la puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B
type: Documentation
description: Este documento proporciona información sobre la administración de la función de puntuación de cuenta y posible cliente predictivo en Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 3%

---

# Administre la puntuación predictiva de clientes potenciales y cuentas en Adobe Real-Time Customer Data Platform, B2B edition

>[!NOTE]
>
>Solo los usuarios con permiso Administrar IA B2B pueden crear, cambiar y eliminar objetivos de puntuación.

Este tutorial le guiará por los pasos para administrar los objetivos de puntuación del servicio de puntuación de cuenta y posible cliente predictivo. Los objetivos de puntuación pueden ser para un perfil de persona o de cuenta

## Crear una nueva puntuación

Para crear una nueva puntuación, seleccione **[!UICONTROL Services]** en la barra lateral y seleccione **[!UICONTROL Create score]**.

![nuevo-puntaje](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Aparece la pantalla **[!UICONTROL Basic information]**, que le solicita que seleccione un tipo de perfil, introduzca un nombre y una descripción opcional. Cuando termine, seleccione **[!UICONTROL Next]**.

![por favor, introduzca información básica](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Aparecerá la pantalla **[!UICONTROL Define your goal]**. Seleccione la flecha desplegable y, a continuación, seleccione un tipo de objetivo en la ventana desplegable que aparece.

![por favor, selecciona una meta](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Se abre el cuadro de diálogo **[!UICONTROL Goal specifics]**. Seleccione la flecha desplegable y, a continuación, seleccione el nombre del campo de objetivo en la ventana desplegable que aparece.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

Aparecerá la selección **[!UICONTROL Goal conditions]**. Seleccione la flecha desplegable y, a continuación, seleccione condición en la ventana desplegable que aparece.

![plas-goal-specific-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Aparece el campo **[!UICONTROL Goal value]**. A continuación, configure su [!UICONTROL Goal specifics]. Seleccione el panel [!UICONTROL Enter Field Value] e introduzca su valor de objetivo.

>[!NOTE]
>
>Se pueden añadir varios valores de objetivo.

![plas-goal-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Para agregar campos adicionales, seleccione **[!UICONTROL Add field]**.

![plas-goal-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Para configurar el periodo de tiempo de predicción, seleccione la flecha desplegable y, a continuación, el periodo de tiempo que desee.

![plan-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

La política de combinación seleccionada determina cómo se seleccionan los valores de campo de un perfil de persona. En la flecha desplegable, seleccione la política de combinación que desee y, a continuación, seleccione **[!UICONTROL Finish]**.

Aparecerá el cuadro de diálogo **[!UICONTROL Scoring setup is complete]** que confirma que se ha creado la nueva puntuación. Seleccione **[!UICONTROL OK]**.

![puntuación-plas-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Cada proceso de puntuación puede tardar hasta 24 horas en completarse.

Ha vuelto a la ficha **[!UICONTROL Services]**, donde puede ver la nueva puntuación creada en la lista de puntuaciones.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Seleccione la puntuación para ver detalles e información adicional sobre los detalles de la última ejecución.

![información-adicional-puntuación-plas](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Para obtener información más detallada sobre los códigos de error que se pueden ver en los detalles de la última ejecución, consulte la sección sobre [códigos de error de canalización de IA de posibles clientes](#leads-ai-pipeline-error-codes) en este documento.

## Editar una puntuación

Para editar una puntuación, selecciónela en la pestaña **[!UICONTROL Services]** y seleccione **[!UICONTROL Edit]** en el panel de detalles adicionales que hay a la derecha de la pantalla.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Edit instance]**, donde podrá editar la descripción de la puntuación. Realice los cambios y seleccione **[!UICONTROL Save]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>La configuración de puntuación no se puede cambiar, ya que esto generará un déclencheur en el reciclaje y la nueva puntuación del modelo. Equivale a eliminar la puntuación y crear una nueva puntuación. Para editar la configuración de la puntuación, deberá clonar esta puntuación o crear una nueva puntuación.

Ha vuelto a la ficha **[!UICONTROL Services]**. Seleccione la puntuación para ver los detalles de la descripción actualizada en el panel de detalles adicionales situado en la parte derecha de la pantalla.

## Clonar una puntuación

Para clonar una puntuación, selecciónela en la pestaña **[!UICONTROL Services]** y seleccione **[!UICONTROL Clone]** en el panel de detalles adicionales que hay a la derecha de la pantalla.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Aparecerá la pantalla **[!UICONTROL Basic information]**. El tipo, el nombre y la descripción del perfil se clonan a partir de la puntuación original. Modifique estos detalles y seleccione **[!UICONTROL Next]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Aparecerá la pantalla **[!UICONTROL Define your goal]**. Complete la sección de metas como lo haría al crear una nueva puntuación y seleccione **[!UICONTROL Finish]**.

Ha vuelto a la ficha **[!UICONTROL Services]**, donde puede ver la puntuación recién clonada en la lista.

>[!NOTE]
>
>La sección **[!UICONTROL Define your goal]** no se clona desde la puntuación original.

## Eliminar una puntuación

Para eliminar una puntuación, selecciónela en la ficha **[!UICONTROL Services]** y seleccione **[!UICONTROL Delete]** en el panel de detalles adicionales que aparece a la derecha de la pantalla.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Aparecerá el cuadro de diálogo de confirmación **[!UICONTROL Delete documentation]**. Seleccione **[!UICONTROL Delete]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Si se elimina la definición de puntuación, también se eliminarán todas las puntuaciones previstas en el perfil de la persona o el perfil de cuenta, pero no el grupo de campos creado para la definición de puntuación. El grupo de campos quedará &quot;huérfano&quot; en el modelo de datos.

Ha vuelto a la ficha **[!UICONTROL Services]**, donde ya no puede ver la puntuación en la lista.

## Códigos de error de canalización de IA de posibles clientes

| Código de error | Mensaje de error |
| --- | --- |
| 401 | ERROR 401. Canalización de IA de posibles clientes detenida: no hay suficientes cuentas válidas para la puntuación de cuentas. Recuento de cuentas: {}. |
| 402 | ERROR 402. Canalización de IA de posibles clientes detenida: no hay suficientes contactos válidos para la puntuación de contactos. Recuento de contactos: {}. |
| 403 | ERROR 403. Canalización de IA de posibles clientes detenida: no hay suficiente volumen de actividad para la formación de modelos. Recuento de eventos: {}. |
| 404 | ERROR 404. Canalización de IA de posibles clientes detenida: no hay suficientes conversiones para la formación de modelos. Recuento de conversiones: {}. |
| 405 | ERROR 405. Canalización de IA de posibles clientes detenida: actividad demasiado dispersa para una formación de modelo válida. Solo el {} por ciento de las cuentas tiene actividad. |
| 406 | ERROR 406. Canalización de IA de posibles clientes detenida: actividad demasiado dispersa para una formación de modelo válida. Solo el {} por ciento de los contactos tiene actividad. |
| 407 | ERROR 407. Canalización de IA de posibles clientes detenida: los tipos de actividad de datos de puntuación no coinciden con los datos de formación. |
| 408 | ERROR 408. Canalización de IA de posibles clientes detenida: la tasa de falta es demasiado alta para las funciones de actividad. Falta la tarifa: {}. |
| 409 | ERROR 409. Canalización de IA de posibles clientes detenida: el auc de prueba es demasiado bajo. Probar auc: {}. |
| 410 | ERROR 410. Canalización de IA de posibles clientes detenida: el auc de prueba es demasiado bajo después de ajustar los parámetros. Probar auc: {}. |
| 411 | ERROR 411. Canalización de IA de posibles clientes detenida: los datos de formación no tienen suficientes conversiones para producir un modelo fiable. Conversiones: {}. |
| 412 | ERROR 412. Canalización de IA de posibles clientes detenida: los datos de prueba no tienen ninguna conversión para calcular el AUC-ROC. |

| Código de información/advertencia | Mensaje |
| --- | --- |
| 100 | INFORMACIÓN 100. Comprobación de calidad de IA de posibles clientes: el recuento de cuentas es: {}. |
| 101 | INFORMACIÓN 101. Comprobación de calidad de IA de posibles clientes: el número de contactos es: {}. |
| 102 | INFORMACIÓN 102. Comprobación de calidad de IA de posibles clientes: el recuento de oportunidades es: {}. |
| 103 | INFORMACIÓN 103. Comprobación de calidad de IA de posibles clientes: el auc de prueba es bajo. Iniciar ajuste de parámetros. Probando auc: {}. |
| 200 | AVISO 200. Comprobación de calidad de IA de posibles clientes: la tasa de falta de características firmográficas es: {}. |
| 201 | AVISO 201. Comprobación de calidad de IA de posibles clientes: la tasa de falta de características de actividad es: {}. |

## Próximos pasos

Al seguir este tutorial, ahora puede crear y administrar correctamente las puntuaciones. Consulte los siguientes documentos para obtener más información:

* [Puntuación predictiva de posibles clientes y cuentas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorización de trabajos predictivos de puntuación de clientes potenciales y cuentas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
