---
solution: Experience Platform
title: Guía de IU de Playbooks
description: Aprenda a utilizar la interfaz de usuario de Experience Platform para ver y habilitar libros de reproducción.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 2%

---


# (Beta) Cómo habilitar y reutilizar un manual de implementación

>[!AVAILABILITY]
>
>Actualmente, esta funcionalidad está en versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para usar un manual de implementación, vaya a **[!UICONTROL Manuales de casos de uso] > [!UICONTROL Manuales]**. Examine y utilice las distintas opciones de búsqueda y filtrado de la página para seleccionar y empezar a utilizar un manual específico.

## Búsqueda y filtrado {#search-and-filter}

Utilice la ventana de búsqueda y los filtros disponibles en la página para encontrar el manual adecuado para su caso de uso.

Por ejemplo, puede filtrar libros de reproducción que puede utilizar en función del escenario del canal de marketing al que desee destinar: conversión, participación o retención. También puede filtrar los libros de reproducción mostrados según el sector en el que se encuentre o la asignación de derechos de producto a la que tenga acceso: Adobe Journey Optimizer o Real-time CDP.

![Filtrar libros de reproducción por canal de marketing, sector o producto](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

También puede utilizar la funcionalidad de búsqueda para encontrar el manual de instrucciones adecuado para usted. Vea a continuación un ejemplo de cómo encontrar un manual que le ayude a interactuar con usuarios que pueden haber abandonado el carro de compras.

![Interactúe con usuarios que puedan haber abandonado el carro de compras.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

O bien, puede filtrar los libros de reproducción disponibles por los canales que planea utilizar para llegar a sus clientes, como puede ver a continuación:

![Filtrar por canal](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Experimente con los filtros y la opción de búsqueda y encuentre el manual de instrucciones adecuado para usted.

## Ver libro de reproducción y generar recursos {#view-playbook-generate-assets}

Antes de establecer un libro de estrategias y crear instancias de él, debe inspeccionarlo para asegurarse de que se ajuste a sus necesidades. Para ayudarle a comprender mejor los casos de uso que abarcan, todos los libros de reproducción contienen las secciones que se enumeran a continuación. Cuando esté listo para continuar y generar recursos, seleccione **[!UICONTROL Crear instancia]**.

### Diagrama De Ideas {#mindmap}

Utilice la sección de diagrama de ideas de un manual para comprender los pasos del flujo de trabajo que el manual puede ayudarle a resolver. Visualice el flujo de cómo todos los objetos generados pueden ayudarle a lograr el caso de uso, desde la perspectiva de la persona objetivo en el caso de uso.

El diagrama de ideas comienza con una definición de a quién se llega en el recorrido del usuario y describe en cada paso si algo se entrega por Adobe, como un nuevo mensaje o un recordatorio, o si es algo que la persona objetivo hizo que déclencheur el siguiente mensaje o evento.

![Mapa mental del libro de estrategias resaltado.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Resumen {#summary}

Inspect usa la sección de resumen para comprender qué recursos se generan una vez que se crean instancias a partir del manual. Los recursos que se generan para cada manual de implementación se adaptan al caso de uso que habilita el manual de implementación. A continuación, obtendrá más información sobre todos los elementos de la sección Resumen.

| Elemento | Descripción |
---------|----------|
| **[!UICONTROL Audiencia objetivo]** | Describe las personas a las que quiere llegar a través de este manual de casos de uso. |
| **[!UICONTROL Canales de marketing]** | Describe los canales utilizados para llegar a las personas segmentadas en el manual de implementación. |
| **[!UICONTROL Activos técnicos]** | Una lista de los recursos técnicos que se generan después de crear instancias del libro de reproducción. Los recursos generados difieren según el manual de implementación, según el caso de uso. Algunos libros de reproducción pueden generar esquemas, segmentos y recorridos. Otros pueden generar destinos. Consulte la [Explicación de los recursos generados](#understand-assets) Consulte la sección siguiente para obtener más información sobre cómo utilizar y reutilizar los recursos generados. |

{style="table-layout:auto"}

![Resumen del manual resaltado](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instancias {#instances}

Desplácese hacia abajo hasta la sección de instancias para obtener una descripción general de las instancias de este manual que usted o los miembros de su equipo ya han creado. Puede utilizar varios controles para ordenar y filtrar las instancias mostradas; por ejemplo, para ver solo las creadas por usted. También puede ver información diversa sobre cada instancia, como se muestra a continuación.

| Elemento | Descripción |
|---------|----------|
| **[!UICONTROL Nombre]** | Nombre de la instancia basado en el manual de implementación. Puede personalizar el nombre y la descripción de una instancia. Lea la sección siguiente sobre [cómo editar metadatos de instancia](#edit-instance-metadata) para obtener más información. |
| **[!UICONTROL Estado]** | Indica el estado de la instancia. A **[!UICONTROL enviado]** La instancia está lista para su uso. |
| **[!UICONTROL Creado]** | Indica cuándo se creó la instancia. |
| **[!UICONTROL Creado por]** | Indica quién creó la instancia. |
| **[!UICONTROL Última modificación]** | Indica la última modificación de la instancia. |

{style="table-layout:auto"}

![Instancia de libro de estrategias resaltada.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Habilitar el manual {#enable-playbook}

Cuando esté listo para continuar con una guía de reproducción y crear una instancia, seleccione **[!UICONTROL Crear instancia]** para continuar con el manual y generar recursos técnicos.

![Cree una instancia de un manual de implementación.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Esta acción genera varios recursos que puede utilizar para lograr el caso de uso descrito en el manual de implementación.

![Vista del manual de los recursos generados después de habilitarse.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilice los controles de configuración para editar los nombres y las descripciones de las instancias {#edit-instance-metadata}

Después de crear una instancia basada en un libro de reproducción, puede personalizarla para distinguirla de otras instancias creadas a partir del mismo libro de reproducción. Seleccione el control de configuración como se muestra a continuación. Edite el nombre, la descripción y las notas y seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![Editar el nombre y la descripción de una instancia.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Explicación de los recursos generados {#understand-assets}

>[!IMPORTANT]
>
>¡No hay necesidad de preocuparse! Este es un espacio seguro para experimentar y no se puede romper nada. Aún no hay datos asociados a ninguno de los recursos que cree. Primero debe introducir los datos para lograr los casos de uso.

Es importante comprender que los recursos generados difieren según el caso de uso que active:

* Se generan diferentes recursos para diferentes tipos de libros de reproducción. Estos recursos se crean específicamente para el caso de uso conseguido mediante el manual de implementación. Por ejemplo, un manual genera un esquema, un segmento, un recorrido y mensajes. Otro manual genera un esquema, un segmento y un destino para activar los datos.
* Los recursos en sí difieren entre libros de reproducción. Por ejemplo, para **[!UICONTROL Enviar Un Mensaje De Cumpleaños A Los Invitados]** manual, la audiencia que se crea tiene la regla `birthday=today AND year=any`.

Para ilustrar un ejemplo, consulte **[!UICONTROL Carro abandonado: mercancía]** manual, puede ver que se crea un recorrido específico que incluye los mensajes creados para este caso de uso.

![Recorrido creado a partir del manual de casos de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Uso y edición de los recursos generados {#use-and-edit-assets}

A medida que explora los recursos que se generan después de crear una instancia de un libro de reproducción, puede editar cualquiera de los recursos creados.

Si usted o alguien de su equipo crea otra instancia del manual, los recursos editados se conservan y se crean nuevos recursos para la nueva instancia del manual.

El comportamiento descrito anteriormente es verdadero para todos los recursos que se crean, excepto para los esquemas. En el caso de los esquemas, no se crean nuevos esquemas cuando se crea una nueva instancia de un libro de reproducción, por lo que utilizará el esquema editado de otra instancia del libro de reproducción en la instancia recién creada.

>[!TIP]
>
>Realice pruebas en el entorno limitado de desarrollo y pase a la producción cuando esté listo.
>
>Una vez generados los objetos, puede seguir probando en los entornos limitados de desarrollo añadiendo datos. Puede probar los recursos todo el tiempo que desee en el entorno limitado de desarrollo y duplicar la lógica de recursos (definiciones de segmentos, recorridos, esquemas, etc.) en el entorno limitado de producción cuando esté listo.

### Reutilizar libros de reproducción {#reuse-playbooks}

Al crear varias instancias del mismo manual, puede implementar el mismo caso de uso más adelante, sin modificar los detalles de la implementación anterior del caso de uso.

### Compartir el manual y los recursos generados con otros integrantes del equipo {#share-playbook}

Puede compartir la instancia y los recursos generados con otros integrantes del equipo. Para ello, copie el vínculo URL del explorador y compártalo con su equipo para darles una visión general de los recursos generados.

![URL resaltada en una vista del manual de casos de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Pasos siguientes {#next-steps}

Al leer esta guía de la interfaz de usuario, ahora sabe cómo interpretar las distintas secciones de un libro de reproducción y cómo utilizar los recursos que se generan después de crear una instancia de un libro de reproducción. A continuación, puede examinar el catálogo de libros de reproducción para encontrar el libro de reproducción adecuado para su caso de uso y leer la guía de solución de problemas si encuentra algún error.