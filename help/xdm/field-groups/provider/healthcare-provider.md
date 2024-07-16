---
title: Grupo de campos de esquema de proveedor de atención médica
description: Obtenga información sobre el grupo de campos Esquema del proveedor de atención médica.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!UICONTROL Proveedor de atención médica] grupo de campos de esquema

[!UICONTROL Proveedor de atención médica] es un grupo de campos de esquema estándar para la clase [[!UICONTROL Proveedor]](../../classes/provider.md). Proporciona un único campo de tipo de objeto `healthcareProvider` que captura propiedades relacionadas con un profesional de la salud individual o una organización de instalaciones de salud con licencia para proporcionar servicios de diagnóstico y tratamiento de atención médica.

![](../../images/field-groups/healthcare-provider.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `addressDetails` | Matriz de objetos | Muestra los detalles de dirección del proveedor. Cada objeto incluye las siguientes propiedades: <ul><li>`address`: ([[!UICONTROL Dirección postal]](../../data-types/postal-address.md)): La dirección postal del proveedor.</li><li>`addressType`: (cadena) tipo de dirección que indica dónde proporciona servicios el proveedor.</li></ul> |
| `emailAddress` | [[!UICONTROL Dirección de correo electrónico]](../../data-types/email-address.md) | La dirección de correo electrónico del proveedor. |
| `fax` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | Número de fax del proveedor. |
| `phoneNumber` | [[!UICONTROL Número de teléfono]](../../data-types/phone-number.md) | Número de teléfono del proveedor. |
| `qualifications` | Matriz de objetos | Enumera las certificaciones, licencias o formación relacionadas con la prestación de atención. Cada objeto incluye las siguientes propiedades: <ul><li>`issuer`: ([[!UICONTROL Detalles de la cuenta]](../../data-types/account-details.md)): La organización que regula y emite la calificación.</li><li>`activePeriod`: (entero) año hasta el cual la calificación es válida.</li><li>`code`: (Cadena) Una representación codificada de la calificación.</li></ul> |
| `classification` | Cadena | La clasificación del proveedor de servicios basada en la clase o categoría (como atención al paciente, atención no médica, etc.). |
| `isActive` | Booleano | Indica si el proveedor está activo. |
| `languages` | Matriz de cadenas | Una lista de idiomas en los que el proveedor realiza operaciones. |
| `practiceGroupName` | Cadena | Nombre del grupo de práctica del proveedor de servicios. |
| `practiceGroupType` | Cadena | El tipo de grupo de práctica para el proveedor de servicios. |
| `practiceType` | Cadena | El tipo de práctica para el proveedor de servicios. |
| `specialties` | Matriz de cadenas | Una lista de especialidades ofrecidas por este proveedor. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
