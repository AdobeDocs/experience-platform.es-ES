---
title: IU de configuración de identidad
description: Aprenda a utilizar la interfaz de usuario de configuración de identidad.
badge: Beta
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 6cdb622e76e953c42b58363c98268a7c46c98c99
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# IU de configuración de identidad

>[!AVAILABILITY]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en fase beta. Póngase en contacto con el equipo de su cuenta de Adobe para obtener información sobre los criterios de participación. La funcionalidad y la documentación están sujetas a cambios.

La configuración de identidad es una característica de la interfaz de usuario del servicio de identidad de Adobe Experience Platform que puede utilizar para designar áreas de nombres únicas y configurar la prioridad del área de nombres.

Lea esta guía para aprender a configurar los ajustes de identidad en la interfaz de usuario.

## Requisitos previos

Lea los siguientes documentos antes de empezar a trabajar con la configuración de identidad:

* [Reglas de vinculación de gráfico de identidad](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Prioridad de área de nombres](./namespace-priority.md)
* [Simulación de gráfico](./graph-simulation.md)

## Configuración de la identidad

Para obtener acceso a la configuración de identidad, vaya al área de trabajo del servicio de identidad en la interfaz de usuario de Adobe Experience Platform y, a continuación, seleccione **[!UICONTROL Configuración]**.

![Botón de configuración de identidad seleccionado.](../images/rules/identities-ui.png)

La página de configuración de identidad se divide en dos secciones: [!UICONTROL Áreas de nombres de persona] y [!UICONTROL Áreas de nombres de dispositivos o cookies]. Las áreas de nombres de persona son identificadores para individuos únicos. Pueden ser ID entre dispositivos, direcciones de correo electrónico y números de teléfono. Las áreas de nombres de dispositivos o cookies son identificadores para dispositivos y exploradores web y no se les puede dar una prioridad mayor que a las áreas de nombres de personas. Tampoco puede designar un dispositivo o espacio de nombres de cookie para que sea un espacio de nombres único.

### Configurar prioridad de área de nombres

Para configurar la prioridad del área de nombres, seleccione un área de nombres en el menú de configuración de identidad y, a continuación, arrastre y suelte el área de nombres en el orden que desee. Coloque un área de nombres en la parte superior de la lista para darle una prioridad mayor y, a la inversa, coloque un área de nombres en la parte inferior de la lista para darle una prioridad menor. El área de nombres con la prioridad más alta también debe designarse como área de nombres única.

![Espacio de trabajo de configuración de identidades con un área de nombres de persona resaltada.](../images/rules/namespace-priority.png)

### Designar un área de nombres única

Para designar un área de nombres única, active la casilla de verificación [!UICONTROL Único por gráfico] que corresponde a ese área de nombres. Puede seleccionar más de un área de nombres única para la configuración de identidad.

![Dos áreas de nombres seleccionadas y definidas como únicas.](../images/rules/unique-namespace.png)

Una vez establecidas las áreas de nombres únicas, los gráficos ya no podrán tener varias identidades que contengan un área de nombres única. Por ejemplo, si ha designado CRMID como un área de nombres única, un gráfico solo puede tener una identidad con el área de nombres CRMID. Para obtener más información, lea la [descripción general del algoritmo de optimización de identidad](./identity-optimization-algorithm.md#unique-namespace).

Cuando haya terminado con sus configuraciones, seleccione **[!UICONTROL Siguiente]**. Aparecerá un mensaje de confirmación, aprovecha esta oportunidad para comprobar que las configuraciones son correctas y, a continuación, selecciona **[!UICONTROL Finalizar]**.

![La página de validación con el estado Fin resaltado.](../images/rules/finish.png)

Aparece un mensaje de advertencia que indica que los gráficos existentes solo se verán afectados por el algoritmo de gráficos si los gráficos se actualizan **después de guardar la configuración** y que la identidad principal de los fragmentos de evento en el Perfil del cliente en tiempo real no se actualizará incluso después de que cambie la prioridad del área de nombres. Además, se le notifica que la nueva configuración tardará **seis horas** en surtir efecto. Para confirmar, escribe el nombre de tu zona protegida y selecciona **[!UICONTROL Confirmar]**.

![Ventana de confirmación que muestra una advertencia sobre un retraso de seis horas antes de que se procesen las configuraciones.](../images/rules/confirm-settings.png)

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Resolución de problemas y preguntas frecuentes](./troubleshooting.md)
* [Prioridad de área de nombres](./namespace-priority.md)
* [IU de simulación de gráficos](./graph-simulation.md)