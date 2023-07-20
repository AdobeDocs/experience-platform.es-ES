---
title: (Beta) Complementar perfiles de origen con atributos proporcionados por los socios
description: Aprenda a complementar los perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nuevas perspectivas sobre la base de clientes y mejorar la optimización de audiencias.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Complementar perfiles de origen con atributos proporcionados por el socio

>[!AVAILABILITY]
>
>* Esta funcionalidad beta está disponible para los clientes con licencia de Real-Time CDP (servicio de aplicaciones), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Obtenga más información sobre estos paquetes en la [descripciones de productos](https://helpx.adobe.com/legal/product-descriptions.html) y póngase en contacto con el representante del Adobe para obtener más información.

Complementa perfiles de origen con atributos de socios de datos de confianza para mejorar la base de datos, obtener nueva información sobre la base de clientes y obtener una mejor optimización de audiencia.

![Enriquezca los perfiles con atributos proporcionados por los socios para obtener información general visual de alto nivel sobre los casos de uso.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Requisitos previos y planificación {#prerequisites-and-planning}

A medida que considere la posibilidad de complementar sus propios perfiles de origen con atributos de socios de datos, debe analizar y abordar los siguientes detalles sobre el bucle de enriquecimiento de datos con el socio de datos:

* Piense en la ubicación donde se exportará la lista de audiencias desde Real-Time CDP para compartirla con el proveedor de datos. Esta ubicación debe admitir la exportación de archivos.
* ¿Cuáles son los identificadores que espera el proveedor de datos para que puedan clasificarse en atributos adicionales?
* ¿Cómo se volverá a introducir en Real-Time CDP el archivo que contiene los atributos proporcionados por el socio? Por ejemplo, los archivos se pueden ingerir a través de conectores de origen de almacenamiento en la nube como [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) o [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* ¿Cuál es la cadencia con la que espera que los atributos proporcionados por el socio se devuelvan a Real-Time CDP y se actualicen?

>[!WARNING]
>
>Los atributos adicionales proporcionados por el socio introducidos en Real-Time CDP afectan a su *riqueza promedio de perfiles*. Lea el [Descripción del producto de Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) para obtener más información sobre la riqueza de perfiles.

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

![Enriquezca los perfiles con atributos proporcionados por los socios para obtener información general visual de alto nivel sobre los casos de uso.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. As a **cliente**, los atributos de licencia del **socio de datos**.
2. As a **cliente**, puede ampliar los datos de perfil y el modelo de gobernanza para dar cabida a **socio** Atributos proporcionados por.
3. As a **cliente**, incorporará las audiencias que desea enriquecer con el socio de datos. Por lo general, estas audiencias están marcadas por identificadores de entrada como elementos de información de identificación personal (PII) como correo electrónico, nombre, dirección u otros.
4. El **socio** anexa atributos con licencia para los perfiles con los que pueden coincidir. Opcionalmente, una [ID de socio](/help/identity-service/namespaces.md) se puede incluir e ingerir en el área de nombres de ID con ámbito de socio.
5. As a **cliente**, puede cargar atributos del socio de datos en perfiles de clientes en Real-Time CDP.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la descripción general de alto nivel anterior.

### Atributos de licencia del socio {#license-attributes-from-partner}

Este paso se trata en la [requisitos previos](#prerequisites-and-planning) y el Adobe de supone que dispone de los acuerdos contractuales adecuados con proveedores de datos de confianza para aumentar sus perfiles de origen.

### Amplíe los datos de perfil y el modelo de gobernanza para dar cabida a los atributos proporcionados por los socios. {#extend-governance-model}

En este punto, está ampliando el marco de trabajo de administración de datos en Real-Time CDP para dar cabida a los atributos proporcionados por los socios.

Tiene la opción de crear un nuevo esquema del **[!UICONTROL Perfil individual de XDM]** o ampliar un esquema existente del mismo tipo para incluir atributos proporcionados por el socio. Adobe recomienda encarecidamente crear un nuevo esquema con un nuevo conjunto de grupos de campos que representen mejor los atributos adicionales del proveedor de datos. Esto garantiza que los esquemas de datos estén limpios y puedan evolucionar de forma independiente entre sí.

Para incluir atributos proporcionados por el socio en un esquema, puede crear un nuevo grupo de campos con los atributos esperados o utilizar uno de los grupos de campos preconfigurados proporcionados por Adobe.

Lea las páginas de documentación siguientes para obtener más información:

* [Conceptos básicos de composición de esquemas](/help/xdm/schema/composition.md)
* [Descripción general de [!UICONTROL Perfil individual de XDM] clase](/help/xdm/classes/individual-profile.md)
* [Crear y editar esquemas en la interfaz de usuario](/help/xdm/ui/resources/schemas.md)
* [Creación y edición de grupos de campos de esquema en la interfaz de usuario](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

También en este paso, piense en cómo cambia el modelo de gobernanza de datos a medida que amplía su estrategia de administración de datos para incluir datos de terceros proporcionados por el socio. Explore las consideraciones de los vínculos de documentación siguientes:

* (**Muy pronto**) Mantenga los datos de terceros en un conjunto de datos independiente para que sea fácil eliminarlos y deshacer integraciones.
* (**Muy pronto**) Use el [caducidad del conjunto de datos](/help/hygiene/ui/dataset-expiration.md) funcionalidad en el conjunto de datos para clientes que compraron el complemento de higiene de datos.
* (**Muy pronto**) Tenga cuidado al crear conjuntos de datos derivados que extraen datos de terceros, ya que una vez mezclados, la única solución para eliminar los datos de terceros es eliminar todo el conjunto de datos derivado.

>[!TIP]
>
>Si decide complementar los perfiles del cliente con un identificador basado en persona del proveedor de datos, puede crear un nuevo tipo de identidad del tipo **[[!UICONTROL ID de socio]](/help/identity-service/namespaces.md)**.
>
>Obtenga más información sobre el ID de socio en la [sección tipos de identidad](/help/identity-service/namespaces.md).
>Más información [definición de campos de identidad](/help/xdm/ui/fields/identity.md) en la interfaz de usuario del Experience Platform.

### Exportar audiencias que desee enriquecer cuando se introduzca información de identificación personal (PII) o PII con hash {#export-audiences}

Exporte las audiencias que desea que el socio enriquezca. Utilice los destinos de almacenamiento en la nube proporcionados por Real-Time CDP, como Amazon S3 o SFTP. Lea las siguientes páginas de documentación para completar este paso:

* [Amazon S3 destination](/help/destinations/catalog/cloud-storage/amazon-s3.md) página de documentación
* [Destino SFTP](/help/destinations/catalog/cloud-storage/sftp.md) página de documentación
* Cómo: [conexión a un destino](/help/destinations/ui/connect-destination.md)
* Cómo: [exportar datos a un destino de almacenamiento en la nube](/help/destinations/ui/activate-batch-profile-destinations.md)

### Su socio de datos adjunta atributos con licencia para los perfiles con los que pueden coincidir {#partner-appends-attributes}

En este paso, el socio de datos anexa atributos con licencia para la audiencia exportada. La salida suele estar disponible como archivo plano que se puede volver a introducir en Real-Time CDP. Más información sobre [ingesta de archivos en Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP anexa atributos enriquecidos al perfil del cliente {#ingest-data}

Ahora necesita introducir datos del socio a través de un conector de origen para devolver los datos enriquecidos a Real-Time CDP y complementar sus perfiles con datos proporcionados por el socio.

Algunos conectores de origen recomendados para este fin pueden ser:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitaciones y solución de problemas {#limitations-and-troubleshooting}

Tenga en cuenta las siguientes limitaciones a medida que explora el caso de uso descrito en esta página:

* Si decide utilizar ID de socio, tenga en cuenta que estos ID no se utilizan para crear su [gráfico de identidad](/help/identity-service/ui/identity-graph-viewer.md).

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

* (**Muy pronto**) [!BADGE Beta]{type=Informative}**Aproveche el reconocimiento asistido por socios** para personalizar las experiencias en el sitio durante la visita y para volver a direccionar las visitas posteriores fuera del sitio sin que el usuario se autentique ni tenga un historial anterior con su marca.
* (**Muy pronto**) [!BADGE Beta]{type=Informative}**Activación expandida** uso de ID de socio para publicar ecosistemas que no aceptan PII o PII con hash.