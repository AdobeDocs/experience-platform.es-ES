---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Introducción a Real-time Customer Data Platform
description: Utilice este escenario de muestra como ejemplo al configurar la implementación de Adobe Real-Time Customer Data Platform.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# Introducción a Real-time Customer Data Platform

Esta guía de introducción le guía por una implementación de ejemplo de Real-time Customer Data Platform (Real-Time CDP). Puede utilizarlo como ejemplo al configurar su propia implementación. Aunque esta guía muestra ejemplos específicos, vincula a información adicional que puede utilizar al crear la configuración.

Este ejemplo muestra la potencia de Real-time Customer Data Platform, con tecnología de Adobe Experience Platform, para lo siguiente:

* Ingesta de datos desde varias fuentes
* Combinarlos en un único [!DNL real-time customer profile]
* Ofrezca una experiencia coherente, relevante y personalizada en todos los dispositivos.

## Ejemplo de uso

Luma, una empresa de ropa deportiva, siempre está intentando mejorar su experiencia como cliente. Tienen una nueva iniciativa para aumentar las ventas relacionadas con regalos. También quieren reducir la sobreexposición, como los anuncios molestos que siguen a los clientes.

En la actualidad, invierten demasiado en medios que cambian el destino de elementos que el visitante no va a comprar a partir de ahora. Por ejemplo, Luma no quiere redireccionar a alguien con un elemento que se haya diseñado como compra única para otra persona.

En este momento, los datos de Luma están dispersos en múltiples fuentes. Como resultado, se enfrentan a desafíos significativos:

* La organización de marketing debe trabajar con varios equipos, cada uno de los cuales es propietario de una fuente de datos, incluidos un sitio web, una aplicación móvil, sistemas de fidelidad, CRM, etc.
* Para cuando el equipo de marketing obtiene acceso a los datos, estos suelen estar anticuados y ya no son relevantes para su campaña, que distingue entre tiempo y minúsculas.
* Necesitan unificar los datos para que se dirijan a una persona, no a los canales.

Como resultado, Luma tiene los siguientes objetivos empresariales:

* Cree una sola vista en tiempo real de sus consumidores a partir de fuentes de datos dispares.
* Personalice las campañas de marketing con mensajes relevantes en diferentes canales y dispositivos.

Para alcanzar estos objetivos, el equipo de marketing debe poder administrar los datos de los clientes a escala.

Con Real-Time CDP, con tecnología de Adobe Experience Platform, la organización de marketing de Luma puede:

1. Recopile datos de plataformas diferentes y asegúrese de que estén disponibles de forma descendente para otras actividades de marketing.
1. Cree una única vista en tiempo real de sus consumidores, independientemente de dónde se originen los datos.
1. Impulse una experiencia coherente, relevante y personalizada en todos los puntos de contacto.

## Pasos

Este tutorial incluye los siguientes pasos:

1. Genere el [perfil de cliente](#customer-profile).
1. [Personalizar](#personalizing-the-user-experience) la experiencia del usuario.
1. Usar [varios orígenes de datos](#using-multiple-data-sources).
1. [Configurar un origen de datos](#configuring-a-data-source).
1. [Recopile los datos](#bringing-the-data-together-for-a-specific-customer) de un cliente específico.
1. Configurar [audiencias](#audiences).
1. Configurar [destinos](#destinations).
1. [Unir el perfil entre dispositivos](#cross-device-identity-stitching).
1. [Analizar el perfil](#analyzing-the-profile).

## Perfil del cliente

Cuando los clientes visitan el sitio por primera vez, no sabe nada sobre ellos.

![Imagen](assets/luma-site.png)

A medida que navegan, los datos se capturan en tiempo real y se envían no solo a un grupo de informes en Adobe Analytics, sino también directamente a Adobe Experience Platform. A medida que se recopilan los datos, empieza a formar una sola vista del consumidor basada en los datos de comportamiento de [!DNL Experience Platform's real-time customer profile].

Es probable que muchos visitantes del sitio web sean clientes repetidos que ya han realizado compras en Luma.  Es importante que Luma personalice la mensajería y las ofertas para dirigirse tanto a los visitantes nuevos como a los habituales, así como a los clientes conocidos.

### Primera visita del cliente nuevo

Por ejemplo, un visitante no identificado navega a la sección para hombres del sitio de Luma y ve a un par de personas con sudaderas.

![Imagen](assets/luma-sweatshirts.png)

A medida que el cliente navega para obtener más información sobre estos productos, estas vistas de productos se recopilan en Adobe Analytics y se envían a [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma puede asignar el comportamiento del visitante a un perfil de usuario en Adobe Experience Platform y comenzar a ensamblar una vista más completa del comportamiento de ese consumidor.

### Obtención de una vista más detallada del cliente

A medida que el cliente sigue interactuando con el sitio web, se obtiene una imagen más clara. Por ejemplo, supongamos que el visitante agrega un producto al carro de compras e inicia sesión.

Cuando el cliente inicia sesión, se identifica como Sarah Rose.

![Imagen](assets/luma-login.png)

Se combinan dos identidades:

* Los datos de navegación anónimos
* Los datos existentes asociados con la cuenta de Sarah Rose

Ambos identidades se combinan en un solo perfil en [!DNL Experience Platform]. Luma ahora tiene una vista unificada de este consumidor.

En función del comportamiento de navegación del visitante anónimo en la sección para hombres del sitio, se podría haber supuesto que el cliente era un hombre. Ahora que ha iniciado sesión, Luma reconoce a Sarah Rose. Luma utiliza la potencia de [!DNL Real-Time Customer Profile] para restringir la mensajería que se le envía a través de los canales.

## Personalización de la experiencia del usuario

Sarah es bienvenida con un mensaje de lealtad y le agradece por ser miembro de Bronze con más información sobre los beneficios y cómo aumentar su estado y los puntos.

Navega a la página principal para buscar más.

![Imagen](assets/luma-personal.png)

Sarah recibe una experiencia de página de inicio personalizada que se entrega de forma dinámica en función de su [!DNL Real-Time Customer Profile] en Adobe Experience Platform.

Ve contenido relevante, gracias a la personalización basada en Adobe Sensei en Adobe Target, que tiene en cuenta sus compras anteriores y su afinidad por la ropa y el equipo que lleva. Luma también adapta el contenido del catálogo masculino a los equipos de running para hombre en función de su navegador más reciente.

Más adelante en la página, se muestran los productos destacados de Sarah, así como una nueva bandeja de recomendaciones basada en los artículos vistos más recientemente.

Este contenido personalizado ayuda a Sarah a encontrar artículos relevantes rápidamente. Esto aumenta las conversiones y proporciona una experiencia del cliente más agradable.

### Devolución del cliente

Sarah se distrae y abandona el sitio, finalizando su sesión. Luma puede utilizar sus datos en Adobe Experience Platform para ayudarla a regresar al sitio.

Real-time Customer Data Platform, con tecnología Adobe Experience Platform, está diseñado para la administración de experiencias del cliente. Permite a las organizaciones:

* Simplificación de la integración y activación de datos
* Gestionar el uso de datos conocidos y desconocidos
* Acelerar los casos de uso de marketing a escala

## Uso de varias fuentes de datos

El equipo de Luma tiene todos sus datos de comportamiento y de clientes en un solo lugar.

![Imagen](assets/luma-dash.png)

Pueden introducir datos de todas las fuentes siguientes:

* Datos de soluciones de Adobe Experience Cloud existentes
* Fuentes que no son de Adobe, como el programa de fidelidad de Luma, el centro de llamadas y los datos del sistema del punto de venta
* Datos de flujo en tiempo real de fuentes de datos de Luma
* Datos en tiempo real de las soluciones de Adobe (no se requieren nuevas etiquetas)

Todos estos datos de diferentes fuentes se combinan en un único perfil de cliente unificado.

## Configuración de una fuente de datos

Use [!DNL Real-Time Customer Data Platform] para introducir nuevas fuentes de datos en Platform. Real-Time CDP incluye un catálogo de fuentes de datos que se pueden añadir rápida y fácilmente al perfil.

![Imagen](assets/luma-source-cat.png)

Por ejemplo, para introducir los datos CRM de Luma, filtre el catálogo por *CRM* y se enumerarán todos los conectores listos para usar que contengan *CRM*. Para agregar [!DNL Microsoft Dynamics CRM] datos:

1. Autorice la conexión.

   ![Imagen](assets/luma-source-auth.png)

1. Elija lo que desea importar de una lista recomendada de tablas preasignadas de XDM.

   <!--    ![image](assets/luma-source-import.png) -->

   Por ejemplo, seleccione **[!UICONTROL Contactos]**. Se carga automáticamente una previsualización de los datos de los contactos para que pueda asegurarse de que todo tiene el aspecto esperado.

   Real-Time CDP soluciona gran parte del trabajo manual de este proceso asignando automáticamente campos estándar al esquema de perfil [!DNL Experience Data Model] (XDM).

1. Revise las asignaciones de campo.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Por ejemplo, compruebe que el campo de correo electrónico de los contactos esté asignado correctamente.\
   Tiene la opción de previsualizar los datos y realizar una asignación avanzada.

1. Establezca una programación.

   ![Imagen](assets/luma-source-sched.png)

Ya está hecho. Acaba de agregar [!DNL Microsoft CRM] como origen de datos a [!DNL Experience Platform].

### Etiquetado de datos ingeridos para políticas de uso

Luma tiene muchas políticas internas que restringen el uso de ciertos tipos de información recopilada, y también debe cumplir con las preocupaciones legales y relacionadas con la privacidad con respecto al uso de datos. Con el control de datos de Adobe Experience Platform, se pueden aplicar etiquetas de uso de datos predefinidas a conjuntos de datos (y campos específicos dentro de esos conjuntos de datos), lo que permite a Luma categorizar sus datos según restricciones de uso específicas.

![](assets/governance-labels.png)

Una vez aplicadas las etiquetas de uso de datos, Luma puede utilizar la gobernanza de datos para crear políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones que se le permite realizar en los datos que contienen determinadas etiquetas. Al intentar realizar una acción en Real-Time CDP que constituye una infracción de directiva, la acción se evita y se alerta para mostrar qué directiva se ha violado y por qué.

Además, Real-Time CDP

## Recopilación de datos para un cliente específico

En este escenario, busque los perfiles de Sarah Rose. Aparece su perfil, con el correo electrónico que usó para iniciar sesión.

<!-- ![image](assets/luma-find-profile.png) -->

Toda la información de perfil que Luma tiene sobre Sarah se muestra. Esto incluye su información personal, como la dirección y el número de teléfono, las preferencias de comunicación y las audiencias para las que califica.

| Categoría | Descripción |
|---|---|
| Identidades | Muestra las identidades que se han vinculado en [!DNL Platform] desde las interacciones de Sarah con Luma entre canales y dispositivos. Se muestra su ECID del sitio web. Su identidad también incluye el ECID de su aplicación móvil, su ID de correo electrónico, un ID de CRM del conjunto de datos [!DNL Microsoft Dynamics] agregado recientemente y un ID de fidelidad pasado a Adobe Experience Platform desde el sistema de fidelidad de Luma. |
| Eventos | Muestra todos los datos de interacción de Sarah con la marca Luma. Esto incluye el artículo que acaba de ver, cualquier cosa que haya visto en el pasado, los correos electrónicos que ha recibido, sus interacciones con el centro de llamadas y en qué canal y dispositivo se produjo cada una de esas interacciones. |

El perfil de Real-Time CDP reduce el flujo de trabajo del equipo de marketing de Luma de semanas a minutos y desbloquea las posibilidades de personalización en función de esta vista de cliente de 360 grados. El perfil combina los datos de comportamiento de cuando navegó por el sitio antes de iniciar sesión, con el perfil de cliente existente, lo que crea una vista completa de Sarah.

El equipo de marketing puede usar este [!DNL Real-Time Customer Profile] mejorado para personalizar mejor la experiencia de Sarah y aumentar la lealtad de su marca con Luma.

## Públicos

Las potentes capacidades de segmentación de Adobe Experience Platform permiten a los especialistas en marketing combinar atributos, eventos y audiencias existentes, según los datos capturados en [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

En este escenario, las recientes interacciones de Sarah en el sitio muestran un comportamiento diferente al de sus acciones pasadas. Ella suele comprar ropa de mujer. Sin embargo, el artículo en su carro es una sudadera grande para hombre.

El equipo de ciencia de datos de Luma ha creado modelos en torno a la tendencia a comprar. Un modelo identifica un cambio repentino en la categoría de la ropa (como hombres/mujeres) o el tamaño para el consumidor existente. El cambio de Sarah en el comportamiento de compra sugiere que no está comprando para sí misma.

<!-- ![image](assets/luma-gift.png) -->

### Definición de una audiencia

Utilice las distintas opciones del editor de expresiones basado en código o composición visual en el espacio de trabajo de audiencias para modificar o crear una audiencia que represente a los abandonadores del carro de compras que parecen estar en proceso de compra de un regalo:

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Debido a que Sarah agregó un elemento de regalo aparente al carro de compras y lo abandonó, Luma puede dirigirla con una oferta de envoltorio para regalos gratuita.

## Destinos

Cuando haya agregado la audiencia &quot;Abandonadores del carro de compras de regalos&quot;, podrá ver aproximadamente cuántas personas forman parte de esta audiencia. Puede realizar acciones en él y ponerlo a disposición para su personalización en todos los canales.

Seleccione **[!UICONTROL Enviar a destinos]**.

En Real-Time CDP, Luma puede actuar sin problemas en sus audiencias para la personalización.\
Aquí vemos todos los destinos disponibles para que Luma los envíe, tanto a soluciones de Adobe como a soluciones que no sean de Adobe:

![Imagen](assets/luma-dest.png)

### Selección de destinos

En esta situación, Luma quiere volver a dirigirse a esta audiencia con personalización en estos destinos:

* Google, para visualización
  <!--* Facebook -->
* Adobe Campaign, para correo electrónico

<!-- ![image](assets/luma-sched-dest.png) -->

### Programación de destinos

También puede programar la exportación de audiencias para que comience o termine en un momento determinado. La audiencia se publicará y actualizará automáticamente en las plataformas configuradas en las fechas programadas.

>[!NOTE]
>
>De forma opcional, si selecciona el campo de fecha, se programa automáticamente para 90 días.

Seleccione **[!UICONTROL Guardar]** para ir a la página siguiente.

Cuando un cliente de esta audiencia realiza una compra, su pertenencia a esta audiencia se suprime en tiempo real. Ya no cumplen los requisitos porque su estatus ha cambiado.

Esto ahorra al director del equipo de medios de Luma cientos de miles de dólares al no usar el inventario para una audiencia que no está calificada.

### Aplicar políticas de uso de datos a los destinos

Adobe Experience Platform incluye controles de privacidad y seguridad para determinar si una audiencia está disponible para activarse en un destino determinado. La activación está habilitada o restringida en función de los fines de marketing asignados al destino cuando se creó, así como de las políticas de uso de datos definidas por su organización.

Si su actividad infringe una directiva, aparece una advertencia. Esta advertencia contiene información de linaje de datos que puede ayudarle a identificar por qué se violó la directiva y qué puede hacer para resolver la infracción.

Con estos controles, [!DNL Experience Platform] ayuda a Luma a cumplir con las regulaciones y a comercializar de forma responsable. Estos controles son flexibles y se pueden modificar para satisfacer los requisitos de los equipos de seguridad y control de Luma, lo que les permite abordar con confianza los requisitos regionales y organizativos para administrar datos de clientes conocidos y desconocidos.

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## Vinculación de identidad entre dispositivos

Sarah explora un sitio de medios sociales en su dispositivo móvil y ve un anuncio de Luma. Le recuerda el artículo que dejó en su carrito.

Más tarde, abre su correo electrónico y ve los correos electrónicos redirigidos. Selecciona un vínculo a Luma desde un correo electrónico.

El vínculo lleva a Sarah a la página principal de Luma móvil, donde ve una experiencia altamente personalizada con tecnología de Adobe Target.

* Es bienvenida como miembro de Bronce.
* Ella ve el mensaje &quot;Regalo&quot;.
* También ve el mensaje &quot;Envoltorio para regalos gratis&quot;, que es parte de sus beneficios de membresía Bronze.
* Sigue siendo un objetivo en la imagen de héroe basado en su afinidad por correr.

Compra el suéter, agrega envoltorio para regalos y escribe una nota de regalo. También tiene la opción de recordar este evento y recibir un recordatorio el año que viene para recibir un regalo en este momento. Ella dice que sí, y está programada en una campaña por correo electrónico al año siguiente para recordarle que compre otro regalo.

Gracias a las capacidades de supresión de audiencia, Sarah no será el objetivo de que el suéter de ese hombre avance.

## Análisis del perfil

Los especialistas en marketing de Luma utilizan Adobe Experience Platform para ver la audiencia de los proveedores de regalos en el panel de Real-Time CDP. Ven los resultados de esta iniciativa a lo largo del tiempo y ven que está creciendo. Los clientes responden a las ofertas y gastan más dinero.

Estas perspectivas permiten a los especialistas en marketing tomar medidas sobre esta señal, que se alimentó de que estos datos estuvieran disponibles en CDP y de que clientes como Sarah estuvieran conectados a la audiencia.

Luma utiliza estos datos de CDP para aumentar la lealtad y la satisfacción del cliente.
