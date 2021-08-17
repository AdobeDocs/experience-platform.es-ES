---
title: Reglas
description: Descubra cómo funcionan las extensiones de etiquetas en Adobe Experience Platform.
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '1977'
ht-degree: 82%

---

# Reglas

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las etiquetas de Adobe Experience Platform siguen un sistema basado en reglas. Buscan interacción de usuarios y datos asociados. Cuando se cumplen los criterios descritos en las reglas, la regla activa la extensión, script o el código del lado del cliente identificados.

Genere reglas para integrar los datos y las funciones de marketing y tecnología publicitaria que unifique productos dispares en una única solución.

## Estructura de reglas

**Eventos (If):** el evento es lo que desea que busque la regla. Se define seleccionando un evento, cualquier condición aplicable y cualquier excepción.

**Acciones (Then):** las activaciones se producen cuando se producen eventos de una regla y se cumplen todas las condiciones. Una regla de déclencheur puede realizar tantas acciones discretas como desee y puede controlar el orden en que se producen estas acciones. Por ejemplo, una única regla para una página de agradecimiento de comercio electrónico puede activar las herramientas de análisis y las etiquetas de terceros desde una única regla. No es necesario crear reglas independientes para cada herramienta o etiqueta.

Puede añadir más tipos de eventos. Los eventos múltiples se unen con un operador OR, por lo que las condiciones de la regla se evalúan si se cumplen algunos de los eventos.

>[!IMPORTANT]
>
>Los cambios no surtirán efecto hasta [que se publiquen](../publishing/overview.md).

### Eventos y condiciones (If)

Los eventos con cualquier condición son la porción *If* de una regla.

Si se produce un evento específico, se evalúan las condiciones y las acciones especificadas se realizan en caso necesario.

* **Eventos**: Especifique uno o más eventos que deben llevarse a cabo para almacenar en déclencheur la regla. Los eventos múltiples se unen mediante un operador OR. Cualquiera de los eventos especificados activa la regla.

* **Condiciones**: Reduzca el evento configurando cualquier condición que deba ser verdadera para que un evento pueda almacenar en déclencheur la regla. Una excepción se define como una condición NOT. Las condiciones múltiples se unen mediante un operador AND.

Los eventos disponibles dependen de las extensiones instaladas. Para obtener más información sobre los eventos de la extensión principal, consulte [Tipos de eventos de la extensión principal](../../extensions/web/core/overview.md#core-extension-event-types).

### Acciones (Then)

Las acciones son la porción *Then* de una regla. Definen lo que desea que ocurra cuando se ejecute la regla. Cuando se activa un evento, si las condiciones se evalúan como “true” y las excepciones como “false”, se realizan las acciones. Puede arrastrar y soltar acciones para ordenarlas según lo desee.

## Creación de reglas

Cree una regla que especifique qué acciones se producen si se cumple una condición.

1. Abra la pestaña [!UICONTROL Reglas] y seleccione **[!UICONTROL Crear nueva regla]**.

   ![](../../images/launch-rule-builder.jpg)

1. Asigne un nombre a la regla.
1. Seleccione el icono de eventos **[!UICONTROL Añadir]**.
1. Seleccione la extensión y uno de los tipos de evento disponibles para esa extensión y, a continuación, configure los ajustes del evento.

   ![](../../images/rule-event-config.png)

   Los tipos de evento disponibles dependen de la extensión seleccionada. La configuración del evento será diferente según el tipo de evento. Algunos eventos no tienen ajustes que se deban configurar.

   >[!IMPORTANT]
   >
   >En una regla del lado del cliente, los elementos de datos se identifican mediante token con el símbolo `%` al principio y al final del nombre del elemento de datos. Por ejemplo, `%viewportHeight%`. En una regla de reenvío de eventos, los elementos de datos reciben el token `{{` al principio y `}}` al final del nombre del elemento de datos. Por ejemplo, `{{viewportHeight}}`.

   Para hacer referencia a datos de Edge Network, la ruta del elemento de datos debe ser `arc.event._<element>_`.

   `arc` significa contexto de respuesta de Adobe.

   Por ejemplo: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Si esta ruta de acceso no se especifica correctamente, no se recopilarán datos.

1. Establezca el parámetro Pedido y, a continuación, seleccione **[!UICONTROL Conservar cambios]**.

   El orden predeterminado para todos los componentes de la regla es 50. Si desea que uno se ejecute antes, asígnele un número inferior a 50.

   * El orden de ejecución es el orden de los números. 1 va antes que 3. 3 va antes que 10. 10 va antes que 100, etc.
   * Las reglas con el mismo orden se ejecutan sin ningún orden en particular.
   * Las reglas se activan en orden, pero no necesariamente finalizan en el mismo orden. Si la Regla A y la Regla B comparten un evento y usted asigna el orden para que la Regla A se ejecute primero, si la Regla A hace algo de forma asíncrona, la Regla A termina antes de que la Regla B comience.

      Si desea que se ejecute más tarde, asígnele un número superior a 50. Para obtener más información sobre la ordenación, consulte [Ordenación de reglas](rules.md#rule-ordering).

1. Seleccione el icono de Condiciones **[!UICONTROL Añadir]** y, a continuación, seleccione un tipo de lógica, una extensión y un tipo de condición, y configure los ajustes de la condición. A continuación, seleccione **[!UICONTROL Conservar cambios]**.

   ![](../../images/condition-settings.png)

   Los tipos de condiciones disponibles dependen de la extensión seleccionada. La configuración de la condición será diferente según el tipo de condición.

   Tipo de lógica:

   * El tipo de lógica regular permite ejecutar acciones si se cumple la condición
   * El tipo de lógica de excepción evita que se ejecuten las acciones si se cumple la condición

   Tiempo de espera (avanzado): esta opción está disponible cuando la secuenciación de componentes de regla está habilitada en la propiedad. Este atributo define la cantidad máxima de tiempo permitida para que se ejecute la condición. Si se alcanza el tiempo de espera, la condición falla y el resto de las condiciones y acciones de la regla se eliminarán de la cola de procesamiento. El valor predeterminado es 2000 ms.

   Puede agregar tantas condiciones como desee. Varias condiciones en la misma regla se unen mediante AND.

1. Seleccione el icono de Acciones **[!UICONTROL Añadir]** y, a continuación, seleccione la extensión y uno de los tipos de acción disponibles para dicha extensión. Configure los ajustes de la acción y, a continuación, seleccione **[!UICONTROL Conservar cambios]**.

   ![](../../images/action-settings.png)

   Los tipos de acciones disponibles dependen de la extensión seleccionada. Los ajustes de la acción diferirán según el tipo de acción.

   (Avanzado) Espere a ejecutar la siguiente acción: esta opción está disponible cuando la secuenciación de componentes de regla está habilitada en la propiedad. Cuando está activado, las etiquetas no llaman a la siguiente acción hasta que esta se complete. Cuando está desactivada, la siguiente acción empieza a ejecutarse de inmediato. El valor predeterminado es **[!UICONTROL Activado]**.

   Tiempo de espera (avanzado): esta opción está disponible cuando la secuenciación de componentes de regla está habilitada en la propiedad. Define la cantidad máxima de tiempo permitida para que se complete la acción. Si se alcanza el tiempo de espera, la acción falla y las acciones posteriores de esta regla se eliminarán de la cola de procesamiento. El valor predeterminado es 2000 ms.


1. Revise la regla y seleccione **[!UICONTROL Guardar regla]**.

   Posteriormente, en el momento de la [publicación](../publishing/overview.md), debe añadir esta regla a una biblioteca e implementarla.

Al crear o editar reglas, puede guardar y compilar en su [biblioteca activa](../publishing/libraries.md#active-library). Esto guarda inmediatamente el cambio en la biblioteca y ejecuta una compilación. Se muestra el estado de la compilación.

## Ordenación de reglas {#rule-ordering}

La ordenación de reglas permite controlar el orden de ejecución de las reglas que comparten un evento.

Suele ser importante que las reglas se activen en un orden específico. Ejemplos: (1) tiene varias reglas que establecen condicionalmente las variables [!DNL Analytics] y debe asegurarse de que la regla con Send Beacon se ejecute la última. (2) tiene una regla que activa [!DNL Target] y otra regla que activa [!DNL Analytics], y desea que la regla de [!DNL Target] se ejecute primero.

Finalmente, la responsabilidad de ejecutar las acciones en orden recae en el desarrollador de la extensión del tipo de evento que está utilizando. Los desarrolladores de extensiones de Adobe se aseguran de que sus extensiones funcionan según lo previsto. En el caso de las extensiones de terceros, Adobe proporciona directrices a los desarrolladores de extensiones para que implementen esto correctamente, pero depende de ellos hacerlo correctamente.

Adobe recomienda encarecidamente que ordene las reglas con números positivos entre 1 y 100 (el valor predeterminado es 50). Al ser más sencillo resulta mejor. Recuerde que debe mantener su orden. Sin embargo, el Adobe reconoce que puede haber casos excepcionales en los que esto parezca restrictivo, por lo que se permiten otros números. Las etiquetas admiten números entre +/- 2.147.483.648. También puede utilizar aproximadamente una docena de cifras decimales, pero si considera que necesita hacerlo en su situación actual, debe reconsiderar algunas de las decisiones que ha tomado para llegar a dicha situación.

>[!IMPORTANT]
>
>En la sección Acción de una regla, las reglas del lado del servidor se ejecutan secuencialmente. Asegúrese de que el pedido sea correcto cuando cree la regla.

### Situaciones

* Cinco reglas comparten un evento. Todas tienen prioridad predeterminada. Quiero que una de ellas se ejecute la última. Solo necesito editar ese componente de regla y darle un número superior a 50 (por ejemplo, 60).
* Cinco reglas comparten un evento. Todas tienen prioridad predeterminada. Quiero que una de ellas se ejecute primero. Solo necesito editar ese componente de regla y darle un número inferior a 50 (por ejemplo, 40).

### Administración de reglas del lado del cliente

El orden de carga de las reglas depende de si la acción de regla está configurada con JavaScript, HTML u otro código del lado del cliente, y si las reglas utilizan un evento de final o principio de página o un tipo de evento diferente.

Puede usar `document.write` en los scripts personalizados independientemente de los eventos configurados para la regla.

Puede ordenar distintos tipos de código personalizado combinándolos entre sí. Por ejemplo, puede tener una acción de código personalizado de JavaScript, luego una acción de código personalizado HTML y luego otra acción de código personalizado de JavaScript. Las etiquetas garantizan que se ejecuten en ese orden.

## Agrupación de reglas

Los eventos y las condiciones de las reglas siempre se incluyen en la biblioteca de etiquetas principal. Las acciones pueden agruparse en la biblioteca principal o cargarse tarde como recursos secundarios según sea necesario. El tipo de evento de la regla determina si las acciones están agrupadas o no.

### Reglas con eventos &quot;Principal: biblioteca cargada&quot; o &quot;Principal: parte superior de la página&quot;

Estos eventos deben ejecutarse casi siempre (a menos que las condiciones se evalúen como false). Por lo tanto, para que sean más eficaces, se incluye el archivo al que hace referencia el código incrustado en la biblioteca principal.

* **JavaScript:** JavaScript está incrustado en la biblioteca de etiquetas principal. El script personalizado se coloca dentro de una etiqueta script y se escribe en el documento mediante `document.write`. Si la regla tiene varios scripts personalizados, se escriben en orden.

   >[!NOTE]
   >
   >Las etiquetas utilizan JavaScript ES5. El reenvío de eventos utiliza ES6.

* **HTML:** el HTML se incrusta en la biblioteca de etiquetas principal. `document.write` se utiliza para escribir el HTML en el documento. Si la regla tiene varios scripts personalizados, se escriben en orden.

### Reglas con cualquier otro evento

Adobe no puede garantizar que se activen otras reglas y que se necesite el código de acción. Por este motivo, las acciones de todos los tipos de evento que no se han enumerado anteriormente no se empaquetan en la biblioteca principal. En su lugar, se almacenan como subrecursos, y la biblioteca principal hace referencia a ellos según sea necesario.

* **JavaScript:** JavaScript se carga desde el servidor como texto normal, dentro de una etiqueta script, y se añade al documento mediante Postscribe. Si la regla tiene varios scripts personalizados de JavaScript, estos se cargan en paralelo desde el servidor, pero se ejecutan en el mismo orden configurado en la regla.
* **HTML:** el HTML se carga desde el servidor y se añade al documento mediante Postscribe. Si la regla tiene varios scripts personalizados de HTML, estos se cargan en paralelo desde el servidor, pero se ejecutan en el mismo orden configurado en la regla.

## Secuencia de componentes de regla {#sequencing}

El comportamiento del entorno de tiempo de ejecución de etiquetas depende de si **[!UICONTROL Run rule components in sequence]** está activado o desactivado para la propiedad.

### Habilitado

Si se habilita, cuando se activa un evento en tiempo de ejecución, las condiciones y acciones de la regla se agregan a una cola de procesamiento (según el orden definido) y se procesan de uno en uno según FIFO. La etiqueta espera a que finalice el componente antes de pasar al siguiente.

Si una condición se evalúa como falsa o alcanza el tiempo de espera definido, las siguientes condiciones y acciones de esa regla se eliminan de la cola.

Si una acción falla o alcanza el tiempo de espera definido, las acciones posteriores de esa regla se eliminan de la cola.

>[!NOTE]
>
>Con esta configuración habilitada, todas las condiciones y acciones se ejecutan de forma asíncrona, incluso si se ha cargado la biblioteca de etiquetas de forma sincrónica.

### Desactivado

Si está desactivado, cuando se activa un evento en tiempo de ejecución, las condiciones de la regla se evalúan de inmediato. Las condiciones múltiples se evalúan en paralelo.

Si todas las condiciones arrojan true (y las excepciones arrojan false), las acciones de la regla se ejecutan de inmediato. Las acciones se llaman en orden, pero las etiquetas no esperan a que una se complete antes de llamar a la siguiente. Si las acciones son sincrónicas, se siguen ejecutando en orden. Si una o más acciones son asincrónicas, algunas acciones se ejecutarán en paralelo.
