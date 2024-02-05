---
title: Complemento de perfiles de origen con atributos proporcionados por socios
description: Aprenda a complementar los perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nuevas perspectivas sobre la base de clientes y mejorar Audience Optimization.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 9737508bd8435f4edf0e60a3559c1b4352ccb29f
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 79%

---

# Complemento de perfiles de origen con atributos proporcionados por socios

>[!AVAILABILITY]
>
>* Esta funcionalidad está disponible para los clientes con licencia de Real-Time CDP (servicio de aplicación), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Obtenga más información acerca de estos paquetes en las [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html?lang=es) y póngase en contacto con el representante de Adobe para obtener más información.

Complemente perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y optimizar mejor los públicos.

![Enriquezca los perfiles con atributos proporcionados por los socios para obtener información general visual de alto nivel sobre los casos de uso.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Por qué considerar este caso de uso {#why-this-use-case}

La mayoría de las marcas, incluso las que son ricas en datos de origen, pueden beneficiarse de la racionalización de sus datos y de obtener una comprensión más matizada de los clientes, sus comportamientos, patrones y preferencias.

Adobe Real-time Customer Data Platform puede ayudar a las marcas a complementar de forma responsable sus datos de origen con información, identificadores y atributos valiosos de uno o más socios de confianza.

El Adobe entiende que no existe un enfoque único que se adapte a todos los casos y permite una interoperabilidad perfecta con los socios de datos e identidades para fomentar una participación individualizada y reflexiva en todas las etapas del ciclo de vida del cliente. Estas capacidades están respaldadas por un marco de trabajo de gobernanza de datos de confianza, que permite un control matizado sobre dónde y cómo se utilizan los datos de los socios. Por ejemplo, es posible que desee utilizar las perspectivas proporcionadas por el socio para la segmentación, pero no para la personalización.

Por ejemplo, siga los pasos descritos en este caso de uso cuando necesite enriquecer los registros de cliente con señales demográficas e intencionales.

## Requisitos previos y planificación

A medida que considere la posibilidad de complementar sus propios perfiles de origen con atributos de socios de datos, debe analizar y abordar los siguientes detalles sobre el bucle de enriquecimiento de datos con el socio de datos:

* Piense en la ubicación donde se exportará la lista de públicos desde Real-Time CDP para compartirla con el proveedor de datos. Esta ubicación debe admitir la exportación de archivos.
* ¿Cuáles son los identificadores que espera el proveedor de datos para que puedan clasificarse en atributos adicionales?
* ¿Cómo se volverá a ingerir en Real-Time CDP el archivo que contiene los atributos proporcionados por el socio? Por ejemplo, los archivos se pueden ingerir a través de conectores de origen de almacenamiento en la nube como [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) o [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* ¿Cuál es la cadencia con la que espera que los atributos proporcionados por el socio se devuelvan a Real-Time CDP y se actualicen?

>[!WARNING]
>
>Los atributos adicionales proporcionados por socios introducidos en Real-Time CDP afectan a su *riqueza del perfil promedio*. Lea la [Descripción del producto de Real-Time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) para obtener más información acerca de la riqueza del perfil.

## Tutorial de vídeo {#video-walkthrough}

Vea el tutorial de vídeo a continuación para ver un tutorial sobre cómo complementar las audiencias de origen con atributos proporcionados por los socios:

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

![Enriquezca los perfiles con atributos proporcionados por los socios para obtener información general visual de alto nivel sobre los casos de uso.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Como **cliente**, adquiere licencias de atributos del **socio de datos**.
2. Como **cliente**, puede ampliar los datos de perfil y el modelo de gobernanza para dar cabida a atributos proporcionados por **socios**.
3. Como **cliente**, incorpora los públicos que desea enriquecer con el socio de datos. Por lo general, estos públicos están marcados por identificadores de entrada, como elementos de información de identificación personal (PII), como correo electrónico, nombre, dirección u otros.
4. El **socio** anexa atributos con licencia para los perfiles con los que pueden coincidir. Opcionalmente, un [ID de socio](/help/identity-service/features/namespaces.md) se puede incluir e ingerir en el área de nombres de ID con ámbito de socio.
5. Como **cliente**, carga atributos del socio de datos en perfiles de clientes en Real-Time CDP.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Atributos de licencia del socio {#license-attributes-from-partner}

Este paso se trata en los [requisitos previos](#prerequisites-and-planning) y Adobe supone que dispone de los acuerdos contractuales adecuados con proveedores de datos de confianza para aumentar sus perfiles de origen.

### Amplíe los datos de perfil y el modelo de gobernanza para dar cabida a los atributos proporcionados por los socios. {#extend-governance-model}

En este punto, está ampliando el marco de trabajo de administración de datos en Real-Time CDP para dar cabida a los atributos proporcionados por los socios.

Tiene la opción de crear un nuevo esquema de la clase **[!UICONTROL Perfil individual de XDM]** o ampliar un esquema existente del mismo tipo para incluir atributos proporcionados por socios. Adobe recomienda encarecidamente crear un esquema con un nuevo conjunto de grupos de campos que representen mejor los atributos adicionales del proveedor de datos. Esto garantiza que los esquemas de datos estén limpios y puedan evolucionar de forma independiente entre sí.

Para incluir atributos proporcionados por el socio en un esquema, puede crear un nuevo grupo de campos con los atributos esperados o emplear uno de los grupos de campos preconfigurados proporcionados por Adobe.

Lea las páginas de documentación siguientes para obtener más información:

* [Conceptos básicos de composición de esquemas](/help/xdm/schema/composition.md)
* [Información general de la clase [!UICONTROL Perfil individual de XDM]](/help/xdm/classes/individual-profile.md)
* [Creación y edición de esquemas en la IU](/help/xdm/ui/resources/schemas.md)
* [Creación y edición de grupos de campos de esquema en la IU](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

También en este paso, piense en cómo cambia el modelo de gobernanza de datos a medida que amplía su estrategia de administración de datos para incluir datos de terceros proporcionados por el socio. Explore las consideraciones de los vínculos de documentación siguientes:

* (**Muy pronto**) Mantenga los datos de terceros en un conjunto de datos independiente para que sea fácil eliminarlos y deshacer integraciones.
* (**Muy pronto**) Use la funcionalidad de [caducidad del conjunto de datos](/help/hygiene/ui/dataset-expiration.md) en el conjunto de datos para clientes que compraron el complemento de higiene.
* (**Muy pronto**) Tenga cuidado al crear conjuntos de datos derivados que extraen datos de terceros, ya que, una vez mezclados, la única solución para quitar los datos de terceros es eliminar todo el conjunto de datos derivado.

>[!TIP]
>
>Si decide complementar los perfiles del cliente con un identificador basado en personas del proveedor de datos, puede crear un nuevo tipo de identidad de **[[!UICONTROL ID de socio]](/help/identity-service/features/namespaces.md)**.
>
>Obtenga más información acerca del ID de socio en la [sección tipos de identidad](/help/identity-service/features/namespaces.md).
>Lea acerca de [cómo definir campos de identidad](/help/xdm/ui/fields/identity.md) en la interfaz de usuario de Experience Platform.

### Exporte públicos que desee enriquecer cuando se introduzca información de identificación personal (PII) o PII con hash {#export-audiences}

Exporte los públicos que desea que el socio enriquezca. Utilice los destinos de almacenamiento en la nube proporcionados por Real-Time CDP, como Amazon S3 o SFTP. Lea las siguientes páginas de documentación para completar este paso:

* Página de documentación de [destino de Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* Página de documentación de [Destino SFTP](/help/destinations/catalog/cloud-storage/sftp.md)
* Cómo [conectar a un destino](/help/destinations/ui/connect-destination.md)
* Cómo [exportar datos a un destino de almacenamiento en la nube](/help/destinations/ui/activate-batch-profile-destinations.md)

### Su socio de datos adjunta atributos con licencia para los perfiles con los que pueden coincidir {#partner-appends-attributes}

En este paso, el socio de datos anexa atributos con licencia para el público exportado. La salida suele estar disponible como archivo plano que se puede volver a introducir en Real-Time CDP. Más información acerca de la [ingesta de archivos en Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP anexa atributos enriquecidos al perfil del cliente {#ingest-data}

Ahora necesita ingerir los datos del socio a través del conector de origen para devolver los datos enriquecidos a Real-Time CDP y complementar sus perfiles con datos proporcionados por socios.

Algunos conectores de origen recomendados para este fin pueden ser los siguientes:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitaciones y solución de problemas {#limitations-and-troubleshooting}

Tenga en cuenta las siguientes limitaciones a medida que explora el caso de uso descrito en esta página:

* Si decide utilizar ID de socios, tenga en cuenta que estos no se utilizan para crear su [gráfico de identidad](/help/identity-service/features/identity-graph-viewer.md).

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* Utilice la compatibilidad con datos de terceros en Real-Time CDP para [ampliar su base de perfiles con perfiles potenciales de socios de datos y participe con ellos para adquirir o llegar a nuevos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Personalice experiencias en el sitio para visitantes desconocidos mediante el reconocimiento de visitantes asistido por socios](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita sin que el usuario se autentique ni tenga historial previo con su marca.
* [Activación ampliada de perfiles y audiencias de clientes potenciales](/help/destinations/ui/activate-prospect-audiences.md) para seleccionar destinos.
