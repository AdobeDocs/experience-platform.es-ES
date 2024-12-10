---
title: Grupo de campos de esquema de cobertura
description: Obtenga información acerca del grupo de campos Esquema de cobertura.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 7b84c0cf-3bd4-4ba8-a8cc-85e6b3f2b59e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# [!UICONTROL Cobertura] del grupo de campos de esquema

[!UICONTROL Cobertura] es un grupo de campos de esquema estándar para la [[!DNL Plan] clase](../../../classes/plan.md). Proporciona un único campo de tipo de objeto `healthcareCoverage` que está diseñado para proporcionar los identificadores y descriptores de alto nivel de un plan de seguro, normalmente la información que aparecería en una tarjeta de seguro, que se puede utilizar para pagar, en parte o en su totalidad, la prestación de productos y servicios de atención médica.

![Estructura del grupo de campos](../../../images/healthcare/field-groups/coverage/coverage.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Beneficiario del plan] | `beneficiary` | [[!UICONTROL Referencia]](../data-types/reference.md) | La parte que se beneficia de la cobertura del seguro y el paciente cuando se proporcionan los productos o servicios. |
| [!UICONTROL Clase] | `class` | Matriz de objetos | Un conjunto de clasificadores específicos de suscriptor. Consulte la [sección siguiente](#class) para obtener más información. |
| [!UICONTROL Contacto] | `contract` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Las pólizas que constituyen esta cobertura de seguro. |
| [!UICONTROL Costo Para Beneficiario] | `costToBeneficiary` | Matriz de objetos | Un conjunto de códigos que indican la categoría de coste y el importe asociado que se han detallado en la póliza y que pueden haberse incluido en la tarjeta sanitaria. Consulte la [sección siguiente](#cost-to-beneficiary) para obtener más información. |
| [!UICONTROL Excepción] | `exception` | Matriz de objetos | Un conjunto de códigos que indican excepciones o reducciones en los costes de los pacientes y sus períodos de vigencia. Consulte la [sección siguiente](#exception) para obtener más información. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | El identificador de la cobertura según lo emitido por el asegurador. |
| [!UICONTROL Plan de seguro] | `insurancePlan` | [[!UICONTROL Referencia]](../data-types/reference.md) | El plan de seguro detalla, beneficios y costes que constituyen esta cobertura de seguro. |
| [!UICONTROL Aseguradora] | `insurer` | [[!UICONTROL Referencia]](../data-types/reference.md) | El suscriptor del programa o plan, el pagador o la compañía de seguros. |
| [!UICONTROL Pago De] | `paymentBy` | Matriz de objetos | El enlace a la parte pagadora y, opcionalmente, lo que será responsable de pagar. Consulte la [sección siguiente](#payment-by) para obtener más información. |
| [!UICONTROL Fechas De Inicio Y Finalización De Cobertura] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Período de tiempo durante el cual la cobertura está activa. La falta de una fecha de inicio indica que la fecha de inicio no se conoce y que falta una fecha de finalización significa que la cobertura está en curso. |
| [!UICONTROL Titular de la póliza] | `policyHolder` | [[!UICONTROL Referencia]](../data-types/reference.md) | La parte que tiene la póliza de seguro. |
| [!UICONTROL Relación del beneficiario] | `relationship` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La relación del beneficiario con el suscriptor. |
| [!UICONTROL Suscriptor] | `subscriber` | [[!UICONTROL Referencia]](../data-types/reference.md) | La parte que mantiene la relación contractual con la póliza. |
| [!UICONTROL Identificador de suscriptor] | `subscriberId` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | El ID asignado del asegurador al suscriptor. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El tipo de cobertura. |
| [!UICONTROL Número dependiente] | `dependent` | Cadena | El designador de un dependiente bajo la cobertura. |
| [!UICONTROL Tipo] | `kind` | Cadena | El tipo de cobertura. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL Red de aseguradoras] | `network` | Cadena | La red de proveedores a la que el beneficiario puede solicitar un tratamiento que estará cubierto a la tasa dentro de la red; de lo contrario, se aplican los términos y condiciones fuera de la red. |
| [!UICONTROL Pedido de cobertura] | `order` | Entero | Orden relativo de la cobertura, con un valor mínimo de `0`. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de la cobertura. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL Subrogación] | `subrogation` | Booleano | Cuando `true`, esta instancia de seguro no se ha incluido para la adjudicación, sino para proporcionar a las aseguradoras los detalles para recuperar los costes. |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Estructura de clase](../../../images/healthcare/field-groups/coverage/class.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El tipo de clasificación para el que se proporciona una etiqueta de clase específica del asegurador, o un número y un nombre opcional. Por ejemplo, el tipo se puede usar para identificar una clase de cobertura, un grupo de empleadores, una póliza o un plan. |
| [!UICONTROL Valor] | `value` | [[!UICONTROL Identificador]](../data-types/identifier.md) | El identificador alfanumérico asociado con la etiqueta emitida por el asegurador. |
| [!UICONTROL Nombre] | `name` | Cadena | Breve descripción de la clase. |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Estructura de costo a beneficiario](../../../images/healthcare/field-groups/coverage/cost-to-beneficiary.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Categoría] | `category` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código para identificar el tipo general de beneficios bajo los cuales se proporcionan los productos y servicios. |
| [!UICONTROL Red] | `network` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código para indicar si los beneficios se refieren a proveedores dentro o fuera de la red. |
| [!UICONTROL Término] | `term` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El plazo de los valores, como el beneficio máximo a largo plazo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La categoría de costes centrados en el paciente asociados al tratamiento. |
| [!UICONTROL Unidad] | `unit` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Indica si los beneficios se aplican a una persona o a la familia. |

## `exception` {#exception}

`exception` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Estructura de excepciones](../../../images/healthcare/field-groups/coverage/exception.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El código de la excepción específica. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Periodo de tiempo en el que la excepción está activa. |

## `paymentBy` {#payment-by}

`paymentBy` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![Pago por estructura](../../../images/healthcare/field-groups/coverage/payment-by.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Fiesta] | `party` | [[!UICONTROL Referencia]](../data-types/reference.md) | La lista de partes que proporcionan pagos sin seguro por los costes de tratamiento. |
| [!UICONTROL Responsabilidad] | `responsibility` | Cadena | La descripción de la responsabilidad financiera. |
