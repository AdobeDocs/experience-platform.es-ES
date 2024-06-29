---
title: IU de configuración de identidad
description: Aprenda a utilizar la interfaz de usuario de configuración de identidad.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 605aa5ed2db2bfd7f787f2dff9fa00cee2afbce6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# IU de configuración de identidad

>[!AVAILABILITY]
>
>Esta función aún no está disponible; se espera que el programa beta para reglas de vinculación de gráficos de identidad comience en julio en zonas protegidas de desarrollo. Póngase en contacto con el equipo de su cuenta de Adobe para obtener información sobre los criterios de participación.

La configuración de identidad es una característica de la interfaz de usuario del servicio de identidad de Adobe Experience Platform que puede utilizar para designar áreas de nombres únicas y configurar la prioridad del área de nombres.

Lea esta guía para aprender a utilizar la herramienta de configuración de identidad.

## Requisito previo

Lea los siguientes documentos antes de empezar a trabajar con la configuración de identidad:

* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [Prioridad de área de nombres](./namespace-priority.md)
* [Simulación de gráfico](./graph-simulation.md)

## Configuración de la identidad

Para acceder a la configuración de identidad, vaya al espacio de trabajo del servicio de identidad en la interfaz de usuario de Adobe Experience Platform y, a continuación, seleccione **[!UICONTROL Configuración]**.

![Botón de configuración de identidad seleccionado.](../images/rules/identity-ui.png)

Aparecerá la página de configuración de identidad y se le recibirá con un mensaje de confirmación para recordarle que primero pruebe y valide la configuración de identidad en un simulador para pruebas de desarrollo antes de completar la configuración en un simulador para pruebas de producción.

![La página de configuración de identidad.](../images/rules/identity-settings.png)

La página de configuración de identidad se divide en dos secciones: [!UICONTROL Áreas de nombres de persona] y [!UICONTROL Áreas de nombres de dispositivos o cookies]. Las áreas de nombres de persona son identificadores para individuos únicos. Pueden ser ID entre dispositivos, direcciones de correo electrónico y números de teléfono. Las áreas de nombres de dispositivos o cookies son identificadores para dispositivos y exploradores web y no se les puede dar una prioridad mayor que a las áreas de nombres de personas. Tampoco puede designar un dispositivo o espacio de nombres de cookie para que sea un espacio de nombres único.

### Designar un área de nombres única

Para designar un área de nombres única, seleccione [!UICONTROL Únicos por gráfico] casilla de verificación que corresponde a ese área de nombres. Puede seleccionar más de un área de nombres única para la configuración de identidad.

![Dos áreas de nombres únicas seleccionadas.](../images/rules/unique-namespaces.png)

Una vez establecidas las áreas de nombres únicas, los gráficos ya no podrán tener varias identidades que contengan un área de nombres única. Por ejemplo, si ha designado el ID personalizado de Analytics como un área de nombres única, un gráfico solo puede tener una identidad con el área de nombres de ID personalizada de Analytics. Para obtener más información, lea la [resumen del algoritmo de optimización de identidad](./identity-optimization-algorithm.md#unique-namespace).

### Configurar prioridad de área de nombres

Para configurar la prioridad del área de nombres, seleccione un área de nombres en el menú de configuración de identidad y, a continuación, arrastre y suelte el área de nombres en el orden que desee. Coloque un área de nombres más arriba en la lista para darle una prioridad más alta y, a la inversa, coloque un área de nombres más abajo en la lista para darle una prioridad más baja. El área de nombres con la prioridad más alta también debe designarse como área de nombres única.

Cuando haya terminado con las configuraciones, seleccione **[!UICONTROL Siguiente]**. Aparecerá un mensaje de confirmación, aproveche esta oportunidad para comprobar que las configuraciones son correctas y, a continuación, seleccione **[!UICONTROL Finalizar]**.

![La página de validación.](../images/rules/validate.png)

Aparece una advertencia que indica que la nueva configuración no tendrá implicaciones en los vínculos existentes de un gráfico de identidades y en los fragmentos de perfil de evento de experiencia que ya se han introducido. Para confirmar, introduzca el nombre de la zona protegida y seleccione **[!UICONTROL Confirmar]**.

![La ventana de confirmación.](../images/rules/confirm.png)