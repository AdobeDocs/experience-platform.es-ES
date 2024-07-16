---
title: Clase de directiva
description: Obtenga información acerca de la clase de directiva en el Modelo de datos de experiencia (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# clase [!UICONTROL Policy]

En Experience Data Model (XDM), la clase [!UICONTROL Policy] captura el conjunto mínimo de propiedades que definen una póliza de seguro.

![](../images/classes/policy.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `assignedBeneficiary` | Matriz de [[!UICONTROL tipos de datos de persona]](../data-types/person.md) | Registra el beneficiario (o beneficiarios) asignado a la póliza. |
| `benefitAmount` | [[!UICONTROL Moneda]](../data-types/currency.md) | El importe que se pagará según los términos de la póliza. |
| `location` | [[!UICONTROL Dirección postal]](../data-types/postal-address.md) | La ubicación en la que se emite la póliza de seguro. |
| `owner` | [!UICONTROL Objeto] | Registra la información de perfil del asegurado. |
| `owner.faxPhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | Número de teléfono del fax del propietario. |
| `owner.homeAddress` | [[!UICONTROL Dirección postal]](../data-types/postal-address.md) | La dirección de la casa del propietario. |
| `owner.homePhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | Número de teléfono de la casa del propietario. |
| `owner.mobilePhone` | [[!UICONTROL Número de teléfono]](../data-types/phone-number.md) | Número de teléfono móvil del propietario. |
| `owner.personalEmail` | [[!UICONTROL Dirección de correo electrónico]](../data-types/email-address.md) | La dirección de correo electrónico personal del propietario. |
| `ID` | [!UICONTROL Cadena] | Un identificador de la póliza de seguro. |
| `_id` | [!UICONTROL Cadena] | Un identificador de cadena único generado por el sistema para el registro. Este campo se utiliza para realizar un seguimiento de la exclusividad de un registro individual, evitar la duplicación de datos y buscar ese registro en servicios descendentes.<br><br>Dado que este campo es generado por el sistema, no se le proporciona un valor explícito durante la ingesta de datos. Sin embargo, puede optar por proporcionar sus propios valores de ID únicos si lo desea. |
| `endDate` | [!UICONTROL DateTime] | La fecha en la que finaliza (o finaliza) la cobertura de la póliza de seguro. |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica si la póliza tiene un beneficiario asignado. |
| `name` | [!UICONTROL Cadena] | El nombre de la póliza de seguro. |
| `startDate` | [!UICONTROL DateTime] | La fecha en la que comienza (o comienza) la cobertura de la póliza de seguro. |
| `type` | [!UICONTROL Cadena] | El tipo de póliza de seguro, como de vivienda, automóvil, alquiler o barco. |

{style="table-layout:auto"}
