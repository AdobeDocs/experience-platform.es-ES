---
solution: Experience Platform
title: Aprenda a crear y compartir sus propios libros de reproducción con el asistente de IA.
description: Cómo crear y compartir sus propios libros de casos de uso.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: f76db5c8d397c6c7b006c70147c054dc0a67be04
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# Cree y comparta sus propios libros de reproducción

[!DNL Playbook Authoring Framework], con tecnología de Asistente de IA en Adobe Experience Platform, le permite crear, administrar y compartir libros de reproducción de forma eficaz dentro de Adobe Experience Platform.

El marco de trabajo sigue un proceso de tres pasos:

1. **Captura de metadatos**: use el Asistente para IA o el [formulario web] para capturar metadatos del manual de implementación.

2. **Asociación técnica**: agregue recursos técnicos específicos, como recorridos o audiencias, al libro de reproducción. Puede mantener un control total sobre el proceso de creación del libro de estrategias dentro del entorno limitado de desarrollo, lo que garantiza la alineación con los esquemas y otras estructuras de datos únicas.

3. **Distribución de libros de reproducción**: Comparta libros de reproducción entre distintas organizaciones. Por ejemplo, el Centro de Excelencia Martech de ACME en Alemania puede crear un manual &quot;dorado&quot; y distribuirlo a organizaciones regionales en Tailandia, Australia, etc. para ayudar a estandarizar el caso de uso de marketing.

## Crear un libro de estrategias

Puede crear un libro de reproducción de dos formas: mediante el asistente de IA o manualmente. Lea las secciones siguientes para aprender a hacerlo.

### Resumen del manual

Siga estos pasos para crear un manual con el asistente de IA:

En el panel de navegación izquierdo, seleccione **[!UICONTROL Libros de reproducción]**.

![ &quot;Libros de reproducción&quot; resaltados en el panel de navegación izquierdo de la interfaz de usuario.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Seleccione **[!UICONTROL Nuevo libro de estrategias]** y luego seleccione **Generar libro de estrategias con el Asistente de IA**.

![Interfaz de libro de reproducción con la opción &quot;Generar libro de reproducción con el asistente de IA&quot; seleccionada.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

En el campo de solicitud, describa el caso de uso.

**Ejemplo**: &quot;Capte a los clientes de ACME que navegaron por las zapatillas pero no completaron la compra&quot;.

![Interfaz de libro de reproducción con área de formulario web resaltada.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Seleccione **[!UICONTROL Generar]** para crear los metadatos del libro de reproducción.

![Área de solicitud con el botón &quot;Generar&quot; del libro de reproducción resaltado.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Una vez generado, seleccione **[!UICONTROL Editar]** para modificar el título, la descripción y los metadatos generados según sea necesario.

![Libro de reproducción generado con el botón &quot;Editar&quot; resaltado.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Para asegurarse de que los ingenieros de datos tengan todos los detalles necesarios para configurar el caso de uso, rellene la sección **[!UICONTROL Detalles del manual]**. Aunque son opcionales, estos campos ayudan a capturar información clave, lo que facilita la conexión de los componentes técnicos adecuados. Seleccione **[!UICONTROL Editar]** para agregar valores a los siguientes campos:

* **Sector**
* **Público objetivo**
* **Canal de marketing**

![La sección de detalles del libro de reproducción con el botón &quot;Editar&quot; resaltado.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Una vez generados los metadatos, seleccione **[!UICONTROL Editar mapa de recorrido]** para ajustar los pasos del mapa de recorrido según sea necesario.

![Editar el botón de asignación de recorrido.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Edite el mapa de recorrido una vez que capture los metadatos del manual.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

A continuación, proceda a asociar el manual de implementación con los recursos técnicos. Para crear un libro de reproducción manualmente, seleccione **[!UICONTROL Crear libro de reproducción manualmente]**.

![Crear libro de reproducción manualmente](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Aparecerá una plantilla de libro de estrategias en blanco. Rellene detalles como **Título** y **Descripción**. También puede editar el mapa de recorrido para añadir eventos y puntos de contacto según sea necesario.

## Asociar el manual con los recursos técnicos

Independientemente de si crea un libro de reproducción manualmente o con el asistente de IA, debe asociarlo a los activos técnicos necesarios. Vaya a la pestaña **[!UICONTROL Assets técnico]** y seleccione el producto requerido. Para este ejemplo, seleccione **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> En una versión futura se agregará compatibilidad con Real-Time CDP.

![Se resaltaron la ficha &quot;Recursos técnicos&quot; y el botón &quot;Agregar producto requerido&quot;.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Elija **[!UICONTROL Seleccionar un recurso]** para asociar este libro de reproducción con un recorrido como se muestra en la imagen siguiente. A continuación, seleccione **Publicar libro de reproducción** para finalizar el libro de reproducción.

![: botón &quot;Seleccionar recursos&quot; resaltado en la ficha &quot;Recursos técnicos&quot;](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Seleccionar un recorrido](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Una vez publicado, el manual extrae y asocia automáticamente el esquema del recorrido y los detalles de audiencia.

![Libro de reproducción publicado](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Todos los libros de reproducción creados están disponibles en la ficha **Tus libros de reproducción**.

![&quot;Sus libros de reproducción&quot;, ficha](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Puede seleccionar cualquier manual del catálogo para crear instancias que desee reutilizar. Consulte la documentación para [aprender a crear instancias](/help/use-case-playbooks/playbooks/create-share-reuse.md).

La opción ![&quot;Crear instancia&quot; se resaltó en la ficha &quot;Descripción general del manual&quot; una vez que seleccionó un manual.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Una vez publicado un libro de reproducción, no se puede editar. Para realizar cambios, elimine el manual y comience de nuevo.

## Ejemplos de peticiones

El asistente de IA puede procesar varias estructuras de solicitud y extraer detalles clave al tiempo que filtra la información innecesaria. A continuación se muestran algunos ejemplos de mensajes de usuario y cómo el sistema los interpreta:

**Ejemplo 1:**

&quot;Cree una campaña titulada &quot;Complete la apariencia&quot; para aumentar las ventas y el CLV. La campaña anima a los clientes que compraron utensilios de cocina o muebles a completar una compra complementaria mediante recomendaciones y ofertas personalizadas relacionadas con su compra. Primero envíe un mensaje a los clientes con recomendaciones de productos. Si no realiza ninguna compra en un plazo de 7 días, recibe un segundo mensaje con recomendaciones y ofertas de productos. Utilice notificaciones push y correo electrónico para ponerse en contacto con los clientes. Clientes objetivo que hayan realizado una compra en los últimos 7 días en la categoría de utensilios de cocina o muebles y que no hayan sido objetivos en los últimos 30 días. Como parte de la campaña, queremos medir los KPI como los clics (correo electrónico, aplicación, SMS, push), CTR, E-Wallet CTR, AOV Conversion.CLV Revenue, eventos de compra total (en tienda, digital, centro de llamadas).&quot;

![Mensaje de ejemplo 1](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**Ejemplo 2:**

&quot;Nombre del proyecto: Boletín de moda
Antecedentes: (proactivo o solución de problemas): recorrido diseñado para enviar boletines informativos de moda a los clientes de ACME que se hayan suscrito a la comunicación de boletines informativos.
Objetivo: Enviar correos electrónicos de newsletter de moda a los clientes de ACME que se suscribieron para la comunicación.
Detalles promocionales: El cliente recibe noticias de moda en el canal de correo electrónico semanalmente. El correo electrónico debe ser personalizado y las variaciones de contenido deben basarse en el género, el idioma y el mercado.
Canales/puntos de contacto del proyecto: correo electrónico
Destinatarios objetivo: Clientes que se han suscrito a las comunicaciones del boletín de moda ACME.
KPI de objetivo/métricas de participación/ROI: 1. Aumentar los ingresos de productos. 2. Impulse la lealtad del cliente&quot;.

![Mensaje de ejemplo 2](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**Ejemplo 3:**

&quot;Empuje a los compradores a comprar productos durante una campaña promocional de productos en curso.
Interactúe con los compradores durante una promoción continua enviando comunicaciones adecuadas por correo electrónico, SMS o notificaciones push para comprar productos. Envíeles un correo electrónico recordatorio después de 24 horas de que no participen en la promoción&quot;.

![Ejemplo 3 ](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**Ejemplo 4:**

&quot;Vende zapatos a jugadores de secundaria&quot;.

![Ejemplo 4 ](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

El asistente de IA elimina todos los detalles innecesarios, como el nombre del proyecto o el fondo. Extrae los elementos clave como la &quot;audiencia de destino&quot;, el &quot;objetivo de campaña&quot; y el &quot;canal de marketing&quot; y funciona con cualquier estilo de entrada.

Estos ejemplos muestran cómo la IA puede refinar y extraer detalles esenciales de las indicaciones del usuario.

>[!NOTE]
>
> Evite PII o palabras explícitas al escribir sus mensajes.

## Directrices y moderación de contenido

Al crear libros de reproducción, tenga en cuenta el idioma y el contenido que incluye. Los libros de reproducción son visibles en toda la organización y los usuarios pueden marcar cualquier contenido ofensivo o inapropiado.

### Proceso de indicación y revisión

Si un libro de reproducción está marcado por contenido inapropiado u ofensivo, se comunica automáticamente a Adobe para su revisión. A continuación, Adobe revisa el contenido marcado y, si se considera inapropiado, se notifica al cliente y se elimina el manual.

## Pasos siguientes

Ahora que sabe cómo crear y publicar libros de reproducción con el Asistente de IA, aprenda a empezar con los libros de reproducción disponibles y elija el adecuado para su caso de uso en [Lista de libros de reproducción](/help/use-case-playbooks/playbooks/choose.md).
