---
solution: Experience Platform
title: Creación, uso compartido y reutilización de instancias de libros de reproducción
description: Aprenda a crear, compartir y reutilizar instancias del manual para lograr su caso práctico de marketing.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 51e4a77472ccb560dbfa5f56011ce50932d87b64
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# (Beta) Crear, compartir y reutilizar instancias del manual

>[!AVAILABILITY]
>
>Actualmente, esta funcionalidad está en versión beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para usar un manual de implementación, vaya a **[!UICONTROL Manuales de casos de uso] > [!UICONTROL Manuales]**. Examine y utilice las distintas opciones de búsqueda y filtrado de la página para seleccionar y empezar a utilizar un manual específico.

## Creación de una instancia de libro de estrategias {#create-playbook-instance}

Antes de crear una instancia de libro de reproducción, explore los libros de reproducción disponibles para [descubra el manual adecuado para usted](/help/use-case-playbooks/playbooks/discover.md). Cuando esté listo para continuar con una guía de reproducción y crear una instancia, seleccione **[!UICONTROL Crear instancia]** para continuar con el manual y generar recursos técnicos.

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

Al leer esta guía y la de descubrir el manual adecuado para usted, ahora sabe interpretar las distintas secciones de un manual y cómo utilizar los recursos que se generan después de crear una instancia de un manual.

A continuación, puede examinar el catálogo de libros de reproducción para encontrar el libro de reproducción adecuado para su caso de uso y leer el [guía de solución de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) si tiene algún problema.