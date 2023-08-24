---
title: Capte y adquiera nuevos clientes a través de casos de uso de prospección
description: Aprenda a atraer y adquirir nuevos clientes a través de casos de uso de prospección, habilitados por la compatibilidad con datos de socios en Real-Time CDP.
source-git-commit: 9dd305be4dcb45c290a2b8ee0476191949369adc
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 14%

---

# Capte y adquiera nuevos clientes a través de casos de uso de prospección

>[!AVAILABILITY]
>
>* La funcionalidad está disponible para los clientes con licencia de Real-Time CDP (servicio de aplicaciones), Activación de Adobe Experience Platform, Real-Time CDP, Real-Time CDP Prime y Real-Time CDP Ultimate. Obtenga más información acerca de estos paquetes en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) y póngase en contacto con el representante de Adobe para obtener más información.

Utilice la compatibilidad con datos de terceros en Real-Time CDP para ampliar su base de perfiles con perfiles potenciales de socios de datos y comprometerse con ellos para adquirir o llegar a nuevos clientes.

![Resumen visual de alto nivel del caso de uso de prospección de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando considere la posibilidad de ponerse en contacto con los clientes nuevos y adquirirlos mediante la compatibilidad con datos de socios en Real-Time CDP, tenga en cuenta los siguientes requisitos previos en el proceso de planificación:

* ¿Cuál es la cadencia con la que espera que los perfiles proporcionados por el socio se introduzcan en Real-Time CDP y se actualicen?
* ¿Qué identidades requieren sus destinos descendentes?
* Asegúrese de que los identificadores introducidos sean procesables de forma descendente
* ¿Los datos del socio que está ingiriendo están vinculados a un identificador duradero ampliamente aceptado, como información de identificación personal (PII), PII con hash o un identificador de socio?
* ¿Qué políticas de uso de datos debe tener en cuenta desde la perspectiva del socio y desde su propio equipo legal, de privacidad o de cumplimiento?

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

Antes de expandir Real-Time CDP para atraer y adquirir nuevos clientes, asegúrese de utilizar Real-Time CDP para crear una base sólida para los datos de origen. Los flujos de trabajo para lograr este caso de uso son similares a los flujos de trabajo para interactuar con los clientes conocidos.

![Resumen visual de alto nivel del caso de uso de prospección de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. As a **cliente**, obtiene la licencia de perfiles de clientes potenciales de uno o más **socios de datos** para ayudar a impulsar la adquisición de clientes de canal.
2. As a **cliente**, puede ampliar los datos de perfil y el modelo de gobernanza para introducir la variable **socio** Lista proporcionada por el cliente de perfiles de clientes potenciales.
3. As a **cliente**, puede cargar perfiles de clientes potenciales en Real-Time CDP y crear políticas de gobernanza para garantizar un uso responsable.
4. As a **cliente**, las audiencias se crean a partir de la lista de perfiles de clientes potenciales.
5. As a **cliente**, activa las audiencias de clientes potenciales a destinos que aceptan las identidades disponibles en la lista de clientes potenciales.
6. Si es necesario, trabaje con **socio de datos** para la activación de audiencias de última milla a destinos de medios de pago deseados.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Funcionalidad y elementos de la interfaz de usuario que utilizará {#ui-functionality-and-elements}

A medida que complete los pasos para implementar el caso de uso, utilizará las siguientes funciones y elementos de la interfaz de usuario de Real-Time CDP (enumerados en el orden en que los usará). Asegúrese de que dispone de los permisos de control de acceso basados en atributos necesarios para todas estas áreas o pídale al administrador del sistema que le conceda los permisos necesarios.

* [Identidades](/help/identity-service/namespaces.md)
* [Esquemas](/help/xdm/home.md)
* [Etiquetas de uso de datos](/help/data-governance/labels/overview.md)
* [Conjuntos de datos](/help/catalog/datasets/overview.md)
* [Fuentes](/help/sources/home.md)
* [Perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md)
* [Audiencias potenciales](/help/segmentation/ui/prospect-audience.md)
* [Destinos](/help/destinations/home.md)

### Detalles del perfil de terceros de licencia del socio {#license-profiles-from-partner}

Este paso se trata en la [requisitos previos](#prerequisites-and-planning) El Adobe de y supone que dispone de los acuerdos contractuales adecuados con proveedores de datos de confianza para introducir perfiles de clientes potenciales proporcionados por el socio de datos.

### Amplíe los datos de perfil y el modelo de control para dar cabida a los perfiles de clientes potenciales proporcionados por los socios {#extend-governance-model}

Como preparación para recibir perfiles potenciales de su socio de datos, debe ampliar el marco de trabajo de administración de datos en Real-Time CDP para dar cabida a este nuevo tipo de perfil.

Los componentes de identidad, administración de datos y control que utilizará son los siguientes:

* Un nuevo **[!UICONTROL ID de socio]** tipo de identidad de los perfiles proporcionados por el socio
* Un nuevo **[!UICONTROL Perfil de cliente potencial individual XDM]** clase XDM
* **(Documentación próximamente)** Grupos de campo adaptados para el soporte de datos de socios
* **(Documentación próximamente)** Etiquetas de terceros que agregará a los atributos procedentes de socios

#### Crear un área de nombres de identidad de ID de socio {#create-partner-id-namespace}

Comience creando un nuevo tipo de identidad para los perfiles que recibirá del socio. Para ello, en la sección Identity, debe crear un nuevo área de nombres de identidad del tipo **[!UICONTROL ID de socio]**.

![Cree un nuevo área de nombres de identidad de ID de socio.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Obtenga más información acerca de las áreas de nombres de ID de socio en la [sección tipos de identidad](/help/identity-service/namespaces.md).
* Lea acerca de [cómo definir campos de identidad](/help/xdm/ui/fields/identity.md) en la interfaz de usuario de Experience Platform.

#### Cree un nuevo esquema con **[!UICONTROL Perfil de cliente potencial individual XDM]** clase

Siguiente, en **[!UICONTROL Administración de datos]** > **[!UICONTROL Esquemas]**, cree un nuevo esquema y asígnele el **[!UICONTROL Perfil de cliente potencial individual XDM]** clase.

![Busque la clase de perfil de cliente potencial individual XDM en el generador de esquemas XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lea cómo [crear y editar esquemas en la interfaz de usuario](/help/xdm/ui/resources/schemas.md) y obtenga información completa sobre la clase de perfil de cliente potencial individual de XDM (vínculo previsto).

El **[!UICONTROL Perfil de cliente potencial individual XDM]** viene preconfigurado con los campos que se muestran a continuación. Para enriquecer el esquema con atributos proporcionados por el socio para los perfiles del cliente potencial, puede crear un nuevo grupo de campos con los atributos que espera y agregarlo al esquema o puede utilizar uno de los grupos de campos preconfigurados proporcionados por Adobe.

![Campos preconfigurados para la clase de perfil de cliente potencial individual XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

A continuación, debe seleccionar la identidad de ID de socio que creó anteriormente como identidad principal para el esquema. Los registros de perfil deben llevar un identificador principal. Este paso es necesario para asegurarse de que los datos del cliente potencial se pueden cargar en el almacén de perfiles y estar disponibles para la segmentación y activación.

>[!AVAILABILITY]
>
>Los perfiles de clientes potenciales están restringidos automáticamente para utilizar únicamente áreas de nombres de ID del tipo ID de socio. Esto es por diseño y garantiza una separación limpia entre los perfiles de origen y los perfiles potenciales.

![Seleccione el ID de socio configurado anteriormente como identidad principal en el esquema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Tenga en cuenta que el esquema aún no está habilitado para el perfil. Cambie el botón de perfil para habilitar este esquema para su inclusión en el servicio de perfil. Para obtener más información sobre la activación del esquema para su uso en el Perfil del cliente en tiempo real, lea la [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilitar esquema para perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Agregue la etiqueta de control de datos de terceros a todos los campos del esquema

Considere la posibilidad de agregar etiquetas de gobernanza de datos de terceros a todos los campos que conforman el esquema. Esto es importante para garantizar un uso responsable de los datos de terceros y minimizar el riesgo de fuga de datos. Encuentre más información sobre las etiquetas de gobernanza de datos de terceros (añada un vínculo a documentos de Jordan)

Para realizar esto, siga los pasos a continuación:

1. Vaya al esquema que ha creado y seleccione. **[!UICONTROL Etiquetas]** pestaña.
2. Seleccione todos los campos de este esquema con el botón de casilla de verificación en la parte superior y, a continuación, haga clic en el icono de lápiz a la derecha para aplicar etiquetas de control de datos a este esquema.
3. Seleccione el **[!UICONTROL Ecosistema de partners]** Etiqueta de las categorías de la izquierda.
4. Elija la etiqueta llamada **[!UICONTROL Terceros]** y seleccione **[!UICONTROL Guardar]**.
5. Tenga en cuenta que todos los campos del esquema ahora llevan la etiqueta seleccionada en el paso anterior.

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

Para cargar algunos datos de ejemplo y rellenar perfiles de clientes potenciales, cree un conjunto de datos y cargue un archivo que haya recibido del socio de datos. Complete los pasos siguientes:

1. Vaya a **[!UICONTROL Administración de datos]** > **[!UICONTROL Conjuntos de datos]** y seleccione **[!UICONTROL Crear conjunto de datos]**.
2. Seleccione Crear conjunto de datos a partir de esquema
3. Seleccione el esquema que ha creado en un paso anterior
4. Asigne un nombre al conjunto de datos y, opcionalmente, una descripción.
5. Seleccione **[!UICONTROL Finalizar]**.

![Un registro de los pasos para crear un conjunto de datos para perfiles de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Tenga en cuenta que, de forma similar al paso para crear un esquema, debe habilitar el conjunto de datos para que se incluya en el perfil del cliente en tiempo real. Para obtener más información sobre la activación del conjunto de datos para su uso en el Perfil del cliente en tiempo real, lea la [tutorial de creación de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilite el conjunto de datos para el perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Para cargar un archivo que haya recibido del socio en el conjunto de datos, seleccione el conjunto de datos, desplácese hacia abajo en el carril derecho y seleccione **[!UICONTROL Añadir datos]**. Puede arrastrar y soltar el archivo o seleccionar **[!UICONTROL Elegir archivos]** para ir a la ubicación del archivo y seleccionarlo.

![Agregar archivo al conjunto de datos.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Después de cargar la lista de perfiles del socio de datos en Real-Time CDP, continúe con la [Inspect la sección de perfiles de clientes potenciales cargados](#inspect-profiles) para comprobar que los perfiles del cliente potencial se están rellenando en la interfaz de usuario.

#### Ingesta de datos de clientes potenciales mediante conectores de origen

Puede configurar importaciones recurrentes de archivos para introducir datos del socio a través de un conector de origen e introducir la lista de perfiles potenciales en Real-Time CDP.

A continuación se enumeran algunos conectores de origen recomendados para este fin, pero tenga en cuenta que cualquier método de ingesta basado en archivos en Real-Time CDP funciona para su propósito.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Después de cargar la lista de perfiles del socio de datos en Real-Time CDP, continúe con la siguiente sección para comprobar que los perfiles del cliente potencial se están rellenando en la interfaz de usuario.

#### Inspect los perfiles de clientes potenciales cargados {#inspect-profiles}

Para ver la lista de perfiles de clientes potenciales, vaya a **[!UICONTROL Posibles clientes]** > **[!UICONTROL Perfiles]** en el carril izquierdo.

Tenga en cuenta que los perfiles de clientes potenciales que acaba de cargar en Real-Time CDP pueden tardar hasta dos horas en mostrarse en la **[!UICONTROL Examinar]** Vista de la pantalla Perfil del cliente potencial. Si la página muestra el mensaje &quot;No hay perfiles de cliente potencial para examinar en este momento&quot;, vuelva a intentarlo después de un tiempo. Después de un poco de espera, los perfiles de los posibles clientes deberían empezar a aparecer en la **[!UICONTROL Examinar]** vista.

>[!TIP]
>
>Tenga en cuenta la presencia de **[!UICONTROL Área de nombres de identidad]** columna. Si trabaja con varios proveedores de datos, utilice esta columna para deducir el origen de los perfiles del cliente potencial.

![Vista de los perfiles de clientes potenciales cargados en Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

También puede seleccionar cualquier perfil de cliente potencial para realizar una inspección adicional, como se muestra a continuación.

![Vista de cómo inspeccionar perfiles de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Más información sobre [perfiles de clientes potenciales](/help/profile/ui/prospect-profile.md).

### Crear audiencias de clientes potenciales {#create-prospect-audiences}

Utilice la funcionalidad de segmentación de Real-Time CDP para crear audiencias a partir de los perfiles de clientes potenciales. Utilice las reglas de segmentación deseadas para crear audiencias adaptadas.

Para empezar y crear audiencias compuestas de perfiles de clientes potenciales, vaya a **[!UICONTROL Posibles clientes]** > **[!UICONTROL Audiencias]**.

![Vista de audiencias de clientes potenciales.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Tenga en cuenta que la experiencia de creación de audiencias para perfiles de clientes potenciales difiere de la experiencia para crear audiencias de sus clientes de origen conocidos. Esta vista se limita a:

* Atributos de la clase de cliente potencial que creó anteriormente.
* Solo evaluación del perfil del lote.
* No admite la creación de audiencias basadas en eventos de series temporales.

Más información sobre [audiencias de clientes potenciales](/help/segmentation/ui/prospect-audience.md).

### Activar perfiles de clientes potenciales en destinos {#activate-to-destinations}

Utilice las audiencias de clientes potenciales exportándolas a destinos. Actualmente, solo determinados destinos como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) o el [!BADGE Alfa]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) compatibilidad de destino activación de perfiles de clientes potenciales.

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* [Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Aproveche el reconocimiento asistido por socios para personalizar las experiencias en el sitio](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita sin que el usuario se autentique ni tenga historial previo con su marca.
* [Activación ampliada de perfiles y audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md) para seleccionar destinos.