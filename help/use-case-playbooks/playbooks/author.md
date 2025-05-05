---
solution: Experience Platform
title: Aprenda a crear y compartir sus propios libros de reproducción con el asistente de IA.
description: Cómo crear y compartir sus propios libros de casos de uso.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# Cree y comparta sus propios libros de reproducción (Beta)

[!DNL Playbook Authoring Framework], con tecnología de Asistente de IA en Adobe Experience Platform, le permite crear, administrar y compartir libros de reproducción de forma eficaz dentro de Adobe Experience Platform.

El marco de trabajo sigue un proceso de tres pasos:

1. **Captura de metadatos**: use el Ayudante de IA o el formulario web para capturar metadatos del manual de implementación.

2. **Asociación técnica**: agregue recursos técnicos específicos, como recorridos o audiencias, al libro de reproducción. Puede mantener un control total sobre el proceso de creación del libro de estrategias dentro del entorno limitado de desarrollo, lo que garantiza la alineación con los esquemas y otras estructuras de datos únicas.

3. **Distribución de libros de reproducción**: Comparta libros de reproducción entre distintas organizaciones. Por ejemplo, el Centro de Excelencia Martech de ACME en Alemania puede crear un manual &quot;dorado&quot; y distribuirlo a organizaciones regionales en Tailandia, Australia, etc. para ayudar a estandarizar el caso de uso de marketing.

## Crear un libro de estrategias

Puede crear un libro de reproducción de dos formas: mediante el asistente de IA o manualmente. Lea las siguientes secciones para aprender a crear un manual con el asistente de IA.

### Resumen del manual

Siga estos pasos para crear un manual con el asistente de IA:

En el panel de navegación izquierdo, seleccione **[!UICONTROL Libros de reproducción]**.

![IU de plataforma con la opción &quot;Libros de reproducción&quot; resaltada en el panel de navegación izquierdo.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Seleccione **[!UICONTROL Nuevo libro de estrategias]** y luego seleccione **Generar libro de estrategias con el Asistente de IA**.

![Interfaz de creación de libros de reproducción que muestra la opción &quot;Generar libro de reproducción con el Asistente de IA&quot; seleccionada.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Utilice el campo de solicitud para describir el caso de uso. Por ejemplo:

&quot;Capte a los clientes de ACME que exploraron las zapatillas de running pero que no completaron la compra&quot;.

![Interfaz de creación de libros de reproducción que resalta el área de formulario web donde los usuarios pueden escribir una solicitud.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Seleccione **[!UICONTROL Generar]** para crear los metadatos del libro de reproducción.

![Interfaz de creación de libros de reproducción que muestra el botón &quot;Generar&quot; resaltado en el área de solicitud.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Una vez generado, seleccione **[!UICONTROL Editar]** para modificar el título, la descripción y los metadatos generados según sea necesario.

![Libro de reproducción generado con el botón &quot;Editar&quot; resaltado, que permite a los usuarios modificar los metadatos.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Para asegurarse de que los ingenieros de datos tengan todos los detalles necesarios para configurar el caso de uso, rellene la sección **[!UICONTROL Detalles del manual]**. Aunque son opcionales, estos campos ayudan a capturar información clave, lo que facilita la conexión de los componentes técnicos adecuados. Seleccione **[!UICONTROL Editar]** para agregar valores a los siguientes campos:

* **Sector**
* **Público objetivo**
* **Canal de marketing**

![La sección de detalles del libro de reproducción con el botón &quot;Editar&quot; resaltado para que pueda agregar o modificar detalles como el sector, la audiencia de destino y el canal de marketing.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Una vez generados los metadatos, seleccione **[!UICONTROL Editar mapa de recorrido]** para ajustar los pasos del mapa de recorrido según sea necesario.

![Botón &quot;Editar mapa de recorrido&quot; para modificar los pasos del mapa de recorrido.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Interfaz del editor de mapas de recorrido para que pueda ajustar los pasos después de capturar los metadatos del libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

A continuación, proceda a asociar el manual de implementación con los recursos técnicos. Para crear un libro de reproducción manualmente, seleccione **[!UICONTROL Crear libro de reproducción manualmente]**.

![La opción &quot;Crear libro de reproducción manualmente&quot; para iniciar un libro de reproducción a partir de una plantilla en blanco.](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Aparecerá una plantilla de libro de estrategias en blanco. Rellene detalles como **Título** y **Descripción**. También puede editar el mapa de recorrido para añadir eventos y puntos de contacto según sea necesario.

## Asociar el manual con los recursos técnicos

Independientemente de si crea un libro de reproducción manualmente o con el asistente de IA, debe asociarlo a los activos técnicos necesarios. Vaya a la pestaña **[!UICONTROL Assets técnico]** y seleccione el producto requerido. Para este ejemplo, seleccione **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> En una versión futura se agregará compatibilidad con Real-Time CDP.

![La ficha &quot;Assets técnico&quot; con el botón &quot;Agregar producto requerido&quot; resaltó que puede usar para asociar recursos técnicos con el libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Elija **[!UICONTROL Seleccionar un recurso]** para asociar este libro de reproducción con un recorrido como se muestra en la imagen siguiente. A continuación, seleccione **Publicar libro de reproducción** para finalizar el libro de reproducción.

![La ficha &quot;Assets técnico&quot; con el botón &quot;Seleccionar recursos&quot; resaltó que puede usar para asociar un recorrido con el libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Seleccione un recorrido para asociarlo a un libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Una vez publicado, el manual extrae y asocia automáticamente el esquema del recorrido y los detalles de audiencia.

![Libro de reproducción publicado que muestra metadatos y recursos técnicos asociados.](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Todos los libros de reproducción creados están disponibles en la ficha **Tus libros de reproducción**.

![: ficha &quot;Sus libros de reproducción&quot; que muestra una lista de los libros de reproducción creados.](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Puede seleccionar cualquier manual del catálogo para crear instancias que desee reutilizar. Consulte la documentación para [aprender a crear instancias](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![La ficha &quot;Información general del libro de estrategias&quot; con la opción &quot;Crear instancia&quot; resaltada.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Una vez publicado un libro de reproducción, no se puede editar. Para realizar cambios, elimine el manual y comience de nuevo.

## Ejemplos de peticiones

El asistente de IA puede procesar varias estructuras de solicitud y extraer detalles clave al tiempo que filtra la información innecesaria. A continuación se muestran algunos ejemplos de indicaciones del usuario y de cómo las interpreta el sistema.

**Ejemplo 1:**

&quot;Cree una campaña titulada &quot;Complete la apariencia&quot; para aumentar las ventas y el CLV. La campaña anima a los clientes que compraron utensilios de cocina o muebles a completar una compra complementaria mediante recomendaciones y ofertas personalizadas relacionadas con su compra. Primero envíe un mensaje a los clientes con recomendaciones de productos. Si no realiza ninguna compra en un plazo de 7 días, recibe un segundo mensaje con recomendaciones y ofertas de productos. Utilice notificaciones push y correo electrónico para ponerse en contacto con los clientes. Clientes objetivo que hayan realizado una compra en los últimos 7 días en la categoría de utensilios de cocina o muebles y que no hayan sido objetivos en los últimos 30 días. Como parte de la campaña, queremos medir los KPI como los clics (correo electrónico, aplicación, sms, push), CTR, E-Wallet CTR, AOV Conversion.CLV Revenue, eventos de compra total (en tienda, digital, centro de llamadas).&quot;

![Ejemplo de un mensaje largo introducido en el cuadro de entrada de texto para generar un libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Ejemplo 2:**

&quot;Nombre del proyecto: Boletín de moda
Antecedentes: (proactivo o solución de problemas): recorrido diseñado para enviar boletines informativos de moda a los clientes de ACME que se hayan suscrito a la comunicación de boletines informativos.
Objetivo: Enviar correos electrónicos de newsletter de moda a los clientes de ACME que se suscribieron para la comunicación.
Detalles promocionales: El cliente recibe noticias de moda en el canal de correo electrónico semanalmente. El correo electrónico debe ser personalizado y las variaciones de contenido deben basarse en el género, el idioma y el mercado.
Canales/puntos de contacto del proyecto: correo electrónico
Destinatarios objetivo: Clientes que se han suscrito a las comunicaciones del boletín de moda ACME.
KPI de objetivo/métricas de participación/ROI: 1. Aumentar los ingresos de productos. 2. Impulse la lealtad del cliente&quot;.

![Ejemplo de un mensaje de estilo lista organizado introducido en el cuadro de entrada de texto para generar un libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Ejemplo 3:**

&quot;Empuje a los compradores a comprar productos durante una campaña promocional de productos en curso.
Interactúe con los compradores durante una promoción continua enviando comunicaciones adecuadas por correo electrónico, SMS o notificaciones push para comprar productos. Envíeles un correo electrónico recordatorio después de 24 horas de que no participen en la promoción&quot;.

![Ejemplo de un mensaje conciso introducido en el cuadro de entrada de texto para generar un libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Ejemplo 4:**

&quot;Vende zapatos a jugadores de secundaria&quot;.

![Ejemplo de un mensaje de una línea introducido en el cuadro de entrada de texto para generar un libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

El asistente de IA elimina todos los detalles innecesarios, como el nombre del proyecto o el fondo. Extrae los elementos clave como la &quot;audiencia de destino&quot;, el &quot;objetivo de campaña&quot; y el &quot;canal de marketing&quot; y funciona con cualquier estilo de entrada.

Estos ejemplos muestran cómo la IA puede refinar y extraer detalles esenciales de las indicaciones del usuario.

>[!NOTE]
>
> Evite PII o palabras explícitas al escribir sus mensajes.

## Directrices y moderación de contenido

Al crear libros de reproducción, tenga en cuenta el idioma y el contenido que incluye. Los libros de reproducción son visibles en toda la organización y cualquier contenido ofensivo o inapropiado que los usuarios marquen.

### Proceso de indicación y revisión

Si un libro de reproducción contiene contenido inapropiado u ofensivo, Adobe recibe automáticamente un informe para su revisión. Adobe revisa el contenido marcado, notifica al cliente si lo considera inapropiado y elimina el manual de implementación.

## Compartir libros de reproducción en zonas protegidas {#share-playbooks-sandboxes}

Al crear y publicar un libro de reproducción en una zona protegida, estará disponible automáticamente en todas las zonas protegidas de su organización. Esta función elimina la necesidad de compartir manualmente y le permite crear instancias del manual en cualquier otra zona protegida sin problemas.

>[!TIP]
>
>Si el manual hace referencia a campos que no están disponibles en el esquema de unión de la zona protegida de destino o si carece de los permisos necesarios, aparece un mensaje de error al intentar crear la instancia. El mensaje especifica los campos y/o permisos que faltan.

Si falta algún campo en el esquema de unión, un cuadro de diálogo lo resalta durante la importación.

![Cuadro de diálogo que enumera los campos que faltan en el esquema de unión durante el proceso de importación del libro de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Uso compartido de libros de reproducción entre organizaciones {#sharing-playbooks-organizations}

Compartir libros de reproducción entre organizaciones ayuda a garantizar la coherencia y la eficacia cuando varios equipos necesitan seguir las mismas prácticas recomendadas. Para compartir un manual de una organización a otra, siga estos pasos:

1. **Inicie sesión en la organización de origen**: vaya a la organización que contiene el manual que creó y que desea compartir desde la ficha **[!UICONTROL Sus libros de reproducción]**.
2. **Publicar el libro de reproducción**: Si el libro de reproducción no se ha publicado todavía, debe publicarlo antes de compartirlo.

   >[!NOTE]
   >
   >Debe establecerse una asociación entre las organizaciones de origen y de destino para permitir el uso compartido del manual. Aprenda a [crear una solicitud de asociación con una organización](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request).

3. **Iniciar uso compartido**: Una vez que se publique el libro de reproducción y se establezca una asociación, seleccione **[!UICONTROL Compartir libro de reproducción]**.
4. **Seleccione la organización de destino**: elija la organización con la que desea compartir el manual de implementación cuando se le solicite.
5. **Confirmar y compartir**: Confirme su selección. Recibirá mensajes de confirmación que indican que el uso compartido se ha realizado correctamente.
6. **Verificar la organización de destino**: Inicie sesión en la organización de destino para verificar que el manual esté disponible.
7. **Importar el manual**: selecciona **[!UICONTROL Importar]** para llevar el manual a la organización de destino. Puede verlo en la ficha **Libros de reproducción**.

Si no aparece el manual, asegúrese de que se publique y de que la asociación de organización esté activa.

>[!IMPORTANT]
>
>No se admite el uso compartido transitorio de libros de reproducción. Si comparte un manual de una organización a otra y luego lo importa, no se puede volver a compartir desde la organización receptora a una tercera organización.

## Permisos necesarios {#required-permissions}

Para acceder a la zona protegida y utilizar esta función, necesita los siguientes permisos:

### Permisos de zona protegida

Estos permisos son necesarios para acceder al entorno de zona protegida donde existe la función:

* **Administrar zona protegida**
* **Ver zona protegida**

* **Permisos para compartir paquetes**:

Estos permisos son necesarios para la funcionalidad de uso compartido interno:

* [**Administrar paquete**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Compartir paquete**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Utilice estos permisos para lo siguiente:

* Introduzca el entorno de zona protegida
* Acceder a la función dentro de la zona protegida
* Administrar y compartir paquetes según sea necesario

Estos permisos se encuentran en la sección **[!UICONTROL Zonas protegidas]** de la lista de permisos.

![Se ha resaltado la lista de permisos con permisos relevantes para administrar y compartir libros de reproducción.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Recorridos y objetos relacionados: permisos

Al crear Recorridos que utilizan libros de reproducción, podría hacer referencia a otros objetos, como **Canales**, **Audiencias** y otras entidades. Cada uno de estos objetos tiene su propio conjunto de permisos.

Estos son los permisos clave para las acciones relacionadas con el Recorrido, como:

* **Ver recorrido**
* **Administrar recorrido**
* Permisos relacionados con objetos como audiencias y canales

También necesita los siguientes permisos de audiencia:

* **Lectura de segmento**
* **Lectura de perfil**
* **Lectura de conjunto de datos**

Como los Recorridos son muy flexibles y pueden incluir muchos objetos interconectados, sus [permisos completos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) se documentan por separado y pueden variar según el caso de uso en que se encuentren.

## Pasos siguientes

Ahora que sabe cómo crear, publicar y compartir libros de reproducción con el Asistente de IA, aprenda a empezar con los libros de reproducción disponibles y elija el adecuado para su caso de uso en [Lista de libros de reproducción](/help/use-case-playbooks/playbooks/choose.md).