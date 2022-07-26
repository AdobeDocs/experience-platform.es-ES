---
title: Grupo de campos de esquema de proveedor de atención médica
description: Este documento proporciona una descripción general del grupo de campos de esquema del proveedor de atención médica.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# [!UICONTROL Proveedor de atención médica] grupo de campos de esquema

[!UICONTROL Proveedor de atención médica] es un grupo de campos de esquema estándar para la variable [[!UICONTROL Proveedor] class](../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareProvider` que recoge propiedades relacionadas con un profesional de la salud o una organización de centros de salud autorizada para prestar servicios de diagnóstico y tratamiento de la salud.

![](../../images/field-groups/healthcare-provider.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `addressDetails` | Matriz de objetos | Muestra los detalles de dirección del proveedor. Cada objeto incluye las siguientes propiedades: <ul><li>`address`: ([[!UICONTROL Dirección postal]](../../data-types/postal-address.md)): La dirección postal del proveedor.</li><li>`addressType`: (Cadena) El tipo de dirección que indica dónde proporciona los servicios el proveedor.</li></ul> |
| `emailAddress` | [[!UICONTROL Dirección de correo electrónico]](../../data-types/email-address.md) | La dirección de correo electrónico del proveedor. |
| `fax` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de fax del proveedor. |
| `phoneNumber` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | El número de teléfono del proveedor. |
| `qualifications` | Matriz de objetos | Enumera las certificaciones, licencias o capacitación relacionadas con la prestación de atención. Cada objeto incluye las siguientes propiedades: <ul><li>`issuer`: ([[!UICONTROL Detalles de la cuenta]](../../data-types/account-details.md)): La organización que regula y emite la calificación.</li><li>`activePeriod`: (Número entero) El año hasta el cual es válida la calificación.</li><li>`code`: (Cadena) Una representación codificada de la cualificación.</li></ul> |
| `classification` | Cadena | Clasificación del proveedor de servicios basada en la clase o categoría (por ejemplo, atención al paciente, atención no al paciente, etc.). |
| `isActive` | Booleano | Indica si el proveedor está activo. |
| `languages` | Matriz de cadenas | Lista de idiomas en los que el proveedor realiza operaciones. |
| `practiceGroupName` | Cadena | El nombre del grupo de prácticas para el proveedor de servicios. |
| `practiceGroupType` | Cadena | Tipo de grupo de prácticas para el proveedor de servicios. |
| `practiceType` | Cadena | Tipo de práctica del proveedor de servicios. |
| `specialties` | Matriz de cadenas | Una lista de especialidades ofrecidas por este proveedor. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte la [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
