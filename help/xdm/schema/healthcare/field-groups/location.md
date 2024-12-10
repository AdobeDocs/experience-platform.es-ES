---
title: Grupo de campos del esquema de ubicación
description: Obtenga información acerca del grupo de campos Esquema de ubicación.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# [!UICONTROL Ubicación] grupo de campos de esquema

[!UICONTROL Ubicación] es un grupo de campos de esquema estándar para la [[!DNL Location] clase](../classes/location.md). Proporciona un único campo de tipo de objeto `healthcareLocation` que captura detalles e información de posición de un lugar.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/location.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Dirección] | `address` | [[!UICONTROL Dirección]](../data-types/address.md) | La dirección de la ubicación física. |
| [!UICONTROL Característica] | `characteristic` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Una colección de las características de la ubicación. |
| [!UICONTROL Contacto] | `contact` | Matriz de [[!UICONTROL detalles de contacto extendidos]](../data-types/extended-contact-detail.md) | Los datos de contacto de la ubicación. |
| [!UICONTROL Extremo] | `endpoint` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Los extremos técnicos que proporcionan acceso a los servicios operativos de la ubicación. |
| [!UICONTROL Formulario] | `form` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La forma física de la ubicación. |
| [!UICONTROL Horas de operación] | `hoursOfOperation` | Matriz de [[!UICONTROL disponibilidad]](../data-types/availability.md) | Qué días y horas suele estar abierta esta ubicación (incluidas las excepciones). |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | El código o número único que identifica la ubicación. |
| [!UICONTROL Administrar organización] | `managingOrganization` | [[!UICONTROL Referencia]](../data-types/reference.md) | La organización responsable del aprovisionamiento y el mantenimiento. |
| [!UICONTROL Estado operativo] | `operationalStatus` | [[!UICONTROL Codificación]](../data-types/coding.md) | El estado operativo de la ubicación. |
| [!UICONTROL Parte De La Ubicación] | `partOf` | [[!UICONTROL Referencia]](../data-types/reference.md) | La ubicación de la que forma parte esta ubicación. |
| [!UICONTROL Posición] | `position` | Objeto | La situación geográfica absoluta. Contiene tres propiedades en formato Double: <li>`longitude`: longitud con datos WGS84</li> <li>`latitude`: latitud con datos WGS84.</li> <li>`altitude`: Altitud con datos WGS84.</li> |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El tipo de función realizada en la ubicación. |
| [!UICONTROL Servicio virtual] | `virtualService` | Matriz de [[!UICONTROL detalles de servicio virtual]](../data-types/virtual-service-detail.md) | Los detalles de conexión de un servicio virtual. |
| [!UICONTROL Alias] | `alias` | Matriz de cadenas | Una lista de nombres alternativos que la ubicación es o era conocida como. |
| [!UICONTROL Descripción] | `description` | Cadena | Más información para identificar la ubicación más allá de su nombre. |
| [!UICONTROL Modo] | `mode` | Cadena | El modo de la ubicación. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Nombre] | `name` | Cadena | El nombre de la ubicación. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de la ubicación. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
