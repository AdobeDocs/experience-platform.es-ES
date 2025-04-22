---
title: IU de configuración de identidad
description: Aprenda a utilizar la interfaz de usuario de configuración de identidad.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: a309f0dca5ebe75fcb7abfeb98605aec2692324d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 3%

---

# IU de configuración de identidad

>[!AVAILABILITY]
>
>Las reglas de vinculación de gráficos de identidad están actualmente en disponibilidad limitada y todos los clientes pueden acceder a ellas desde los entornos limitados de desarrollo.
>
>* **Requisitos de activación**: la característica permanecerá inactiva hasta que configure y guarde su [!DNL Identity Settings]. Sin esta configuración, el sistema seguirá funcionando normalmente, sin cambios en el comportamiento.
>* **Notas importantes**: durante esta fase de disponibilidad limitada, la segmentación de Edge puede producir resultados inesperados en los miembros del segmento. Sin embargo, la transmisión y la segmentación por lotes funcionarán según lo esperado.
>* **Pasos siguientes**: para obtener información sobre cómo habilitar esta característica en los entornos limitados de producción, póngase en contacto con el equipo de la cuenta de Adobe.

La configuración de identidad es una característica de la interfaz de usuario del servicio de identidad de Adobe Experience Platform que puede utilizar para designar áreas de nombres únicas y configurar la prioridad del área de nombres.

Lea esta guía para aprender a configurar los ajustes de identidad en la interfaz de usuario.

## Requisitos previos

Lea los siguientes documentos antes de empezar a trabajar con la configuración de identidad:

* [[!DNL Identity Graph Linking Rules]](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Prioridad del área de nombres](./namespace-priority.md)
* [Simulación de gráfico](./graph-simulation.md)

### Definición de permisos {#set-permissions}

A continuación, debe asegurarse de que su cuenta esté aprovisionada con los siguientes permisos:

* **[!UICONTROL Ver configuración de identidad]**: aplique este permiso para poder ver áreas de nombres únicas y su prioridad en la página de exploración del área de nombres de identidad.
* **[!UICONTROL Editar configuración de identidad]**: aplique este permiso para poder editar y guardar la configuración de identidad.

Póngase en contacto con el administrador si no tiene estos permisos. Para obtener más información, lea la [guía de permisos](../../access-control/abac/ui/permissions.md).

## Configuración de la identidad

Para obtener acceso a la configuración de identidad, vaya al área de trabajo del servicio de identidad en la interfaz de usuario de Adobe Experience Platform y, a continuación, seleccione **[!UICONTROL Configuración]**.

![Interfaz del panel de identidad con el botón &quot;Configuración&quot; seleccionado.](../images/rules/dashboard.png)

La página de configuración de identidad se divide en dos secciones: [!UICONTROL Áreas de nombres de persona] y [!UICONTROL Áreas de nombres de dispositivos o cookies]. Las áreas de nombres de persona son identificadores para individuos únicos. Pueden ser ID entre dispositivos, direcciones de correo electrónico y números de teléfono. Las áreas de nombres de dispositivos o cookies son identificadores para dispositivos y exploradores web y no se les puede dar una prioridad mayor que a las áreas de nombres de personas. Tampoco puede designar un dispositivo o espacio de nombres de cookie como un espacio de nombres único.

### Configurar prioridad de área de nombres

Para configurar la prioridad del área de nombres, seleccione un área de nombres en el menú de configuración de identidad y, a continuación, arrastre y suelte el área de nombres en el orden que desee. Coloque un área de nombres en la parte superior de la lista para darle una prioridad mayor y, a la inversa, coloque un área de nombres en la parte inferior de la lista para darle una prioridad menor. El área de nombres con la prioridad más alta también debe designarse como área de nombres única.

![Espacio de trabajo de configuración de identidades con un área de nombres de persona resaltada.](../images/rules/namespace-priority.png)

### Designar un área de nombres única

Para designar un área de nombres única, active la casilla de verificación [!UICONTROL Único por gráfico] que corresponde a ese área de nombres. Puede seleccionar **hasta un máximo de tres áreas de nombres únicas** para la configuración de la configuración de identidad.

Una vez establecidas las áreas de nombres únicas, los gráficos ya no podrán tener varias identidades que contengan un área de nombres única. Por ejemplo, si ha designado CRMID como un área de nombres única, un gráfico solo puede tener una identidad con el área de nombres CRMID. Para obtener más información, lea la [descripción general del algoritmo de optimización de identidad](./identity-optimization-algorithm.md#unique-namespace).

Cuando haya terminado con sus configuraciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![Dos áreas de nombres seleccionadas y definidas como únicas.](../images/rules/unique-namespace.png)

A partir de aquí, debe confirmar lo siguiente antes de continuar con el paso final:

1. Las áreas de nombres únicas seleccionadas.
2. La existencia de una identidad con el área de nombres única con mayor prioridad en cada perfil conocido.
3. Orden de prioridad del área de nombres.

![Ventana de confirmación con el botón &quot;confirmar&quot; seleccionado.](../images/rules/confirmation.png)

### Confirmar la configuración {#confirm-your-settings}

>[!IMPORTANT]
>
>* El paso final es otro mensaje de confirmación que indica que los gráficos existentes solo se verán afectados por el algoritmo de gráficos **si los gráficos se actualizan después de guardar la configuración** y que la identidad principal de los fragmentos de evento en el Perfil del cliente en tiempo real no se actualizará incluso después de que cambie la prioridad del área de nombres.
>
>* Además, se le notifica que su configuración nueva o actualizada tardará **seis horas** en surtir efecto. Para confirmar, escribe el nombre de tu zona protegida y selecciona **[!UICONTROL Confirmar]**.

![Ventana de confirmación que muestra una advertencia sobre un retraso de seis horas antes de que se procesen las configuraciones.](../images/rules/complete.png)

## Pasos siguientes

Para obtener más información sobre [!DNL Identity Graph Linking Rules], lea la siguiente documentación:

* [Información general de [!DNL Identity Graph Linking Rules]](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Guía de implementación](./implementation-guide.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Resolución de problemas y preguntas frecuentes](./troubleshooting.md)
* [Prioridad del área de nombres](./namespace-priority.md)
* [IU de simulación de gráficos](./graph-simulation.md)