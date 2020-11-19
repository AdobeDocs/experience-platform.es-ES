---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Introducción a la plataforma de datos de clientes en tiempo real
seo-title: Introducción a la plataforma de datos de clientes en tiempo real
description: 'Caso de ejemplo para la plataforma de datos del cliente en tiempo real de '
seo-description: 'Caso de ejemplo para la plataforma de datos del cliente en tiempo real de '
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 1%

---


# Introducción a la plataforma de datos de clientes en tiempo real

Esta guía de introducción le guía a través de una implementación de muestra de la Plataforma de datos del cliente en tiempo real (CDP en tiempo real). Puede utilizarlo como ejemplo al configurar su propia implementación. Aunque esta guía muestra ejemplos específicos, vincula a información adicional que puede utilizar al crear la configuración.

Este ejemplo muestra el poder de la plataforma de datos del cliente en tiempo real, con tecnología de Adobe Experience Platform, para:

* Ingestar datos de varias fuentes
* Combinarlos en un solo [!DNL real-time customer profile]
* Ofrezca una experiencia coherente, relevante y personalizada en todos los dispositivos.

## Ejemplo de uso

Luma, una compañía de ropa deportiva, siempre está tratando de mejorar su experiencia con los clientes. Tienen una nueva iniciativa para aumentar las ventas relacionadas con regalos. También desean reducir la sobreexposición, como los anuncios molestos que siguen a los clientes.

Actualmente, están gastando demasiado en medios que se vuelven a enfocar en elementos que el visitante no va a comprar para avanzar. Por ejemplo, Luma no quiere redirigirse a alguien con un artículo que fue diseñado como una compra única para otra persona.

En este momento, los datos de Luma están dispersos en múltiples fuentes. Como resultado, se enfrentan a importantes desafíos:

* La organización de marketing debe trabajar con varios equipos que poseen una fuente de datos, incluidos un sitio web, una aplicación móvil, sistemas de fidelidad, CRM, etc.
* Para cuando el equipo de mercadotecnia obtiene acceso a los datos, a menudo están obsoletos y ya no son relevantes para su campaña que diferencia tiempo.
* Necesitan unificar los datos para que destinatario a una persona, no a canales.

Como resultado, Luma tiene los siguientes objetivos comerciales:

* Cree una vista única en tiempo real de sus consumidores a partir de sus distintas fuentes de datos.
* Personalice las campañas de marketing con mensajes relevantes en diferentes canales y dispositivos.

Para alcanzar estos objetivos, el equipo de mercadotecnia debe poder administrar los datos de los clientes a escala.

Con CDP en tiempo real, con la tecnología de Adobe Experience Platform, la organización de mercadotecnia de Luma puede:

1. Recopile datos de distintas plataformas y asegúrese de que esté disponible en el flujo descendente para otras actividades de marketing.
1. Cree una única vista en tiempo real de sus consumidores, independientemente de dónde se originen los datos.
1. Impulse una experiencia coherente, relevante y personalizada en todos los puntos de contacto.

## Pasos

Este tutorial incluye los siguientes pasos:

1. Genere el perfil [](#customer-profile)del cliente.
1. [Personalice](#personalizing-the-user-experience) la experiencia del usuario.
1. Utilice [varias fuentes](#using-multiple-data-sources)de datos.
1. [Configure un origen](#configuring-a-data-source)de datos.
1. [Recopilar los datos](#bringing-the-data-together-for-a-specific-customer) de un cliente específico.
1. Configure [segmentos](#segments).
1. Configure [los destinos](#destinations).
1. [Apriete el perfil entre dispositivos](#cross-device-identity-stitching).
1. [Analizar el perfil](#analyzing-the-profile).

## Perfil del cliente

Cuando los clientes visitan el sitio por primera vez, usted no sabe nada de ellos.

![imagen](assets/luma-site.png)

A medida que navegan, los datos se capturan en tiempo real y se envían no sólo a un grupo de informes en Adobe Analytics, sino también directamente a Adobe Experience Platform. A medida que se recopilan los datos, se empieza a formar una sola vista del consumidor, basada en los datos de comportamiento de [!DNL Experience Platform's real-time customer profile].

Muchos visitantes al sitio web son probablemente clientes repetidos que han comprado anteriormente a Luma.  Es importante que Luma personalice los mensajes y las ofertas para abordar tanto los visitantes nuevos como los repetidos, así como los clientes conocidos.

### Primera visita del nuevo cliente

Por ejemplo, un visitante sin identificar navega a la sección de hombres del sitio de Luma y vista a una pareja que lleva camisas sudaderas.

![imagen](assets/luma-sweatshirts.png)

A medida que el cliente hace clic para obtener más información sobre estos productos, estas vistas se recopilan en Adobe Analytics y se envían a [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma puede asignar el comportamiento del visitante a un perfil de usuario en Adobe Experience Platform y empezar a crear una vista más rica del comportamiento de ese consumidor.

### Obtener una vista más detallada del cliente

A medida que el cliente continúa interactuando con el sitio web, surge una imagen más clara. Por ejemplo: supongamos que el visitante agrega un producto al carro de compras e inicia sesión.

Cuando el cliente inicia sesión, ella se identifica como Sarah Rose.

![imagen](assets/luma-login.png)

Se combinan dos identidades:

* Los datos de exploración anónimos
* Los datos existentes asociados con la cuenta de Sarah Rose

Ambas identidades se combinan en un solo perfil en [!DNL Experience Platform]. Luma tiene ahora una vista unificada de este consumidor.

Según el comportamiento de navegación del visitante anónimo en la sección Hombres del sitio, se podría haber asumido que el cliente era un hombre. Ahora que ha iniciado sesión, Luma reconoce a Sarah Rose. Luma utiliza el poder del [!DNL Real-time Customer Profile] para refinar los mensajes que se le envían a través de los canales.

## Personalización de la experiencia del usuario

Sarah es bienvenida con un mensaje de lealtad y agradecida por ser miembro del Bronce con más información sobre beneficios y cómo aumentar su estatus y puntos.

Ella hace clic en la página de inicio para explorar un poco más.

![imagen](assets/luma-personal.png)

Sarah recibe una experiencia de página de inicio personalizada que se distribuye dinámicamente, basada en ella [!DNL Real-time Customer Profile] en Adobe Experience Platform.

Ella ve contenido relevante, gracias a la personalización impulsada por Adobe Sensei en Adobe Target, que tiene en cuenta sus compras pasadas y la afinidad hacia la utilización de ropa y equipo. Luma también adapta el contenido del catálogo masculino a los engranajes en marcha para los hombres según su última exploración.

Más abajo de la página, se muestran productos destacados a Sarah, así como una nueva bandeja de recomendaciones basada en los artículos que ha visto más recientemente.

Este contenido personalizado ayuda a Sarah a encontrar artículos relevantes rápidamente. Esto aumenta las conversiones y proporciona una experiencia de cliente más agradable.

### Devolver al cliente

Sarah se distrae y abandona el sitio, terminando su sesión. Luma puede usar sus datos en Adobe Experience Platform para ayudarla a regresar al sitio.

La plataforma de datos del cliente en tiempo real, con tecnología de Adobe Experience Platform, está diseñada para la administración de la experiencia del cliente. Permite a las organizaciones:

* Simplifique la integración y activación de datos
* Administrar el uso de datos conocidos y desconocidos
* Acelerar los casos de uso de mercadotecnia a escala

## Uso de varias fuentes de datos

El equipo de Luma tiene todos sus datos de comportamiento y de clientes en un solo lugar.

![imagen](assets/luma-dash.png)

Pueden ingestar datos de todas las fuentes siguientes:

* Datos de soluciones de Adobe Experience Cloud existentes
* Fuentes que no son de Adobe, como el programa de lealtad de Luma, el centro de llamadas y los datos del sistema del punto de venta
* Datos de flujo continuo en tiempo real de fuentes de datos Luma
* Datos en tiempo real de soluciones de Adobe (no se requieren etiquetas nuevas)

Todos estos datos de fuentes diferentes se combinan en un único perfil de cliente unificado.

## Configuración de una fuente de datos

Se utiliza [!DNL Real-time Customer Data Platform] para traer nuevas fuentes de datos a la plataforma. CDP en tiempo real incluye un catálogo de fuentes de datos que se pueden agregar al perfil en tan solo unos clics.

![imagen](assets/luma-source-cat.png)

Por ejemplo, para ingestar datos CRM de Luma, filtre el catálogo por *CRM* y se muestran todos los conectores listos para usar que contienen *CRM* . Para agregar [!DNL Microsoft Dynamics CRM] datos:

1. Autorice la conexión.

   ![imagen](assets/luma-source-auth.png)

1. Elija lo que desea importar desde una lista recomendada de tablas XDM preasignadas.

   <!--    ![image](assets/luma-source-import.png) -->

   Por ejemplo, seleccione **[!UICONTROL Contactos]**. Se carga automáticamente una previsualización de los datos de los contactos para asegurarse de que todo se ve como se espera.

   La plataforma Adobe Experience lleva gran parte del trabajo manual de este proceso asignando automáticamente los campos estándar al esquema de perfil [!DNL Experience Data Model] (XDM).

1. Revise las asignaciones de campos.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Por ejemplo, compruebe por doble que el campo de correo electrónico de los contactos está correctamente asignado.\
   Tiene la opción de previsualización de los datos y realizar asignaciones avanzadas.

1. Configure una programación.

   ![imagen](assets/luma-source-sched.png)

Ya está hecho. Acaba [!DNL Microsoft CRM] de agregarse como fuente de datos a [!DNL Experience Platform].

### Etiquetado de datos ingestados para directivas de uso

Luma tiene muchas políticas internas que restringen el uso de ciertos tipos de información recopilada, y también debe cumplir con las preocupaciones legales y relacionadas con la privacidad con respecto al uso de datos. Con Adobe Experience Platform [!DNL Data Governance], las etiquetas de uso de datos predefinidas se pueden aplicar a conjuntos de datos (y a campos específicos dentro de dichos conjuntos de datos), lo que permite a la luminancia categorizar sus datos según restricciones de uso específicas.

![](assets/governance-labels.png)

Una vez aplicadas las etiquetas de uso de datos, Luma puede usar [!DNL Data Governance] para crear políticas de uso de datos. Las políticas de uso de datos son reglas que describen los tipos de acciones que se le permite realizar en datos que contienen ciertas etiquetas. Al intentar realizar una acción en tiempo real de CDP que constituye una infracción de política, se evita la acción y se proporciona una alerta para mostrar qué política se violó y por qué.

## Reunir los datos para un cliente específico

En este escenario, busque perfiles para Sarah Rose. Aparece su perfil, con el correo electrónico en el que solía iniciar sesión.

<!-- ![image](assets/luma-find-profile.png) -->

Toda la información de perfil que Luma tiene sobre Sarah muestra. Esto incluye su información personal como dirección y número de teléfono, preferencias de comunicación y los segmentos para los que califica.

| Categoría | Descripción |
|---|---|
| Identidades | Muestra las identidades que han estado vinculadas entre sí [!DNL Platform] desde las interacciones de Sarah con Luma a través de canales y dispositivos. Se muestra su ECID del sitio web. Su identidad también incluye el ECID de su aplicación móvil, su ID de correo electrónico, un ID de CRM del conjunto de datos recientemente agregado y un ID de lealtad que se pasa a Adobe Experience Platform desde el sistema de fidelidad a Luma. [!DNL Microsoft Dynamics] |
| Eventos | Muestra todos los datos de interacción de Sarah con la marca Luma. Esto incluye el artículo que acaba de ver, cualquier cosa que haya visto en el pasado, los correos electrónicos que ha recibido, sus interacciones con el centro de llamadas y en qué canal y dispositivo han ocurrido cada una de esas interacciones. |

El perfil CDP en tiempo real reduce el flujo de trabajo del equipo de mercadotecnia Luma de semanas a minutos y desbloquea las posibilidades de personalización basadas en esta vista de 360 grados para el cliente. El perfil combina los datos de comportamiento de cuando exploró el sitio antes de iniciar sesión, con su perfil de cliente existente, creando una vista integral de Sarah.

El equipo de mercadotecnia puede usar esta herramienta mejorada, [!DNL Real-time Customer Profile] para personalizar mejor la experiencia de Sarah y aumentar su lealtad de marca con Luma.

## Segmentos

Las potentes funciones de segmentación de Adobe Experience Platform permiten a los especialistas en mercadotecnia combinar atributos, eventos y segmentos existentes, según los datos capturados en la [!DNL Real-time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

En este escenario, las recientes interacciones de Sarah en el sitio muestran un comportamiento diferente al de sus acciones pasadas. Ella generalmente compra ropa de mujer. Sin embargo, el artículo en su carro es una camisa grande para hombres.

El equipo de ciencia de datos Luma ha creado modelos en torno a la propensión a comprar. Un modelo identifica un cambio repentino en la categoría de ropa (como hombres/mujeres) o el tamaño del consumidor existente. El cambio de Sarah en el comportamiento de compra sugiere que no está comprándose por sí misma.

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

Como Sarah agregó un artículo de regalo aparente en el carro y lo abandonó, Luma puede destinatario con una oferta de envoltura de regalo gratuita.

## Destinos

Cuando agregó el segmento &quot;Abandonadores de carro de compras de regalos&quot;, puede ver aproximadamente cuántas personas forman parte de este segmento. Puede realizar acciones al respecto y hacer que esté disponible para su personalización en todos los canales.

Haga clic en **[!UICONTROL Enviar a destinos]**.

En Adobe, CDP en tiempo real, Luma puede actuar sin problemas en sus segmentos de audiencia para la personalización.\
Aquí vemos todos los destinos disponibles para que Luma envíe este destino a soluciones tanto de Adobe como de no Adobe:

![imagen](assets/luma-dest.png)

### Selección de destinos

En este escenario, Luma quiere volver a dirigir esta audiencia con personalización en todos estos destinos:

* Google, para visualización

   <!--* Facebook -->
* Adobe Campaign, para correo electrónico

<!-- ![image](assets/luma-sched-dest.png) -->

### Destinos de programación

También puede programar el segmento para que se inicio o finalice en un momento determinado. El segmento se publicará y se actualizará automáticamente en las plataformas configuradas en las fechas programadas.

>[!NOTE]
>
>De forma opcional, si hace clic en el campo de fecha, automáticamente se programan 90 días de espera.

Haga clic en **[!UICONTROL Guardar]** para ir a la página siguiente.

Cuando un cliente de esta audiencia realiza una compra, su pertenencia a esta audiencia se suprime en tiempo real. Ya no cumplen los requisitos porque su estado ha cambiado.

Esto ahorra al director del equipo de medios de Luma cientos de miles de dólares al no usar el inventario para una audiencia que no está calificada.

### Aplicación de directivas de uso de datos para destinos

Adobe Experience Platform incluye controles de seguridad y privacidad para determinar si un segmento está disponible para activarse en un destino determinado. La activación está habilitada o restringida en función de los fines de mercadotecnia asignados al destino cuando se creó, así como de las directivas de uso de datos definidas por su organización.

Si la actividad infringe la política, aparece una advertencia. Esta advertencia contiene información de linaje de datos que puede ayudarle a identificar por qué se violó la política y qué puede hacer para resolver la infracción.

Con estos controles, [!DNL Experience Platform] ayuda a Luma a cumplir con las regulaciones y comercializar de manera responsable. Estos controles son flexibles y pueden modificarse para cumplir con los requisitos de los equipos de seguridad y gobernanza de Luma, permitiéndoles abordar con confianza los requisitos regionales y organizativos para administrar datos conocidos y desconocidos de los clientes.

### Lienzo del flujo de datos

Al guardar, un lienzo de flujo de datos visual muestra el segmento asignado desde el perfil unificado a los tres destinos seleccionados.

![imagen](assets/luma-flow.png)

## Vinculación de identidad entre dispositivos

Sarah explora un sitio de medios sociales en su dispositivo móvil, y ve un anuncio de Luma. Le recuerda el artículo que dejó en su carro.

Más tarde, abre su correo electrónico y ve los mensajes dirigidos a otro objetivo. Ella hace clic en un vínculo a Luma desde un correo electrónico.

El enlace lleva a Sarah a la página de inicio móvil de Luma, donde ve una experiencia altamente personalizada con tecnología de Adobe Target.

* Ella es bienvenida como miembro del Bronce.
* Ella ve el mensaje de &quot;Regalo&quot;.
* También ve el mensaje &quot;Free Gift Wrap&quot; (Envolver regalos gratis), que es parte de sus beneficios de membresía en bronce.
* Todavía está en la imagen de héroe basada en su afinidad por correr.

Ella compra el jersey, agrega envoltura de regalo y escribe una nota de regalo. También tiene la opción de recordar este evento y recibir un recordatorio el año que viene para recibir un regalo en este momento. Ella dice que sí, y está programada en una campaña de correo electrónico el año siguiente para recordarle que compre otro regalo.

Gracias a las capacidades de supresión de audiencias, Sarah no será el objetivo de que el jersey de los hombres avance.

## Análisis del perfil

Los especialistas en mercadotecnia de luminancia utilizan Adobe Experience Platform para ver el segmento de los proveedores de regalos en el Panel CDP en tiempo real. Ellos vista los resultados de esta iniciativa con el tiempo y ven que está creciendo. Los clientes están respondiendo a ofertas y gastando más dinero.

Estas perspectivas permiten a los especialistas en mercadotecnia tomar medidas sobre esta señal, que se alimentó con la disponibilidad de estos datos en CDP y con clientes como Sarah conectados al segmento.

Luma utiliza estos datos CDP para aumentar la lealtad y la satisfacción del cliente.
