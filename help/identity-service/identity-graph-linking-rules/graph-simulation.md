---
title: Guía de IU de simulación de gráficos
description: Aprenda a utilizar la simulación de gráfico en la interfaz de usuario del servicio de ID.
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 28eab3488dccdcc6239b9499e875c31ff132fd48
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 3%

---

# Guía de la interfaz de usuario de [!DNL Graph Simulation] {#graph-simulation}

>[!CONTEXTUALHELP]
>id="platform_identities_graphsimulation"
>title="Simulación de gráficos"
>abstract="Simule gráficos para comprender cómo vincula el servicio de identidad las identidades y cómo funciona el algoritmo de optimización de identidad."

[!DNL Graph Simulation] es una herramienta en la interfaz de usuario del servicio de identidad que puedes usar para simular cómo se comporta un gráfico de identidad dada una combinación particular de identidades y cómo configuras el [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md).

Vea el siguiente vídeo para obtener información adicional sobre el uso de la interfaz [!DNL Graph Simulation] en el área de trabajo de la interfaz de usuario del servicio de identidad:

>[!VIDEO](https://video.tv.adobe.com/v/3444046/?captions=spa&learn=on&enablevpops)

Lea este documento para aprender cómo puede usar [!DNL Graph Simulation] para comprender mejor el comportamiento del gráfico de identidad y cómo funciona el algoritmo del gráfico.

## Conocer la interfaz de [!DNL Graph Simulation] {#interface}

Puede acceder a [!DNL Graph Simulation] en la interfaz de usuario de Adobe Experience Platform. Seleccione **[!UICONTROL Identities]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Graph Simulation]** en el encabezado superior.

![Interfaz de simulación de gráficos en la interfaz de usuario de Adobe Experience Platform.](../images/graph-simulation/graph-simulation.png)

La interfaz [!DNL Graph Simulation] se puede dividir en tres secciones:

>[!BEGINTABS]

>[!TAB Eventos]

Eventos: utilice el panel **[!UICONTROL Events]** para agregar identidades y simular un gráfico. Una identidad completa debe tener un área de nombres de identidad y su valor de identidad correspondiente. Debe añadir al menos dos identidades para simular un gráfico. También puede seleccionar **[!UICONTROL Load Example]** para introducir un evento preconfigurado y la configuración del algoritmo.

![Panel de eventos de la herramienta Simulación de gráficos.](../images/graph-simulation/events.png)

>[!TAB Configuración de algoritmo]

Configuración del algoritmo: Utilice el panel **[!UICONTROL Algorithm configuration]** para agregar y configurar el algoritmo de optimización para sus áreas de nombres. Puede arrastrar y soltar un área de nombres para modificar su respectiva clasificación de prioridad. También puede seleccionar **[!UICONTROL Unique Per Graph]** para determinar si un área de nombres es única.

![La configuración del algoritmo de la herramienta de simulación de gráficos.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Visor de gráficos simulado]

visualizador de gráfico simulado: el gráfico simulado visualizador muestra el gráfico resultante en función de los eventos agregados y del algoritmo que ha configurado. Una línea recta entre dos identidades significa que se establece un vínculo. Una línea discontinua indica que se ha eliminado un vincular.

![El gráfico simulado visualizador panel, con un ejemplo de un gráfico simulado.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Añadir eventos {#add-events}

Para empezar, seleccione **[!UICONTROL Add events]**.

![Se seleccionó el botón Agregar eventos.](../images/graph-simulation/add-events.png)

Aparece una ventana emergente para [!UICONTROL Event #1]. Desde aquí, introduzca su área de nombres de identidad y la combinación de valor de identidad. Puede utilizar el menú desplegable para seleccionar un área de nombres de identidad. También puede escribir las primeras letras de un área de nombres y, a continuación, seleccionar las opciones proporcionadas en el menú desplegable. Una vez que haya seleccionado el área de nombres, proporcione un valor de identidad que se corresponda con el área de nombres.

![Ventana de #1 de eventos con una interfaz vacía.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>El valor de identidad que ingresó durante [!DNL Graph Simulation] ejercicios no tiene por qué ser valores de identidad reales y puede ser marcadores de posición simples.

Una vez completada la primera identidad, seleccione el icono de agregar (**`+`**) para agregar una segunda identidad.

![La primera identidad completa de {Email: tom@acme.com} se ingresa en el panel Eventos de la simulación de gráficos.](../images/graph-simulation/event-one-added.png)

A continuación, repita los mismos pasos y añada una segunda identidad. Se requieren dos identidades completas para generar un gráfico de identidades. En el ejemplo siguiente, se agrega un ECID como área de nombres y se proporciona con el valor `111`. Cuando termine, seleccione **[!UICONTROL Save]**.

![Una segunda identidad de {ECID: 111} se agrega al Evento #1.](../images/graph-simulation/first-event.png)

La [!UICONTROL Events] interfaz se actualiza para mostrar su primer evento, que en este caso es: `{Email: tom@acme.com, ECID: 111}`.

![La interfaz de eventos actualizada con {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

A continuación, repita los mismos pasos para agregar un segundo evento. Para el evento #2, agregue `{Email: summer@acme.com}` como su primera identidad y, a continuación, agregue la misma `{ECID: 111}` como la segunda identidad, creando así un segundo evento de: `{Email: summer@acme.com}, {ECID: 111}`. Cuando finalice, debería tener dos eventos, uno para `{Email: tom@acme.com, ECID: 111}` y otro para `{Email: summer@acme.com}, {ECID: 111}`.

![Interfaz de eventos actualizada con dos eventos.](../images/graph-simulation/two-events.png)

### Cargar ejemplo {#load-example}

Seleccione **[!UICONTROL Load example]** para configurar un gráfico de ejemplo con un algoritmo preestablecido y una configuración de evento.

![Opción de ejemplo de carga seleccionada.](../images/graph-simulation/load-example.png)

Aparece una ventana emergente que le proporciona escenarios de gráficos disponibles entre los que puede elegir:

| Gráfico de ejemplo | Descripción | Ejemplo |
| --- | --- | --- |
| Dispositivo compartido | Dispositivo compartido hace referencia a escenarios en los que dos usuarios diferentes inician sesión en el mismo dispositivo individual. | Un esposo y una esposa comparten un iPad para navegar por Internet y el comercio electrónico. |
| Teléfono no válido (no único) | Teléfono no válido o no único se refiere a escenarios en los que dos usuarios diferentes usan el mismo número de teléfono para crear un cuenta. | Una madre y su hija usan el número de teléfono compartido de su casa para inscribirse en cualquier cuenta comercio electrónico. |
| Valores de identidad “incorrectos” | Los valores de identidad &quot;malos&quot; se refieren a escenarios en los que el servicio de identidad genera IDFA no únicos debido a un implementación erróneo. | WebSDK envía erróneamente un `user_null` valor para cada evento debido a problemas de implementación de código. |

![Ventana que muestra los ejemplos preconfigurados disponibles: dispositivo compartido, teléfono no válido y valores de identidad erróneos.](../images/graph-simulation/example-options.png)

Seleccione cualquiera de las opciones para cargar [!DNL Graph Simulation] con los eventos y el algoritmo preconfigurados. Puede seguir realizando configuraciones en cualquier ejemplo de escenario de gráfico cargado previamente.

![Los eventos y el algoritmo configurados para el teléfono no válido.](../images/graph-simulation/example-loaded.png)

Cuando termine, seleccione **[!UICONTROL Simulate]**.

![Se simuló un gráfico de ejemplo para un teléfono no válido.](../images/graph-simulation/example-simulated.png)

### Usar versión de texto {#use-text-version}

También puede utilizar el modo de texto para configurar eventos. Para usar el modo de texto, seleccione el icono de configuración y, a continuación, seleccione **[!UICONTROL Text (Advanced users)]**.

![Icono de configuración seleccionado.](../images/graph-simulation/settings.png)

Puede introducir manualmente sus identidades con el modo de texto. Use dos puntos (`:`) para distinguir el valor de identidad que corresponde al área de nombres que ha introducido y, a continuación, use una coma (`,`) para separar las identidades. Para distinguir distintos eventos entre sí, utilice una nueva línea para cada evento.

![El panel de eventos que usa la versión de modo de texto.](../images/graph-simulation/text-version.png)

### Editar evento {#edit-event}

Para editar un evento, seleccione los puntos suspensivos (`...`) junto a un evento determinado y, a continuación, seleccione **[!UICONTROL Edit]**.

![Icono de edición de evento seleccionado.](../images/graph-simulation/edit.png)

### Eliminar evento {#delete-event}

Para eliminar un evento, seleccione los puntos suspensivos (`...`) junto a un evento determinado y, a continuación, seleccione **[!UICONTROL Delete]**.

![Icono de evento de eliminación seleccionado.](../images/graph-simulation/delete.png)

## Configurar algoritmo {#configure-algorithm}

>[!IMPORTANT]
>
>El algoritmo que configure dicta cómo el servicio de identidad trata las áreas de nombres introducidas en los eventos. Las configuraciones que haya creado en [!DNL Graph Simulation UI] no se guardarán en la configuración de identidad.

Una vez añadidos los eventos, se puede configurar el algoritmo que se utilizará para simular el gráfico. Para empezar, seleccione **[!UICONTROL Add config]**.

![Panel de configuración del algoritmo.](../images/graph-simulation/add-config.png)

Aparece una fila de configuración vacía. En primer lugar, escriba el mismo espacio de nombres que utilizó para los eventos. En este caso, comience introduciendo el correo electrónico. Una vez que especifique su espacio de nombres, las columnas de [!UICONTROL Identity Symbol] y [!UICONTROL Identity Type] se rellenan automáticamente.

![La primera entrada de configuración.](../images/graph-simulation/add-namespace.png)

Siguiente, repita los mismos pasos y añada su segunda área de nombres, que en este caso es el ECID. Una vez introducidos todos los espacios de nombres, puede empezar a configurar sus prioridades y su carácter único.

* **Prioridad de área de nombres**: La prioridad de un área de nombres determina su importancia relativa en comparación con las otras áreas de nombres de un gráfico de identidad determinado. Por ejemplo, si el gráfico de identidad tiene cuatro áreas de nombres diferentes: CRMID, ECID, Correo electrónico y Apple IDFA, puede configurar prioridades para determinar un orden de importancia para las cuatro áreas de nombres.
* **Área de nombres única**: Si se designa un área de nombres como única, el Servicio de identidad generará gráficos con la advertencia de que solo puede existir una identidad con un área de nombres única. Por ejemplo, si el área de nombres de correo electrónico está designada como un área de nombres única, un gráfico solo puede tener una identidad con el correo electrónico. Si hay más de una identidad con el área de nombres de correo electrónico, se eliminará el vínculo más antiguo.

Para configurar la prioridad del área de nombres, seleccione y arrastre las filas de área de nombres al orden de prioridad que desee, donde la fila superior representa la prioridad superior y la fila inferior representa la prioridad inferior. Para designar un área de nombres como única, active la casilla de verificación **[!UICONTROL Unique Per Graph]**.

Cuando termine, seleccione **[!UICONTROL Simulate]**.

![Todas las áreas de nombres configuradas.](../images/graph-simulation/all-namespaces.png)

## Ver gráfico simulado

La sección [!UICONTROL Simulated Graph] muestra los gráficos de identidad generados en función de los eventos agregados y el algoritmo configurado.

| Iconos de gráficos | Descripción |
| --- | --- |
| Línea continua | Una línea sólida representa un vínculo establecido entre dos identidades. |
| Línea de puntos | Una línea discontinua representa una vincular eliminada entre dos identidades. |
| Número en línea | Un número en una línea representa la marca de tiempo de cuándo se generó ese vincular dado. El número más bajo (1), representa el vínculo establecido más antiguo. |

En el gráfico de ejemplo siguiente, existe una línea de puntos entre `{Email: tom@acme.com}` y `{ECID: 111}` debido a las siguientes razones:

* El correo electrónico se ha designado como único durante el paso de configuración del algoritmo. Por lo tanto, solo puede existir una identidad con un área de nombres de correo electrónico en un gráfico.
* El vínculo entre `{Email: tom@acme.com}` y `{ECID: 111}` fue la primera identidad establecida (#1 de evento). Es el vínculo más antiguo y, por lo tanto, se elimina.

![Panel del visor de gráficos simulado, con un ejemplo de gráfico simulado.](../images/graph-simulation/simulated-graph.png)

## Próximos pasos

Al leer este documento, ahora sabe cómo usar la herramienta [!DNL Graph Simulation] para comprender mejor cómo se tratan los datos de identidad según un conjunto determinado de reglas y configuraciones. Para obtener más información, lea los siguientes documentos:

* [Información general de [!DNL Identity Graph Linking Rules]](./overview.md)
* [Algoritmo de optimización de identidad](./identity-optimization-algorithm.md)
* [guía de implementación](./implementation-guide.md)
* [Solución de problemas y preguntas más frecuentes](./troubleshooting.md)
* [Ejemplos de configuraciones de gráficos](./example-configurations.md)
* [Prioridad del espacio de nombres](./namespace-priority.md)
* [Configuración de identidad IU](./identity-settings-ui.md)
