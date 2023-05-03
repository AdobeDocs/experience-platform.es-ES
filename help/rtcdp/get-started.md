---
keywords: RTCDP;CDP;Real-time Customer Data Platform;plataforma de datos de clientes en tiempo real;cdp en tiempo real;cdp;rtcdp
title: Introducción a Real-time Customer Data Platform
description: Utilice este escenario de muestra como ejemplo al configurar la implementación de Adobe Real-Time Customer Data Platform.
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 2%

---

# Introducción a Real-time Customer Data Platform

Esta guía de introducción le guía a través de una implementación de muestra de Real-time Customer Data Platform (Real-Time CDP). Puede usarlo como ejemplo al configurar su propia implementación. Aunque esta guía muestra ejemplos específicos, vincula a información adicional que puede utilizar al crear la configuración.

Este ejemplo muestra la potencia de Real-time Customer Data Platform, con tecnología de Adobe Experience Platform, para:

* Ingesta de datos de varias fuentes
* Combínelos en una sola [!DNL real-time customer profile]
* Ofrezca una experiencia coherente, relevante y personalizada entre dispositivos.

## Caso de uso

Luma, una compañía de ropa deportiva, siempre está tratando de mejorar su experiencia con el cliente. Tienen una nueva iniciativa para aumentar las ventas relacionadas con regalos. También desean reducir la sobreexposición, como los anuncios molestos que siguen a los clientes.

Actualmente, están gastando demasiado en medios que se vuelven a destinar a elementos que el visitante no va a comprar para avanzar. Por ejemplo, Luma no quiere volver a dirigirse a alguien con un artículo que fue diseñado como una compra única para otra persona.

En este momento, los datos de Luma están dispersos en múltiples fuentes. Como resultado, se enfrentan a importantes desafíos:

* La organización de marketing debe trabajar con varios equipos que sean propietarios de una fuente de datos, incluidos un sitio web, una aplicación móvil, sistemas de fidelidad, CRM, etc.
* Para cuando el equipo de marketing obtiene acceso a los datos, a menudo están obsoletos y ya no son relevantes para su campaña que diferencia tiempo.
* Deben unificar los datos para que se dirijan a una persona, no a los canales.

Como resultado, Luma tiene los siguientes objetivos comerciales:

* Cree una vista única en tiempo real de sus consumidores a partir de sus diferentes fuentes de datos.
* Personalice las campañas de marketing con mensajes relevantes en diferentes canales y dispositivos.

Para alcanzar estos objetivos, el equipo de marketing debe poder administrar los datos de los clientes a escala.

Con Real-Time CDP, con tecnología de Adobe Experience Platform, la organización de marketing de Luma puede:

1. Recopile datos de plataformas diferentes y asegúrese de que esté disponible de forma descendente para otras actividades de marketing.
1. Cree una sola vista en tiempo real de sus consumidores, independientemente de dónde se originan los datos.
1. Impulse una experiencia coherente, relevante y personalizada en todos los puntos de contacto.

## Pasos

Este tutorial incluye los siguientes pasos:

1. Cree el [perfil del cliente](#customer-profile).
1. [Personalizar](#personalizing-the-user-experience) la experiencia del usuario.
1. Uso [varias fuentes de datos](#using-multiple-data-sources).
1. [Configuración de una fuente de datos](#configuring-a-data-source).
1. [Recopilar los datos](#bringing-the-data-together-for-a-specific-customer) para un cliente específico.
1. Configuración [segmentos](#segments).
1. Configuración [destinos](#destinations).
1. [Vincular el perfil entre dispositivos](#cross-device-identity-stitching).
1. [Analizar el perfil](#analyzing-the-profile).

## Perfil del cliente

Cuando los clientes visitan su sitio por primera vez, no sabe nada sobre ellos.

![imagen](assets/luma-site.png)

A medida que navegan, los datos se capturan en tiempo real y se envían no solo a un grupo de informes en Adobe Analytics, sino también directamente a Adobe Experience Platform. A medida que se recopilan los datos, se empieza a formar una sola vista del consumidor, basada en los datos de comportamiento de [!DNL Experience Platform's real-time customer profile].

Es probable que muchos visitantes del sitio web sean clientes que repiten reservas y que hayan comprado previamente en Luma.  Es importante que Luma personalice los mensajes y las ofertas para dirigirse tanto a visitantes nuevos como repetidos, así como a clientes conocidos.

### Primera visita del cliente nuevo

Por ejemplo, un visitante no identificado navega a la sección Hombres del sitio de Luma y ve un par de sudaderas con camisas.

![imagen](assets/luma-sweatshirts.png)

A medida que el cliente navega para obtener más información sobre estos productos, estas vistas de producto se recopilan en Adobe Analytics y se envían a [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma puede asignar el comportamiento del visitante a un perfil de usuario en Adobe Experience Platform y empezar a ensamblar una vista más rica del comportamiento de ese consumidor.

### Obtener una vista más detallada del cliente

A medida que el cliente sigue interactuando con el sitio web, aparece una imagen más clara. Por ejemplo, supongamos que el visitante agrega un producto al carro de compras e inicia sesión.

Cuando el cliente inicia sesión, ella se identifica a sí misma como Sarah Rose.

![imagen](assets/luma-login.png)

Se combinan dos identidades:

* Los datos de navegación anónimos
* Los datos existentes asociados con la cuenta de Sarah Rose

Ambos identificadores se combinan en un solo perfil en [!DNL Experience Platform]. Luma tiene ahora una visión unificada de este consumidor.

Según el comportamiento de navegación del visitante anónimo en la sección Hombres del sitio, se puede haber asumido que el cliente era un hombre. Ahora que ha iniciado sesión, Luma reconoce a Sarah Rose. Luma utiliza el poder del [!DNL Real-Time Customer Profile] para perfeccionar los mensajes que se le envían a través de los canales.

## Personalización de la experiencia del usuario

Sarah es recibida con un mensaje de lealtad y agradecida por ser miembro del Bronce con más información sobre beneficios y cómo aumentar su estatus y puntos.

Ella navega a la página de inicio para buscar más.

![imagen](assets/luma-personal.png)

Sarah recibe una experiencia de página principal personalizada que se entrega de forma dinámica, basada en ella [!DNL Real-Time Customer Profile] en Adobe Experience Platform.

Ella ve contenido relevante, gracias a la personalización impulsada por Adobe Sensei en Adobe Target, que tiene en cuenta sus compras anteriores y su afinidad hacia la utilización de ropa y equipo. Luma también adapta el contenido del catálogo masculino a los engranajes de transmisión para hombres en función de su última exploración.

Más abajo en la página, se muestran productos destacados a Sarah, así como una nueva bandeja de recomendaciones basada en sus artículos vistos más recientemente.

Este contenido personalizado ayuda a Sarah a encontrar artículos relevantes rápidamente. Esto aumenta las conversiones y proporciona una experiencia de cliente más agradable.

### Devolver al cliente

Sarah se distrae y deja el sitio, terminando su sesión. Luma puede utilizar sus datos en Adobe Experience Platform para ayudarla a regresar al sitio.

Real-time Customer Data Platform, con tecnología de Adobe Experience Platform, está diseñado para la administración de experiencias de los clientes. Permite a las organizaciones:

* Simplificar la integración y activación de datos
* Administrar el uso de datos conocidos y desconocidos
* Acelerar los casos de uso de marketing a escala

## Uso de varias fuentes de datos

El equipo de Luma tiene todos sus datos de comportamiento y de clientes en un solo lugar.

![imagen](assets/luma-dash.png)

Pueden ingerir datos de todas las fuentes siguientes:

* Datos de soluciones de Adobe Experience Cloud existentes
* Fuentes que no son de Adobe, como el programa de lealtad de Luma, el centro de llamadas y los datos de sistemas de puntos de venta
* Transmisión de datos en tiempo real desde fuentes de datos de Luma
* Datos en tiempo real de soluciones de Adobe (no se requieren etiquetas nuevas)

Todos estos datos de fuentes diferentes se combinan en un único perfil unificado del cliente.

## Configuración de una fuente de datos

Uso [!DNL Real-Time Customer Data Platform] para incorporar nuevas fuentes de datos a Platform. Real-Time CDP incluye un catálogo de fuentes de datos que se pueden agregar rápida y fácilmente al perfil.

![imagen](assets/luma-source-cat.png)

Por ejemplo, para introducir los datos CRM de Luma, filtre el catálogo por *CRM* y todos los conectores listos para usar que contengan *CRM* se muestran. Para agregar [!DNL Microsoft Dynamics CRM] datos:

1. Autorice la conexión.

   ![imagen](assets/luma-source-auth.png)

1. Elija lo que desea importar de una lista recomendada de tablas XDM preasignadas.

   <!--    ![image](assets/luma-source-import.png) -->

   Por ejemplo, seleccione **[!UICONTROL Contactos]**. Se carga automáticamente una vista previa de los datos de contactos para que pueda asegurarse de que todo se ve como se espera.

   Adobe Experience Platform lleva a cabo gran parte del trabajo manual de este proceso asignando automáticamente los campos estándar al [!DNL Experience Data Model] esquema de perfil (XDM).

1. Revise las asignaciones de campos.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Por ejemplo, compruebe dos veces que el campo de correo electrónico de los contactos está asignado correctamente.\
   Tiene la opción de obtener una vista previa de los datos y realizar una asignación avanzada.

1. Establezca una programación.

   ![imagen](assets/luma-source-sched.png)

Ya está hecho. Acaba de añadir [!DNL Microsoft CRM] como fuente de datos en [!DNL Experience Platform].

### Etiquetado de datos introducidos para políticas de uso

Luma tiene muchas políticas internas que restringen el uso de ciertos tipos de información recopilada, y también debe cumplir con las preocupaciones legales y relacionadas con la privacidad con respecto al uso de los datos. Mediante la Administración de datos de Adobe Experience Platform, se pueden aplicar etiquetas de uso de datos predefinidas a conjuntos de datos (y campos específicos dentro de dichos conjuntos de datos), lo que permite a Luma categorizar sus datos según restricciones de uso específicas.

![](assets/governance-labels.png)

Una vez aplicadas las etiquetas de uso de datos, Luma puede utilizar Control de datos para crear políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones que se le permite realizar en los datos que contienen ciertas etiquetas. Cuando se intenta realizar una acción en Real-Time CDP que constituye una infracción de política, la acción se evita y se envía una alerta para mostrar qué política se violó y por qué.

## Agrupación de datos para un cliente específico

En este escenario, busque perfiles para Sarah Rose. Aparece su perfil, con el correo electrónico que utilizó para iniciar sesión.

<!-- ![image](assets/luma-find-profile.png) -->

Toda la información de perfil que Luma tiene sobre las pantallas de Sarah. Esto incluye su información personal como dirección y número de teléfono, preferencias de comunicación y los segmentos para los que califica.

| Categoría | Descripción |
|---|---|
| Identidades | Muestra las identidades que se han vinculado entre sí en [!DNL Platform] de las interacciones de Sarah con Luma a través de canales y dispositivos. Se muestra su ECID del sitio web. Su identidad también incluye el ECID de su aplicación móvil, su ID de correo electrónico, un ID de CRM del recién agregado [!DNL Microsoft Dynamics] conjunto de datos de y un ID de lealtad que se pasa a Adobe Experience Platform desde el sistema de fidelidad de Luma. |
| Eventos | Muestra todos los datos de interacción de Sarah con la marca Luma. Esto incluye el artículo que acaba de ver, cualquier cosa que haya visto en el pasado, los correos electrónicos que ha recibido, sus interacciones con el centro de llamadas y en qué canal y dispositivo se produjeron cada una de esas interacciones. |

El perfil de Real-Time CDP reduce el flujo de trabajo del equipo de marketing de Luma de semanas a minutos y desbloquea las posibilidades de personalización en función de esta vista de cliente de 360 grados. El perfil combina los datos de comportamiento de cuando navegó por el sitio antes de iniciar sesión, con su perfil de cliente existente, lo que crea una vista completa de Sarah.

El equipo de marketing puede utilizar esta mejora, [!DNL Real-Time Customer Profile] para personalizar mejor la experiencia de Sarah y aumentar su lealtad de marca con Luma.

## Segmentos

Las potentes funciones de segmentación de Adobe Experience Platform permiten a los especialistas en marketing combinar atributos, eventos y segmentos existentes, según los datos capturados en la variable [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

En este escenario, las recientes interacciones de Sarah en el sitio muestran un comportamiento diferente al de sus acciones pasadas. Ella generalmente compra ropa de mujer. Sin embargo, el artículo de su carrito es una camisa grande para hombres.

El equipo de ciencia de datos de Luma ha creado modelos en torno a la propensión a comprar. Un modelo identifica un cambio repentino en la categoría de ropa (como hombres/mujeres) o el tamaño para el consumidor existente. El cambio en el comportamiento de compra de Sarah sugiere que no está comprando para sí misma.

<!-- ![image](assets/luma-gift.png) -->

### Definición de un segmento

Modifique o cree un segmento que represente a los abandonadores del carro de compras que parecen estar en proceso de comprar un regalo:

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

Como Sarah agregó un aparente artículo de regalo en el carrito y lo abandonó, Luma puede dirigirlo con una oferta de encapsula de regalo gratuita.

## Destinos

Cuando haya agregado el segmento &quot;Abandonos del carro de compras de regalos&quot;, puede ver aproximadamente cuántas personas forman parte de este segmento. Puede realizar acciones en él y ponerlo a disposición para su personalización en todos los canales.

Select **[!UICONTROL Enviar a destinos]**.

En Real-Time CDP, Luma puede actuar sin problemas en sus segmentos de audiencia para su personalización.\
Aquí vemos todos los destinos disponibles para que Luma envíe este destino a soluciones tanto de Adobe como de no Adobe:

![imagen](assets/luma-dest.png)

### Selección de destinos

En esta situación, Luma quiere volver a dirigirse a esta audiencia con personalización en todos estos destinos:

* Google, para visualización

   <!--* Facebook -->
* Adobe Campaign, para correo electrónico

<!-- ![image](assets/luma-sched-dest.png) -->

### Programación de destinos

También puede programar el inicio o el final del segmento en un momento concreto. El segmento se publicará y se actualizará automáticamente en las plataformas configuradas en las fechas programadas.

>[!NOTE]
>
>De forma opcional, si selecciona el campo de fecha, se programa automáticamente durante 90 días.

Select **[!UICONTROL Guardar]** para ir a la página siguiente.

Cuando un cliente de esta audiencia realiza una compra, su pertenencia a esta audiencia se suprime en tiempo real. Ya no cumplen los requisitos porque su estado ha cambiado.

Esto ahorra al director del equipo de medios de Luma cientos de miles de dólares al no usar el inventario para una audiencia que no está calificada.

### Aplicación de políticas de uso de datos para destinos

Adobe Experience Platform incluye controles de seguridad y privacidad para determinar si un segmento está disponible para activarse en un destino determinado. La activación está habilitada o restringida según los fines de marketing asignados al destino cuando se creó, así como las políticas de uso de datos definidas por su organización.

Si la actividad infringe una directiva, aparece una advertencia. Esta advertencia contiene información de linaje de datos que puede ayudarle a identificar por qué se violó la directiva y qué puede hacer para resolver la infracción.

Con estos controles, [!DNL Experience Platform] ayuda a Luma a cumplir con las regulaciones y a comercializar de forma responsable. Estos controles son flexibles y pueden modificarse para satisfacer los requisitos de los equipos de seguridad y gobernanza de Luma, lo que les permite abordar con seguridad los requisitos regionales y organizativos para administrar datos conocidos y desconocidos de los clientes.

### Lienzo del flujo de datos

Al guardar, un lienzo visual de flujo de datos muestra el segmento asignado desde el perfil unificado a los tres destinos seleccionados.

![imagen](assets/luma-flow.png)

## Vinculación de identidad entre dispositivos

Sarah explora un sitio de medios sociales en su dispositivo móvil, y ve un anuncio de Luma. Le recuerda el artículo que dejó en su carrito.

Más tarde, abre su correo electrónico y ve los correos electrónicos redirigidos. Selecciona un enlace a Luma de un correo electrónico.

El enlace lleva a Sarah a la página de inicio móvil de Luma, donde ve una experiencia altamente personalizada ofrecida por Adobe Target.

* Es recibida como miembro del Bronce.
* Ella ve el mensaje &quot;Regalo&quot;.
* También ve el mensaje &quot;Free Gift Wrap&quot;, que es parte de sus beneficios de membresía en Bronce.
* Todavía está en la imagen de la heroína basada en su afinidad por correr.

Ella compra el suéter, agrega envoltura de regalo y escribe una nota de regalo. También tiene la opción de recordar este evento y recibir un recordatorio el próximo año para recibir un regalo en este momento. Dice que sí, y está programado para una campaña de correo electrónico el año siguiente para recordarle que compre otro regalo.

Gracias a las capacidades de supresión de audiencia, Sarah no será el objetivo con el suéter de esos hombres avanzando.

## Análisis del perfil

Los especialistas en marketing de Luma utilizan Adobe Experience Platform para ver el segmento de regalos en el panel de Real-Time CDP. Ven los resultados de esta iniciativa a lo largo del tiempo y ven que está creciendo. Los clientes responden a las ofertas y gastan más dinero.

Estas perspectivas permiten a los especialistas en marketing tomar medidas sobre esta señal, que se vio impulsada por tener estos datos disponibles en CDP y por tener clientes como Sarah conectados al segmento.

Luma utiliza estos datos CDP para aumentar la lealtad y la satisfacción del cliente.
