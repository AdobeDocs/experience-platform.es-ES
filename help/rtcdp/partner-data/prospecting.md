---
title: Interactúe y adquiera nuevos clientes sin depender de cookies de terceros
description: Aprenda a atraer y adquirir nuevos clientes a través de casos de uso de prospección, sin depender de cookies de terceros.
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: 645295958ea6f94a9f9da13517b0fa1d02010b52
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 85%

---

# Interactúe y adquiera nuevos clientes sin depender de cookies de terceros

>[!AVAILABILITY]
>
>* Esta funcionalidad está disponible para los clientes con licencia de Real-Time CDP (servicio de aplicación), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Obtenga más información acerca de estos paquetes en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) y póngase en contacto con el representante de Adobe para obtener más información.

Utilice la compatibilidad con datos de terceros en Real-Time CDP para ampliar su base de perfiles con perfiles potenciales de socios de datos y comprometerse con ellos para adquirir o llegar a nuevos clientes.

![Información general visual de alto nivel sobre los casos de uso de prospección de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Por qué considerar este caso de uso {#why-this-use-case}

Las marcas se enfrentan simultáneamente a enormes desafíos al ejecutar de forma responsable los casos de uso de adquisición de clientes principales sin depender de cookies de terceros, presupuestos limitados y una mayor demanda de transparencia y retorno de la inversión publicitaria.

Adobe Real-time Customer Data Platform puede ayudar a las marcas a realizar una transición segura de los casos de uso admitidos de Data Management Platform (DMP) a alternativas sin cookies y hacerlo de una manera que afirme la sofisticación y la potencia completas de la segmentación de autoservicio, la depuración de audiencias y la activación en un solo sistema. Todo sin comprometer el enfoque inquebrantable de Adobe en el uso responsable de los datos a través de un marco patentado de gobernanza de datos y consentimiento.

Por ejemplo, siga los pasos descritos en este caso de uso cuando necesite ejecutar una campaña para atraer clientes potenciales para que se conviertan en usuarios o clientes conocidos.

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando considere la posibilidad de ponerse en contacto con clientes nuevos y adquirirlos, tenga en cuenta los siguientes requisitos previos en el proceso de planificación:

* ¿Cuál es la cadencia con la que espera que los atributos proporcionados por el socio se incorporen a Real-Time CDP y se actualicen?
* ¿Qué identidades requieren sus destinos descendentes?
* Asegúrese de que los identificadores introducidos sean procesables de forma descendente
* ¿Los datos del socio que está ingiriendo están vinculados a un identificador duradero ampliamente aceptado, como información de identificación personal (PII), PII con hash o un identificador de socio?
* ¿Qué políticas de uso de datos debe conocer desde la perspectiva del socio y de su propio equipo jurídico, de privacidad o de cumplimiento?

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

Antes de expandir Real-Time CDP para atraer y adquirir nuevos clientes, asegúrese de utilizar Real-Time CDP para crear una base sólida para los datos de origen. Los flujos de trabajo para lograr este caso de uso son similares a los flujos de trabajo para interactuar con los clientes conocidos.

![Resumen visual de alto nivel sobre casos de uso de prospección de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Como **cliente** obtiene la licencia de perfiles de clientes potenciales de uno o más **socios de datos** para impulsar la adquisición de clientes de canal.
2. Como **cliente**, puede ampliar los datos de perfil y el modelo de gobernanza para ingerir la lista de perfiles de clientes potenciales proporcionada por el **socio**.
3. Como **cliente**, puede cargar perfiles de clientes potenciales en Real-Time CDP y crear políticas de gobernanza para garantizar un uso responsable.
4. Como **cliente**, los públicos se crean a partir de la lista de perfiles de clientes potenciales.
5. Como **cliente**, activa los públicos de clientes potenciales a destinos que aceptan las identidades disponibles en la lista de clientes potenciales.
6. Si es necesario, trabaje con el **socio de datos** para la activación en la recta final de públicos a destinos de medios de pago deseados.

## Tutorial de vídeo {#video-walkthrough}

Vea el tutorial en vídeo a continuación para obtener una descripción detallada de cómo llegar a las audiencias de clientes potenciales y participar en ellas:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Funcionalidades y elementos de la interfaz de usuario que utilizará {#ui-functionality-and-elements}

A medida que complete los pasos para implementar el caso de uso, utilizará las siguientes funciones y elementos de la interfaz de usuario de Real-Time CDP (indicados en el orden en que los usará). Asegúrese de que dispone de los permisos de control de acceso basados en atributos necesarios para todas estas áreas o pídale al administrador del sistema que le otorgue los permisos necesarios.

* [Identidades](/help/identity-service/namespaces.md)
* [Esquemas](/help/xdm/home.md)
* [Etiquetas de uso de datos](/help/data-governance/labels/overview.md)
* [Conjuntos de datos](/help/catalog/datasets/overview.md)
* [Fuentes](/help/sources/home.md)
* [Perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md)
* [Audiencias potenciales](/help/segmentation/ui/prospect-audience.md)
* [Destinos](/help/destinations/home.md)

### Detalles del perfil de terceros de licencia del socio {#license-profiles-from-partner}

Este paso se trata en los [requisitos previos](#prerequisites-and-planning) y Adobe supone que dispone de los acuerdos contractuales adecuados con proveedores de datos de confianza para ingerir perfiles de clientes potenciales proporcionados por el socio de datos.

### Amplíe sus datos de perfil y su modelo de gobernanza para dar cabida a los perfiles de clientes potenciales proporcionados por el socio {#extend-governance-model}

Como preparación para recibir perfiles potenciales de su socio de datos, debe ampliar el marco de trabajo de administración de datos en Real-Time CDP para dar cabida a este nuevo tipo de perfil.

Los componentes de identidad, administración de datos y control que utilizará son los siguientes:

* Un nuevo tipo de identidad de **[!UICONTROL ID de socio]** de los perfiles proporcionados por el socio
* Una nueva clase XDM del **[!UICONTROL Perfil de cliente potencial individual de XDM]**
* **(Documentación próximamente)** Grupos de campo adaptados para el soporte de datos del socio
* **(Documentación próximamente)** Etiquetas de terceros que añadirá a los atributos procedentes de socios

#### Crear un área de nombres de identidad de ID de socio {#create-partner-id-namespace}

Comience creando un nuevo tipo de identidad para los perfiles que recibirá del socio. Para ello, en la sección Identidad, debe crear una nueva área de nombres de identidad del tipo **[!UICONTROL ID de socio]**.

![Cree una nueva área de nombres de identidad de ID de socio.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Obtenga más información acerca del ID de socio en la [sección tipos de identidad](/help/identity-service/namespaces.md).
* Lea acerca de [cómo definir campos de identidad](/help/xdm/ui/fields/identity.md) en la interfaz de usuario de Experience Platform.

#### Cree un nuevo esquema con la clase **[!UICONTROL Perfil de cliente potencial individual de XDM]**

 A continuación, en **[!UICONTROL Administración de datos]** > **[!UICONTROL Esquemas]**, cree un nuevo esquema y asígnele la clase **[!UICONTROL Perfil de cliente potencial individual de XDM]**.

![Busque la clase de perfil de cliente potencial individual de XDM en el generador de esquemas XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lea cómo [crear y editar esquemas en la interfaz de usuario](/help/xdm/ui/resources/schemas.md) y obtenga información completa sobre la clase de perfil de cliente potencial individual de XDM (próximo vínculo).

El **[!UICONTROL Perfil de cliente potencial individual de XDM]** viene preconfigurado con los campos que se muestran a continuación. Para enriquecer el esquema con atributos proporcionados por el socio para los perfiles de clientes potenciales, puede crear un nuevo grupo de campos con los atributos que espera y añadirlo al esquema o puede utilizar uno de los grupos de campos preconfigurados que proporciona Adobe.

![Campos preconfigurados para la clase de perfil de cliente potencial individual de XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

A continuación, debe seleccionar la identidad de ID de socio que creó anteriormente como identidad principal para el esquema. Los registros de perfil deben llevar un identificador principal. Este paso es necesario para asegurarse de que los datos del cliente potencial se puedan cargar en el almacén de perfiles y estén disponibles para la segmentación y activación.

>[!AVAILABILITY]
>
>Los perfiles de clientes potenciales están restringidos automáticamente para utilizar únicamente áreas de nombres de ID del tipo ID de socio. Esto es por diseño y garantiza una separación limpia entre los perfiles de origen y los perfiles potenciales.

![Seleccione el ID de socio configurado anteriormente como identidad principal en el esquema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Tenga en cuenta que el esquema aún no está habilitado para el perfil. Cambie el botón de perfil para habilitar este esquema para su inclusión en el servicio de perfil. Para obtener más información sobre la activación del esquema para su uso en el perfil del cliente en tiempo real, lea el [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilitar esquema para perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Añada la etiqueta de control de datos de terceros a todos los campos del esquema

Considere la posibilidad de añadir etiquetas de control de datos de terceros a todos los campos que conforman el esquema. Esto es importante para garantizar un uso responsable de los datos de terceros y minimizar el riesgo de fuga de datos. Encuentre más información sobre [etiquetas de gobernanza de datos de terceros](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Para realizar esto, siga los pasos a continuación:

1. Vaya al esquema que ha creado y seleccione la pestaña **[!UICONTROL Etiquetas]**.
2. Seleccione todos los campos de este esquema con el botón de casilla de verificación en la parte superior y, a continuación, haga clic en el icono de lápiz a la derecha para aplicar las etiquetas de control de datos a este esquema.
3. Seleccione la etiqueta **[!UICONTROL Ecosistema de socios]** de las categorías de la izquierda.
4. Elija la etiqueta llamada **[!UICONTROL Terceros]** y seleccione **[!UICONTROL Guardar]**.
5. Tenga en cuenta que todos los campos del esquema llevan ahora la etiqueta seleccionada en el paso anterior.

>[!SUCCESS]
>
>El esquema ya está listo para usarse y puede continuar con el siguiente paso para introducir datos de clientes potenciales de su socio de datos.

También en este paso, piense en cómo cambia el modelo de gobernanza de datos a medida que amplía su estrategia de administración de datos para incluir datos de terceros proporcionados por el socio. Explore las consideraciones de los vínculos de documentación siguientes:

* (**Muy pronto**) Mantenga los datos de terceros en un conjunto de datos independiente para que sea fácil eliminarlos y deshacer integraciones.
* (**Muy pronto**) Use la funcionalidad de [caducidad del conjunto de datos](/help/hygiene/ui/dataset-expiration.md) en el conjunto de datos para clientes que compraron el complemento de higiene.
* (**Muy pronto**) Tenga cuidado al crear conjuntos de datos derivados que extraen datos de terceros, ya que, una vez mezclados, la única solución para quitar los datos de terceros es eliminar todo el conjunto de datos derivado.

### Cargue la lista de perfiles de clientes potenciales e inspeccione la vista de perfiles de clientes potenciales

Después de preparar el modelo de datos para administrar los perfiles de los clientes potenciales, es hora de introducir los datos.

#### Crear un conjunto de datos y cargar datos de clientes potenciales de muestra

Para cargar algunos datos de ejemplo y rellenar perfiles de clientes potenciales, cree un conjunto de datos y cargue un archivo que haya recibido del socio de datos. Siga estos pasos:

1. Vaya a **[!UICONTROL Administración de datos]** > **[!UICONTROL Conjuntos de datos]** y seleccione **[!UICONTROL Crear conjunto de datos]**.
2. Seleccione Crear conjunto de datos a partir de esquema
3. Seleccione el esquema que ha creado en un paso anterior
4. Asigne un nombre al conjunto de datos y, opcionalmente, una descripción.
5. Seleccione **[!UICONTROL Finalizar]**.

![Un registro de los pasos para crear un conjunto de datos para perfiles de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Tenga en cuenta que, de forma similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el perfil del cliente en tiempo real. Para obtener más información sobre la activación del conjunto de datos para su uso en el Perfil del cliente en tiempo real, lea el [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilitar conjunto de datos para el perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Para cargar un archivo que haya recibido del socio en el conjunto de datos, seleccione el conjunto de datos, desplácese hacia abajo en el carril derecho y seleccione **[!UICONTROL Añadir datos]**. Puede arrastrar y soltar el archivo o seleccionar **[!UICONTROL Elegir archivos]** para ir a la ubicación del archivo y seleccionarlo.

![Añadir archivo al conjunto de datos.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Después de cargar la lista de perfiles del socio de datos en Real-Time CDP, continúe con la [sección Inspeccionar los perfiles de clientes potenciales cargados](#inspect-profiles) para comprobar que los perfiles de clientes potenciales se están rellenando en la interfaz de usuario.

#### Ingesta de datos de clientes potenciales mediante conectores de origen

Puede configurar importaciones recurrentes de archivos para introducir datos del socio a través de un conector de origen y llevar la lista de perfiles potenciales a Real-Time CDP.

A continuación se enumeran algunos conectores de origen recomendados para este fin, pero tenga en cuenta que cualquier método de ingesta basado en archivos en Real-Time CDP funciona para su propósito.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Después de cargar la lista de perfiles del socio de datos en Real-Time CDP, continúe con la siguiente sección para comprobar que los perfiles de clientes potenciales se están rellenando en la interfaz de usuario.

#### Inspeccionar los perfiles de clientes potenciales cargados {#inspect-profiles}

Para ver la lista de perfiles de clientes potenciales, vaya a **[!UICONTROL Clientes potenciales]** > **[!UICONTROL Perfiles]** en el carril izquierdo.

Tenga en cuenta que los perfiles de clientes potenciales que acaba de cargar en Real-Time CDP pueden tardar hasta dos horas en mostrarse en la vista **[!UICONTROL Examinar]** de la pantalla Perfil de cliente potencial. Si la página muestra el mensaje “No hay perfiles de clientes potenciales para examinar en este momento”, vuelva a intentarlo después de un tiempo. Después de esperar un poco, los perfiles de los clientes potenciales deberían empezar a aparecer en la vista **[!UICONTROL Examinar]**.

>[!TIP]
>
>Tenga en cuenta la presencia de la columna **[!UICONTROL Área de nombres de identidad]**. Si trabaja con varios proveedores de datos, utilice esta columna para deducir el origen de los perfiles de clientes potenciales.

![Vista de los perfiles de clientes potenciales cargados en Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

También puede seleccionar cualquier perfil de cliente potencial para realizar una inspección adicional, tal como se muestra a continuación.

![Vista de cómo inspeccionar perfiles de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Más información sobre [perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md).

### Crear públicos de clientes potenciales {#create-prospect-audiences}

Utilice la funcionalidad de segmentación de Real-Time CDP para crear públicos a partir de los perfiles de clientes potenciales. Utilice las reglas de segmentación deseadas para crear públicos adaptados.

Para empezar y crear públicos compuestos de perfiles de clientes potenciales, vaya a **[!UICONTROL Clientes potenciales]** > **[!UICONTROL Públicos]**.

![Vista del público de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Tenga en cuenta que la experiencia de creación de públicos para perfiles de clientes potenciales difiere de la experiencia para crear públicos de sus clientes de origen conocidos. Esta vista se limita a lo siguiente:

* Atributos de la clase de cliente potencial que creó anteriormente.
* Solo evaluación del perfil del lote.
* No admite la creación de públicos basados en eventos de series de tiempo.

Más información sobre [audiencias de clientes potenciales](/help/segmentation/ui/prospect-audience.md).

### Activar perfiles de clientes potenciales en destinos {#activate-to-destinations}

Utilice los públicos de clientes potenciales exportándolos a destinos. Actualmente, solo ciertos destinos de almacenamiento en la nube admiten la activación de perfiles potenciales.

![Destinos que admiten audiencias de clientes potenciales.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Más información](/help/destinations/ui/activate-prospect-audiences.md) acerca de la activación de clientes potenciales en destinos de almacenamiento en la nube.

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* [Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Personalice experiencias en el sitio para visitantes desconocidos mediante el reconocimiento de visitantes asistido por socios](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita sin que el usuario se autentique ni tenga historial previo con su marca.
* [Activación ampliada de perfiles y audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md) para seleccionar destinos.
