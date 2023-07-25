---
solution: Experience Platform
title: Creación, uso compartido y reutilización de instancias de manuales de tácticas
description: Aprenda a crear, compartir y reutilizar instancias del manual de tácticas para lograr su caso de uso de marketing.
badgeBeta: label="Beta" type="Informative"
source-git-commit: e61e200b148e4d17041b3711bd63c796a44b05c8
workflow-type: ht
source-wordcount: '724'
ht-degree: 100%

---


# (Beta) Creación, uso compartido y reutilización de instancias de manuales de tácticas

>[!AVAILABILITY]
>
>Actualmente, esta funcionalidad está en versión beta y no está disponible para todos los usuarios. La documentación y las funcionalidades están sujetas a cambios.

Para usar el manual de tácticas, vaya a **[!UICONTROL Casos de uso de manuales de tácticas] > [!UICONTROL Manuales de tácticas]**. Examine y utilice las distintas opciones de búsqueda y filtrado de la página para seleccionar y utilizar un manual de tácticas específico.

## Creación de una instancia de manual de tácticas {#create-playbook-instance}

Antes de crear una instancia de manual de tácticas, explore los disponibles y [descubra el adecuado para usted](/help/use-case-playbooks/playbooks/discover.md). Cuando esté listo para continuar con un manual de tácticas y crear una instancia, seleccione **[!UICONTROL Crear instancia]** para proseguir y generar recursos técnicos.

![Cree una instancia de un manual de tácticas.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Esta acción genera varios recursos que puede utilizar para lograr el caso de uso descrito en el manual de tácticas.

![Vista del manual de tácticas de los recursos generados después de habilitarse.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Uso de los controles de configuración para editar los nombres y las descripciones de las instancias {#edit-instance-metadata}

Después de crear una instancia basada en un manual de tácticas, puede personalizarla para distinguirla de otras instancias creadas a partir del mismo manual de tácticas. Seleccione el control de configuración como se muestra a continuación. Edite el nombre, la descripción y las notas y seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![Edite el nombre y la descripción de una instancia.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Explicación de los recursos generados {#understand-assets}

>[!IMPORTANT]
>
>No hay necesidad de preocuparse. Este es un espacio seguro para experimentar y no se puede romper nada. Aún no hay datos asociados a ninguno de los recursos que cree. Primero debe introducir los datos para lograr los casos de uso.

Es importante comprender que los recursos generados difieren según el caso de uso que active:

* Se generan diferentes recursos para diferentes tipos de manuales de tácticas. Estos recursos se crean específicamente para el caso de uso conseguido mediante el manual de tácticas. Por ejemplo, un manual de tácticas genera un esquema, un segmento, un recorrido y mensajes. Otro manual de tácticas genera un esquema, un segmento y un destino para activar los datos.
* Los recursos en sí difieren entre los libros de reproducción. Por ejemplo, para el manual de tácticas **[!UICONTROL Enviar un mensaje de cumpleaños a los invitados]**, la audiencia que se crea tiene la regla `birthday=today AND year=any`.

Para ilustrar un ejemplo, consulte el manual de tácticas **[!UICONTROL Carro de compras abandonado: mercancía]**, puede ver que se crea un recorrido específico que incluye los mensajes creados para este caso de uso.

![Recorrido creado a partir del manual de tácticas de casos de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Uso y edición de los recursos generados {#use-and-edit-assets}

A medida que explora los recursos que se generan después de crear una instancia de un manual de tácticas, puede editar cualquiera de los recursos creados.

Si usted o alguien de su equipo crea otra instancia del manual de tácticas, los recursos editados se conservan y se crean nuevos recursos para la nueva instancia del manual de tácticas.

El comportamiento descrito anteriormente es verdadero para todos los recursos que se crean, excepto para los esquemas. En el caso de los esquemas, no se generan nuevos cuando se crea una nueva instancia de un manual de tácticas, por lo que se utiliza el esquema editado de otra instancia del manual de tácticas en la instancia recién creada.

>[!TIP]
>
>Realice pruebas en una zona protegida de desarrollo y pase a la producción cuando termine.
>
>Una vez generados los objetos, puede seguir probando en las zonas protegidas de desarrollo añadiendo datos. Puede probar los recursos todo el tiempo que desee en la zona protegida de desarrollo y duplicar la lógica de recursos (definiciones de segmentos, recorridos, esquemas, etc.) en la zona protegida de producción cuando esté listo.

## Reutilizar manuales de tácticas {#reuse-playbooks}

Al crear varias instancias del mismo manual de tácticas, puede implementar el mismo caso de uso más adelante, sin modificar los detalles de la implementación anterior del caso de uso.

## Compartir el manual de tácticas y los recursos generados con otros integrantes del equipo {#share-playbook}

Puede compartir la instancia y los recursos generados con otros integrantes del equipo. Para ello, copie el vínculo de la URL del explorador y compártalo con su equipo para darle una visión general de los recursos generados.

![URL resaltada en una vista del manual de tácticas del caso de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Pasos siguientes {#next-steps}

Al leer esta guía y la que trata sobre cómo descubrir el manual de tácticas adecuado para usted, ya sabe interpretar las distintas secciones del manual de tácticas y cómo utilizar los recursos que se generan después de crear una instancia del manual de tácticas.

A continuación, puede examinar el catálogo de manuales de tácticas para encontrar el adecuado para su caso de uso y leer la [guía de solución de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) si tiene algún problema.