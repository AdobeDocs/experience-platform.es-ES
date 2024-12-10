---
title: Grupo de campos de esquema de cuenta
description: Obtenga información acerca del grupo de campos Esquema de cuenta.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 376716bd-f79f-421d-b163-0f0e50876b48
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 7%

---

# [!UICONTROL Cuenta] grupo de campos de esquema

[!UICONTROL Account] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../../classes/individual-profile.md) y la [[!DNL Provider class]](../../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareAccount` que se utiliza para registrar transacciones, servicios y otra información financiera relacionada con los servicios de atención médica prestados a un paciente o a un grupo de personas (por ejemplo, con fines de póliza de seguro o facturación).

![Estructura del grupo de campos](../../../images/healthcare/field-groups/account/account.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Saldo] | `balance` | Matriz de objetos | Los saldos de cuenta que calcula y procesa el sistema financiero. Consulte la [sección-debajo](#balances) para obtener más información. |
| [!UICONTROL Estado de facturación] | `billingStatus` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Rastrea el ciclo de vida de la cuenta a través del proceso de facturación. Indica cómo se tratan las transacciones cuando se asignan a la cuenta. |
| [!UICONTROL Cobertura] | `coverage` | Matriz de objetos | La(s) parte(s) responsable(s) de cubrir los costes de esta cuenta y en qué orden deben aplicarse. Consulte la [sección siguiente](#coverage) para obtener más información. |
| [!UICONTROL Moneda] | `currency` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | La moneda predeterminada de la cuenta. |
| [!UICONTROL Diagnóstico] | `diagnosis` | Matriz de objetos | El conjunto de diagnósticos relevantes para la facturación se almacena aquí en la cuenta, donde se pueden secuenciar adecuadamente antes del procesamiento para producir reclamaciones. Consulte la [sección siguiente](#diagnosis) para obtener más información. |
| [!UICONTROL Garante] | `guarantor` | Matriz de objetos | Las partes responsables de equilibrar la cuenta si otras opciones de pago no son suficientes. Consulte la [sección siguiente](#guarantor) para obtener más información. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL identificador]](../data-types/identifier.md) | Un identificador único utilizado para hacer referencia a la cuenta. Puede o no estar destinado al uso humano (por ejemplo, número de tarjeta de crédito). |
| [!UICONTROL Propietario] | `owner` | [[!UICONTROL Referencia]](../data-types/reference.md) | Indica el área de servicio, el hospital, el departamento, etc. con responsabilidad en la administración de la cuenta. |
| [!UICONTROL Procedimiento] | `procedure` | Matriz de objetos | El conjunto de procedimientos relevantes para la facturación se almacena aquí en la cuenta, donde se pueden secuenciar adecuadamente antes del procesamiento para presentar reclamaciones. Consulte la [sección siguiente](#procedure) para obtener más información. |
| [!UICONTROL Cuenta relacionada] | `relatedAccount` | Matriz de objetos | Otras cuentas asociadas relacionadas con esta cuenta. Consulte la [sección siguiente](#related-account) para obtener más información. |
| [!UICONTROL Período de servicio] | `servicePeriod` | [[!UICONTROL Período]](../data-types/period.md) | El intervalo de fechas de los servicios asociados con esta cuenta. |
| [!UICONTROL Asunto] | `subject` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Identifica la entidad que incurre en los gastos. Si bien los destinatarios inmediatos de los servicios o bienes pueden ser entidades relacionadas con el tema, los gastos fueron finalmente incurridos por el sujeto de la cuenta. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Clasifica la cuenta con fines de creación de informes y búsqueda. |
| [!UICONTROL Calculado A Las] | `calculatedAt` | Fecha/Hora | La hora en que se calculó el saldo. |
| [!UICONTROL Descripción] | `description` | Cadena | Proporciona información adicional sobre qué rastrea la cuenta y cómo se utiliza. |
| [!UICONTROL Nombre] | `name` | Cadena | El nombre de la cuenta. |
| [!UICONTROL Estado] | `status` | Cadena | El estado de la cuenta. El valor de esta propiedad debe ser igual a uno de los siguientes valores de enumeración conocidos. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> <li> `on-hold` </li> <li> `unknown`</li> |

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.schema.json)

## `balances` {#balances}

`balances` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de saldos](../../../images/healthcare/field-groups/account/balance.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Agregar] | `aggregate` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Quién se espera que pague esta parte del saldo. |
| [!UICONTROL Importe] | `amount` | [[!UICONTROL Dinero]](../data-types/money.md) | El saldo real calculado para la edad definida en la propiedad term. |
| [!UICONTROL Término] | `term` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | El término de la cuenta. |
| [!UICONTROL Estimación] | `estimate` | Booleano | Si la cantidad es un valor estimado. |

## `coverage` {#coverage}

`coverage` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de cobertura](../../../images/healthcare/field-groups/account/coverage.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Cobertura] | `coverage` | [[!UICONTROL Referencia]](../data-types/reference.md) | La(s) parte(s) responsable(s) de cubrir los costes de esta cuenta y en qué orden deben aplicarse. |
| [!UICONTROL Prioridad] | `priority` | Entero | Prioridad de la cobertura en el contexto de esta cuenta, con un valor mínimo de `0`. |

## `diagnosis` {#diagnosis}

`diagnosis` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de diagnóstico](../../../images/healthcare/field-groups/account/diagnosis.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Condición] | `condition` | [[!UICONTROL Referencia codificable]](../data-types/codeable-reference.md) | El diagnóstico relevante para la cuenta. |
| [!UICONTROL Código de paquete] | `packageCode` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El código del paquete se puede utilizar para agrupar los diagnósticos que se pueden cotizar o entregar como un solo producto (como los fármacos). |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Tipo que este diagnóstico tiene relevante para la cuenta (por ejemplo, admisión, facturación, alta...). |
| [!UICONTROL Fecha Del Diagnóstico] | `dateOfDiagnosis` | Fecha/Hora | Fecha del diagnóstico (cuando está codificado). |
| [!UICONTROL Al Ingresar] | `onAdmission` | Booleano | Si el diagnóstico estaba presente al ingreso. |
| [!UICONTROL Secuencia] | `sequence` | Entero | Clasificación del diagnóstico (para cada tipo), con un valor mínimo de `0`. |

## `guarantor` {#guarantor}

`guarantor` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de garante](../../../images/healthcare/field-groups/account/guarantor.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Fiesta] | `party` | [[!UICONTROL Referencia]](../data-types/reference.md) | La entidad responsable. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../data-types/period.md) | Plazo durante el cual el garante acepta la responsabilidad de la cuenta. |
| [!UICONTROL En espera] | `onHold` | Booleano | El avalista podrá ser objeto de una retención de crédito o de una suspensión temporal de su función. |

## `procedure` {#procedure}

`procedure` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura de procedimiento](../../../images/healthcare/field-groups/account/procedure.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Código] | `code` | [[!UICONTROL Referencia codificable]](../data-types/codeable-reference.md) | El procedimiento relacionado con la cuenta. |
| [!UICONTROL Dispositivo] | `device` | Matriz de [[!UICONTROL referencia]](../data-types/reference.md) | Cualquier dispositivo asociado con el procedimiento correspondiente a la cuenta. |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | Cómo se debe utilizar el valor del procedimiento para cargar la cuenta. |
| [!UICONTROL Código de paquete] | `packageCode` | Matriz de [[!UICONTROL concepto codificable]](../data-types/codeable-concept.md) | El código del paquete se puede utilizar para agrupar procedimientos que se pueden cotizar o entregar como un solo producto (como los DRG). |
| [!UICONTROL Fecha De Servicio] | `dateOfService` | Fecha/Hora | La fecha cuando se utiliza un procedimiento codificado. Si se utiliza una referencia a un procedimiento, se debe utilizar la fecha del procedimiento. |
| [!UICONTROL Secuencia] | `sequence` | Entero | Clasificación del procedimiento (para cada tipo), con un valor mínimo de `0`. |

## `relatedAccount` {#related-account}

`relatedAccount` se proporciona como una matriz de objetos. A continuación se describe la estructura de cada objeto.

![estructura relatedAccount](../../../images/healthcare/field-groups/account/related-account.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
| --- | --- | --- | --- |
| [!UICONTROL Cuenta] | `account` | [[!UICONTROL Referencia]](../data-types/reference.md) | Referencia a una cuenta asociada. |
| [!UICONTROL Relación] | `relationship` | [[!UICONTROL Concepto codificable]](../data-types/codeable-concept.md) | Relación de la cuenta asociada. |
