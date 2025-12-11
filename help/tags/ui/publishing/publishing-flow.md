---
title: Flujo de publicación
description: Conozca el proceso de creación de bibliotecas, realización de pruebas de compilaciones y aprobación para su producción en Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 83%

---

# Flujo de publicación {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Flujo de publicación"
>abstract="Comprenda los niveles de permisos de usuario necesarios para el flujo de publicación, incluidos los derechos de desarrollo, aprobación y publicación."

El flujo de publicación de etiquetas en Adobe Experience Platform hace referencia al proceso de creación de bibliotecas, prueba de compilaciones y aprobación para su producción.

Las acciones disponibles que se pueden realizar con una biblioteca dependen del estado de la biblioteca y del nivel de permiso que tenga. Además, el estado de una biblioteca también afecta a los recursos que contiene (reglas, elementos de datos y extensiones) en función de qué elementos hay en sentido ascendente en el flujo de publicación.

En las siguientes secciones se explican los permisos, el estado de la biblioteca y el flujo ascendente, ya que se refieren al flujo de publicación.

## Permisos {#permissions}

Existen diferentes niveles de permisos de usuario que son importantes para el flujo de publicación; en concreto, los derechos de propiedad [!UICONTROL Develop], [!UICONTROL Approve] y [!UICONTROL Publish]:

* **[!UICONTROL Develop]**: incluye la capacidad de creación de bibliotecas, compilación para desarrollo y presentación para aprobación.
* **[!UICONTROL Approve]**: incluye la capacidad de generar compilaciones de ensayo y aprobar las compilaciones una vez superados los ensayos.
* **[!UICONTROL Publish]**: incluye la capacidad de publicar una biblioteca aprobada.

Estos derechos no son inclusivos. Para que una sola persona realice el flujo de trabajo de principio a fin, se debe otorgar a esa persona los tres derechos dentro de una propiedad determinada.

Consulte la [guía de permisos de usuario](../administration/user-permissions.md) para obtener más información sobre la administración de permisos para etiquetas.

## Estado de la biblioteca {#state}

En cuanto al flujo de publicación, hay cuatro estados básicos en los que puede estar una biblioteca:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Estos cuatro estados se representan como columnas dentro de la pestaña **[!UICONTROL Publishing Flow]**.

![](./images/approval-workflow/flow-ui.png)

Se deben realizar acciones específicas para cambiar de estado una biblioteca. El diagrama siguiente describe todas las acciones que mueven una biblioteca entre los diferentes estados:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Cuando se crean nuevas bibliotecas, comienzan con el estado [!UICONTROL Development]. Los cambios realizados en una biblioteca deben realizarse mientras la biblioteca se encuentra en [!UICONTROL Development]. Cuando se completan las fases de desarrollo y pruebas, la biblioteca se puede enviar para su aprobación.

En la tabla siguiente se describen las acciones disponibles para una biblioteca en el estado [!UICONTROL Development]:

| Acción | Descripción |
| --- | --- |
| [!UICONTROL Edit] | Utilice la pantalla [!UICONTROL Edit Library] para añadir o quitar componentes de la biblioteca. |
| [!UICONTROL Build to Development] | Cree una compilación de la biblioteca. La compilación se genera y se implementa en el entorno al que se asigna la biblioteca. Este paso da error si la biblioteca no se ha asignado a un entorno o si contiene un cambio que ya está definido en el flujo ascendente. |
| [!UICONTROL Submit for Approval] | Cancele la asignación de la biblioteca del entorno de desarrollo y mueva la biblioteca a la columna [!UICONTROL Submitted] para que un usuario con permisos de aprobación pueda gestionarla. La última compilación de la biblioteca debe ser correcta para que esta opción esté habilitada. |
| [!UICONTROL Submit & Build to Staging] | Esto solo lo puede realizar un usuario con derechos de desarrollo y aprobación. Esta acción anula la asignación de la biblioteca del entorno de desarrollo, mueve la biblioteca al estado [!UICONTROL Submitted] y la compila en el entorno de ensayo. La última compilación de la biblioteca debe ser correcta para que esta opción esté habilitada. |
| [!UICONTROL Approve for Publishing] | Esto solo lo puede realizar un usuario con derechos de desarrollo y aprobación. Esta acción anula la asignación de la biblioteca del entorno de desarrollo y la mueve al estado [!UICONTROL Approved], lo que omite el entorno de ensayo y el estado [!UICONTROL Submitted] por completo. La última compilación de la biblioteca debe ser correcta para que esta opción esté habilitada. |
| [!UICONTROL Approve & Publish to Production] | Esto solo lo puede realizar un usuario con derechos de desarrollo, aprobación y publicación. Esta acción anula la asignación de la biblioteca del entorno de desarrollo, la mueve al estado [!UICONTROL Approved] y la publica en producción. Una vez completada la compilación de producción, la biblioteca pasará al estado [!UICONTROL Published]. La última compilación de la biblioteca debe ser correcta para que esta opción esté habilitada. |
| [!UICONTROL Delete] | Elimine la biblioteca del sistema. Esto no quita la compilación del entorno. |

### [!UICONTROL Submitted] {#submitted}

Cuando una biblioteca está en el estado [!UICONTROL Submitted], un usuario con permisos de aprobación puede probar la biblioteca en el entorno de ensayo. Cuando termina la prueba, la biblioteca se aprueba o se rechaza. Las compilaciones rechazadas vuelven a [!UICONTROL Development] para poder realizar los cambios pertinentes antes de reiniciar el flujo de publicación.

En la tabla siguiente se describen las acciones disponibles para una biblioteca en el estado de [!UICONTROL Submitted]:

| Acción | Descripción |
| --- | --- |
| [!UICONTROL Open] | Ver el contenido de la biblioteca. No se permiten cambios en las bibliotecas que no están en la columna [!UICONTROL Development]. Si es necesario realizar cambios, la biblioteca debe rechazarse para que se puedan realizar cambios en [!UICONTROL Development]. |
| [!UICONTROL Build for Staging] | Compile la biblioteca en el entorno de ensayo para su implementación. |
| [!UICONTROL Approve for Publishing] | Mueva la biblioteca a la columna [!UICONTROL Approved] para que un usuario con permisos de publicación pueda gestionarla. |
| [!UICONTROL Approve & Publish to Production] | Esto solo lo puede realizar un usuario con derechos de aprobación y publicación. Esta acción anula la asignación de la biblioteca del entorno de ensayo, la mueve al estado [!UICONTROL Approved] y la publica en producción. Una vez completada la compilación de producción, la biblioteca pasará al estado [!UICONTROL Published]. Esto se puede realizar con una compilación correcta en el entorno de ensayo o sin ella. |
| [!UICONTROL Reject] | Cancele la asignación de la biblioteca del entorno de ensayo y vuelva a moverla a la columna [!UICONTROL Development] para realizar más cambios. |

### [!UICONTROL Approved] {#approved}

Una vez aprobada una biblioteca, un usuario con permisos de publicación podrá publicarla o rechazarla. Las compilaciones rechazadas vuelven a [!UICONTROL Development] para que se puedan realizar los cambios pertinentes antes de que el flujo de publicación se inicie de nuevo.

En la tabla siguiente se describen las acciones disponibles en una biblioteca en el estado [!UICONTROL Approved]:

| Acción | Descripción |
| --- | --- |
| [!UICONTROL Open] | Ver el contenido de la biblioteca. No se permiten cambios en las bibliotecas que no están en la columna [!UICONTROL Development]. Si es necesario realizar cambios, la biblioteca debe rechazarse para que se puedan realizar cambios en [!UICONTROL Development]. |
| [!UICONTROL Build and Publish to Production] | Cancele la asignación de la biblioteca del entorno de ensayo, asigne la biblioteca al entorno de producción e impleméntela.<br><br>**Importante**: cuando se selecciona esta opción, la biblioteca se activa en el entorno de producción. Asegúrese de que la biblioteca contiene los cambios que desea antes de seleccionar esta opción. |
| [!UICONTROL Reject] | Cancele la asignación de la biblioteca del entorno de ensayo y mueva la biblioteca a la columna [!UICONTROL Development] para realizar los cambios pertinentes. |

### [!UICONTROL Published] {#published}

La columna [!UICONTROL Published] muestra qué bibliotecas se publicaron y sus fechas de publicación. La biblioteca publicada actualmente se mostrará con un punto verde junto a ella. A menos que haya realizado una nueva publicación en una biblioteca anterior, esta será siempre la biblioteca situada en la parte superior de la columna.

| Acción | Descripción |
| --- | --- |
| [!UICONTROL Open] | Ver el contenido de la biblioteca. No se permiten cambios en las bibliotecas que no están en la columna [!UICONTROL Development]. Si desea cambiar lo que hay en el entorno de producción, debe crear una nueva biblioteca y moverla a través del proceso de publicación completo. |
| [!UICONTROL Republish] | Esta acción solo está disponible en las cinco bibliotecas publicadas más recientemente y solo si el entorno de producción (A) está configurado con la opción Archivar desactivada y (B) utiliza un host [!UICONTROL Managed by Adobe] en el momento de la compilación. |
| [!UICONTROL Download] | Esta acción solo está disponible en las cinco bibliotecas publicadas más recientemente y solo si el entorno de producción (A) está configurado con la opción Archivar en y (B) utiliza un host [!UICONTROL Managed by Adobe] en el momento de la compilación. |

## Flujo ascendente {#upstream}

Después de publicar su primera biblioteca, es importante comprender el papel del flujo ascendente a medida que mueve bibliotecas más nuevas a través del flujo de publicación.

Si una biblioteca se encuentra actualmente en la fase [!UICONTROL Development], [!UICONTROL Submitted] o [!UICONTROL Approved], esa biblioteca heredará las reglas, los elementos de datos y las extensiones de cualquier biblioteca que esté en el flujo ascendente. Estos recursos heredados constituyen una &quot;línea de base&quot; para cada biblioteca a medida que se desplazan por el flujo de publicación. Básicamente, cada nueva biblioteca podría considerarse simplemente como una serie de cambios que se realizan en la línea de base que establece el flujo ascendente. Esto garantiza que no se sobrescriba por accidente nada de lo que exista en una biblioteca anterior cuando se publique una nueva iteración.

Lo que se incluye en el flujo ascendente depende de la fase actual en que se encuentre la biblioteca. Por ejemplo, las bibliotecas de la columna [!UICONTROL Approved] solo heredan recursos de la biblioteca [!UICONTROL Published], mientras que las bibliotecas de la columna [!UICONTROL Development] heredan los recursos del resto de las columnas.

![](./images/approval-workflow/upstream.png)

Al editar una biblioteca en la IU, todos los recursos heredados del flujo ascendente se representan en la sección **[!UICONTROL Resources Upstream]**. Para ver estos recursos, seleccione la pestaña Expandir debajo del encabezado de la sección.

![](./images/approval-workflow/upstream-collapse.png)

La sección se expande para mostrar los recursos individuales que se heredan del flujo ascendente. Puede utilizar el carril izquierdo para filtrar entre [!UICONTROL Rules], [!UICONTROL Data Elements] y [!UICONTROL Extensions], o bien utilizar la barra de búsqueda para buscar un recurso específico por nombre.

![](./images/approval-workflow/upstream-resources.png)

## Pasos siguientes

En esta guía se proporciona una amplia descripción general del flujo de publicación para bibliotecas en Adobe Experience Platform. Para saber cómo publicar sus bibliotecas, consulte la [información general de publicación](./overview.md).
